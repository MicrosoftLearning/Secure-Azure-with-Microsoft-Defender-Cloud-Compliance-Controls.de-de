---
lab:
  title: "Übung\_07: Herstellen einer Verbindung mit einem Azure\_SQL-Server über einen privaten Azure-Endpunkt im Azure-Portal"
  module: Module 08 - Connect to an Azure SQL server using an Azure Private Endpoint using the Azure portal
---


>**Hinweis**: Für dieses Lab benötigen Sie ein [Azure-Abonnement](https://azure.microsoft.com/en-us/free/?azure-portal=true), in dem Sie über Administratorzugriff verfügen. 


Der private Azure-Endpunkt ist der grundlegende Baustein für Private Link in Azure. Mit Azure-Ressourcen wie VMs können Sie privat und sicher mit Private Link-Ressourcen wie einem Azure SQL-Server kommunizieren.

---

## Qualifikationsaufgaben

- Erstellen eines virtuellen Netzwerks und eines Bastion-Hosts.
  
- Erstellen Sie eine VM.
  
- Erstellen eines Azure SQL-Servers und eines privaten Endpunkts.
  
- Testen der Konnektivität mit dem privaten Endpunkt für SQL Server

## Übungsanweisungen 

### Erstellen Sie eine Ressourcengruppe und ein virtuelles Netzwerk.

>**Hinweis:** Der Bastion-Host wird verwendet, um eine sichere Verbindung mit dem virtuellen Computer herzustellen, um den privaten Endpunkt zu testen. 

1. Starten Sie eine Browsersitzung, und melden Sie sich beim [Azure-Portal-Menü](https://portal.azure.com/) an.
   
2. Geben Sie im Suchfeld oben im Portal **Virtuelle Netzwerke** ein. Wählen Sie in den Suchergebnissen **Virtuelle Netzwerke** aus.

3. Wählen Sie auf der Seite **Virtuelle Netzwerke** die Option **+ Erstellen** aus.

4. Geben Sie unter **Virtuelles Netzwerk erstellen** auf der Registerkarte **Grundlagen** die folgenden Informationen ein, oder wählen Sie sie aus:
   
   |Einstellung|Wert|
   |---|---|
   |**Projektdetails**|
   |Subscription|Wählen Sie Ihr Abonnement aus.|
   |Resource group|Wählen Sie **az-rg-1** aus.|
   |**Instanzendetails**|
   |Name des virtuellen Netzwerks|Geben Sie **vnet-2** ein.|
   |Region|Wählen Sie **(USA) USA, Osten** aus.|  
    
5. Wählen Sie **Weiter** aus, um zur Registerkarte **Sicherheit** zu gelangen.
  
6. Wählen Sie **Azure Bastion aktivieren** im Abschnitt "Azure Bastion" auf der Registerkarte "Sicherheit" aus.

   >**Hinweis**: Azure Bastion ist ein kostenpflichtiger Dienst, der eine sichere RDP/SSH-Verbindung zu Ihren virtuellen Computern über TLS bereitstellt. Beim Herstellen einer Verbindung über Azure Bastion benötigen Ihre virtuellen Computer keine öffentliche IP-Adresse. 

7. Geben Sie die folgenden Informationen im Feld **Azure Bastion** ein, oder wählen Sie sie aus:

   |Einstellung|Wert|
   |---|---|
   |**Projektdetails**|
   |Azure Bastion-Host |Geben Sie **az-bastionhost-1a** ein.|
   |Öffentlicher Azure Bastion-IP-Adressenname|Wählen Sie **Öffentliche IP-Adresse erstellen** aus.|
   |Öffentliche IP-Adresse hinzufügen|Wählen Sie **OK** aus.|

9. Wählen Sie **Weiter** aus, um zur Registerkarte **IP-Adressen** zu gelangen.

10. Klicken Sie im vorhandenen konfigurierten **IPv4-Adressraum** in der Spalte **Subnetze** auf den Eintrag **Standard**.

11. Geben Sie in der Vorlage **Subnetz bearbeiten** die folgenden Informationen ein, oder wählen Sie sie aus:

    |Einstellung|Wert|
    |---|---|
    |**Projektdetails**|
    |Subnetzzweck|Behalten Sie die Standardeinstellung bei.|
    |Name|**subnet-2**|
    |IPv4-Adressbereich|Behalten Sie den Standardwert als „10.0.0.0/16“ bei.|
    |Startadresse|Behalten Sie den Standardwert als „/24(256 addresses)“ bei.|

13. Wählen Sie unten auf der Seite **Subnetz bearbeiten** die Option **Speichern** aus.

14. Wählen Sie unten auf der Seite **IP-Adressen** die Option **Überprüfen + erstellen** aus.

    >**Hinweis:** Es kann bis zu 15 Minuten dauern, bis die Instanziierung der Bastion-Bereitstellung vollständig abgeschlossen ist.

15. Wählen Sie unten auf der Seite **Überprüfen + erstellen** die Option **Erstellen** aus.
 
### Erstellen Sie eine VM.

>**Hinweis**: In dieser Aufgabe erstellen Sie einen virtuellen Computer zum Testen des privaten Endpunkts.

1. Suchen Sie im Portal nach **Virtuelle Computer**, und klicken Sie darauf.

2. Wählen Sie unter **VM** die Option **+ Erstellen** und dann **Azure-VM** aus.

3. Geben Sie diese Informationen auf der Seite **Grundlagen** ein oder wählen Sie sie aus, wenn Sie einen virtuellen Computer erstellen:

   |Einstellung|Wert|
   |---|---|
   |**Projektdetails**|
   |Abonnement|Wählen Sie Ihr Abonnementaus.|
   |Resource group|Wählen Sie **az-rg-1** aus.|
   |**Instanzendetails**|
   |Name des virtuellen Computers|Geben Sie **vm-3** ein.|
   |Region|Wählen Sie **(USA) USA, Osten** aus.|
   |Verfügbarkeitsoptionen|Wählen Sie im Dropdownmenü „Verfügbarkeitszone“ die Option **Keine Infrastrukturredundanz erforderlich** aus.|
   |Sicherheitstyp|Wählen Sie im Dropdownmenü „Sicherheitstyp“ die Option **Standard** aus.|
   |Abbildung|Wählen Sie **Windows Server 2022 Datacenter – x64 Gen2** aus.|
   |VM-Architektur|Wählen Sie **x64** aus.|
   |Mit Azure Spot-Rabatt ausführen|Behalten Sie die Standardeinstellung als deaktiviert bei.|
   |Größe|Behalten Sie die Standardeinstellung bei: Standard_D2s_v3-2 vcpus, 8 GiB memory.|
   |**Administratorkonto**|
   |Benutzername|Geben Sie **Tenantadmin2** ein.|
   |Kennwort|Geben Sie **Superuser#170** ein.|
   |Kennwort bestätigen|Geben Sie erneut **Superuser#170** ein.|
   |**Regeln für eingehende Ports**|
   |Eingangsports auswählen|Wählen Sie **Keine**.|

5. Wählen Sie **Weiter: Datenträger** und dann **Weiter: Netzwerk** aus.
  
6. Geben Sie auf der Seite **Netzwerk** die folgenden Informationen ein, bzw. wählen Sie sie aus:

   |Einstellung|Wert|
   |---|---|
   |**Netzwerkschnittstelle**|
   |Virtuelles Netzwerk|Wählen Sie **vnet-2** aus.|
   |Subnet|Wählen Sie **subnet-2 (10.0.0.0/24)** aus.|
   |Öffentliche IP-Adresse|Wählen Sie **Keine** aus.|
   |NIC-Netzwerksicherheitsgruppe|Wählen Sie **Basic** aus.|
   |Öffentliche Eingangsports|Wählen Sie **Keine**.|
   |Eingangsports auswählen|Behalten Sie die Einstellung als „Leer“ bei.|
   |Löschen Sie die NIC beim Löschen des virtuellen Computers|Behalten Sie die Standardeinstellung als „Aktivieren des beschleunigten Netzwerkbetriebs“ bei.|
   |Lastenausgleich|Behalten Sie die Standardeinstellung „Keine“ bei.|
  
6. Klicken Sie auf **Überprüfen + erstellen**.

7. Überprüfen Sie die Einstellungen, und wählen Sie dann die Option **Erstellen**.

### Erstellen eines Azure SQL-Servers und eines privaten Endpunkts

>**Hinweis**: In diesem Abschnitt erstellen Sie einen SQL-Server in Azure.

1. Geben Sie in das Suchfeld oben auf dem Portal **SQL-Datenbank** ein. Wählen Sie in den Suchergebnissen **SQL-Datenbanken** aus.

2. Klicken Sie auf der Seite **SQL-Datenbanken** auf **+ Erstellen**.
   
3. Geben Sie unter **SQL-Datenbank erstellen** auf der Registerkarte **Grundlagen** die folgenden Informationen ein, bzw. wählen Sie sie aus:

   |Einstellung|Wert|
   |---|---|
   |**Projektdetails**|
   |Subscription|Wählen Sie Ihr Abonnement aus.|
   |Resource group|Wählen Sie **az-rg-1** aus.|
   |**Datenbankdetails**|
   |Datenbankname|Geben Sie **az-sql-db1a** ein.|
   |Servername|Geben Sie **az-sql-svr1a** ein. Wenn dieser Name vergeben ist, erstellen Sie einen eindeutigen Namen.|
   |Standort|Wählen Sie **(USA) USA, Osten** aus.|
   |**Authentifizierung**|
   |Authentifizierungsmethode|Wählen Sie **SQL-Authentifizierung verwenden** aus.|
   |Serveradministratoranmeldung|Geben Sie **Tenantadmin2** ein.|
   |Kennwort|Geben Sie **Superuser#170** ein.|
   |Kennwort bestätigen|Geben Sie **Superuser#170** ein.|

4. Klickan Sie auf **OK**.
   
   |Einstellung|Wert|
   |---|---|
   |**Datenbankdetails**|
   |Möchten Sie einen Pool für elastische SQL-Datenbanken verwenden?|Behalten Sie die Standardeinstellung als „Nein“ bei.|
   |Workloadumgebung|Behalten Sie die Standardeinstellung als Entwicklung bei.|
   |Compute + Speicher|Behalten Sie die Standardeinstellung als „Universell – serverlos“ bei.|
   |**Redundanz für Sicherungsspeicher**|
   |Redundanz für Sicherungsspeicher|Wählen Sie **Lokal redundanter Sicherungsspeicher** aus.|
   
5. Wählen Sie die Registerkarte **Netzwerk** oder die Schaltfläche **Weiter: Netzwerk**.

6. Geben Sie auf der Registerkarte **Netzwerk** die folgenden Informationen ein, bzw. wählen Sie sie aus:

   |Einstellung|Wert|
   |---|---|
   |**Netzwerkkonnektivität**|
   |Konnektivitätsmethode|Wählen Sie **Privater Endpunkt** aus.|
   |Verbindungsrichtlinie|Behalten Sie die Standardeinstellung bei: Standard – Verwendet die Umleitungsrichtlinie für alle Clientverbindungen, die innerhalb von Azure (außer Verbindungen mit privaten Endpunkten) und den Proxy für alle Clientverbindungen, die von außerhalb von Azure stammen.|
   |Verschlüsselungsverbindungen|Behalten Sie die Standardeinstellung als „TLS.12“ bei.|

7. Wählen Sie unter **Private Endpunkte** die Option **+ Privaten Endpunkt hinzufügen** aus.

8. Geben Sie unter **Privaten Endpunkt erstellen** diese Informationen ein, oder wählen Sie sie aus:

   |Einstellung|Wert|
   |---|---|
   |Subscription|Wählen Sie Ihr Abonnement aus.|
   |Resource group|Wählen Sie **az-rg-1** aus.|
   |Location|Wählen Sie **USA, Osten** aus.|
   |Name|Geben Sie **az-pe-1a** ein.|
   |Zielunterressource|Behalten Sie die Standardeinstellung als „SqlServer“ bei.|
   |**Netzwerk**|
   |Virtuelles Netzwerk|Wählen Sie **vnet-2** aus.|
   |Subnet|Wählen Sie **subnet-2** aus.|
   |**Private DNS-Integration**|
   |Integrieren in eine private DNS-Zone|Behalten Sie die Standardeinstellungen als „Ja“ bei.|
   |Private DNS-Zone|Behalten Sie die Standardeinstellung als „(New) privatelink.database.windows.net“ bei|

9. Wählen Sie **OK** aus.

10. Klicken Sie auf **Überprüfen + erstellen**.

11. Klicken Sie auf **Erstellen**.

### Deaktivieren des öffentlichen Zugriffs auf logische Azure SQL-Server

>**Hinweis**: Gehen Sie für dieses Szenario davon aus, dass Sie den gesamten öffentlichen Zugriff auf Ihren Azure SQL-Server deaktivieren und nur Verbindungen aus Ihrem virtuellen Netzwerk zulassen möchten. Die Einstellung **Öffentlicher Zugriff** ist möglicherweise standardmäßig auf **Deaktivieren** gesetzt.

1. Geben Sie im Suchfeld des Azure-Portals **az-sql-svr1a** oder den Servernamen ein, den Sie in den vorherigen Schritten eingegeben haben.

2. Wählen Sie **Netzwerk** aus dem Abschnitt **Sicherheit** von **az-sql-svr1a** aus. Wählen Sie auf der Seite **Netzwerk** die Registerkarte **Öffentlicher Zugriff** aus, und wählen Sie dann **Deaktivieren** für **Öffentlicher Netzwerkzugriff** aus.

   ![image](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/44ff5c24-70cf-49ed-b2ab-5e210c478b3a)

3. Wählen Sie **Speichern**.

### Testen der Verbindung mit dem privaten Endpunkt

>**Hinweis**: In diesem Abschnitt verwenden Sie den virtuellen Computer, den Sie in den vorherigen Schritten erstellt haben, um über den privaten Endpunkt eine Verbindung mit dem SQL-Server herzustellen.

1. Wählen Sie **Ressourcengruppen** im linken Navigationsbereich aus.

2. Wählen Sie **az-rg-1** aus.

3. Wählen Sie **vm-3** aus.

4. Wählen Sie auf der Übersichtsseite für **vm-3** „Verbinden“ und dann **Bastion** aus.

5. Geben Sie den Benutzernamen **Tenantadmin2** und das Kennwort **Superuser#170** ein, die Sie beim Erstellen des virtuellen Computers festgelegt haben.

   **Wichtig:** Wechseln Sie zu den Edge-Einstellungen/Popups und Umleitungen, und schalten Sie die Option „Blockiert“ auf **Aus** um, bevor Sie „Verbinden“ auswählen.

7. Wählen Sie die Schaltfläche **Verbinden** aus.
  
8. Öffnen Sie Windows PowerShell auf dem Server, nachdem Sie eine Verbindung hergestellt haben.

9. Geben Sie `nslookup sqlserver-name.database.windows.net.` ein, und ersetzen Sie **sqlserver-name** durch den Namen des SQL-Servers, den Sie in den vorherigen Schritten erstellt haben. Sie erhalten eine Meldung ähnlich der folgenden:

   ````  
   Server:  UnKnown
   Address:  168.63.129.16
   
   Non-authoritative answer:
   Name:    az-sql-svr1a.privatelink.database.windows.net
   Address:  10.1.0.5
   Aliases:  az-sql-svr1a.database.windows.net
   ````
    
>**Hinweis**: Als Name für den SQL-Server wird die private IP-Adresse 10.1.0.5 zurückgegeben. Diese Adresse befindet sich im Subnetz **az-sql-svr1a** des zuvor von Ihnen erstellten virtuellen Netzwerks **vnet-2**.

9. Installieren Sie [SQL Server Management Studio](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?preserve-view=true&view=sql-server-2017) auf **vm-3**.
 
10. Öffnen Sie **SQL Server Management Studio**.

11. Geben Sie unter **Mit Server verbinden** diese Informationen ein, oder wählen Sie sie aus:

    |Einstellung|Wert|
    |---|---|
    |Servertyp|Wählen Sie **Datenbank-Engine** aus.|
    |Servername|Geben Sie **az-sql-svr1a.database.windows.net** ein.|
    |Authentifizierung|Wählen Sie **SQL Server-Authentifizierung** aus.|
    |Benutzername|Geben Sie **Tenantadmin2** ein.|
    |Kennwort|Geben Sie **Superuser#170** ein.|
    |Kennwort speichern|Wählen Sie **Ja** aus.|
    |Konnektivitätssicherheit|
    |Verschlüsselung|Behalten Sie die Standardeinstellung als „Obligatorisch“ bei.|
   
13. Wählen Sie **Verbinden**.

14. Durchsuchen Sie Datenbanken im linken Menü.

15. Schließen Sie die Remotedesktopverbindung mit vm-3.
  
> **Ergebnisse**: Sie haben über das Azure-Portal eine Verbindung mit einem Azure SQL-Server über einen privaten Azure-Endpunkt hergestellt.
