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
   
2. Wählen Sie im Menü des Azure-Portals + **Ressource erstellen** > **Netzwerk** > **Virtuelles Netzwerk** aus, oder suchen Sie im Suchfeld des Portals nach „Virtuelles Netzwerk“.

3. Klicken Sie auf **Erstellen**.

4. Geben Sie unter **Virtuelles Netzwerk erstellen** auf der Registerkarte **Grundlagen** die folgenden Informationen ein, oder wählen Sie sie aus:
   
   |Einstellung|Wert|
   |---|---|
   |**Projektdetails**|
   |Subscription|Wählen Sie Ihr Abonnement aus.|
   |Resource group|Wählen Sie **Neu erstellen**. Geben Sie **CreateSQLEndpointTutorial** ein. Klicken Sie auf **OK**.|
   |**Instanzendetails**|
   |Name des virtuellen Netzwerks|Geben Sie **myVNet1a** ein.|
   |Region|Wählen Sie **(USA) USA, Osten** aus.|  
    
5. Wählen Sie **Weiter** aus, um zur Registerkarte **Sicherheit** zu gelangen.
  
6. Wählen Sie **Azure Bastion aktivieren** im Abschnitt "Azure Bastion" auf der Registerkarte "Sicherheit" aus.

   >**Hinweis:** Azure Bastion verwendet Ihren Browser, um mithilfe der privaten IP-Adressen eine Verbindung mit virtuellen Computern in Ihrem virtuellen Netzwerk über Secure Shell (SSH) oder Remotedesktopprotokoll (RDP) herzustellen. Die VMs benötigen keine öffentlichen IP-Adressen, keine Clientsoftware und keine spezielle Konfiguration.

7. Geben Sie die folgenden Informationen im Feld **Azure Bastion-Hostname** ein, oder wählen Sie sie aus:

   |Einstellung|Wert|
   |---|---|
   |Azure Bastion-Hostname|Geben Sie **myBastionHost** ein.|
   |Öffentlicher Azure Bastion-IP-Adressenname|Wählen Sie **Öffentliche IP-Adresse erstellen** aus.|
   |Hinzufügen einer öffentlichen IP-Adresse|Geben Sie **my-bstn-public-ip** ein.|
   |SKU|Übernehmen Sie den Standardwert **Standard**.|
   
8. Klickan Sie auf **OK**.

9. Wählen Sie **Weiter** aus, um zur Registerkarte **Sicherheit** zu gelangen.

10. Wählen Sie **Weiter** aus, um zur Registerkarte **IP-Adressen** zu gelangen.

11. Wählen Sie im Feld "Adressraum" in der Spalte "Subnetze" das Wort **default** Subnetz aus.

12. Geben Sie in der Vorlage **Subnetz bearbeiten** die folgenden Informationen ein, oder wählen Sie sie aus:

   |Einstellung|Wert|
   |---|---|
   |Subnetzzweck|Übernehmen Sie den Standardwert **Default**.|
   |Name|Geben Sie **mysubnet1a** ein.|
   |IPv4-Adressbereich|Übernehmen Sie den Standardwert **10.0.0.0**.|
   |Startadresse|Übernehmen Sie den Standardwert **/24 (256 Adressen)**.|

13. Wählen Sie **Speichern**.

14. Wählen Sie am unteren Bildschirmrand **Überprüfen + erstellen** aus, und wenn die Validierung erfolgreich ist, wählen Sie **Erstellen** aus.

    >**Hinweis:** Es kann bis zu 15 Minuten dauern, bis die Instanziierung der Bastion-Bereitstellung vollständig abgeschlossen ist.
 
### Erstellen Sie eine VM.

>**Hinweis**: In dieser Aufgabe erstellen Sie einen virtuellen Computer zum Testen des privaten Endpunkts.

1. Wählen Sie im Menü des Azure-Portals + **Ressource erstellen** > **Compute** > **Virtueller Computer** aus, oder suchen Sie im Suchfeld des Portals nach **Virtueller Computer**.
   
2. Geben Sie unter **Virtuellen Computer erstellen** auf der Registerkarte **Grundlagen** die folgenden Werte ein, oder wählen Sie sie aus:

   |Einstellung|Wert|
   |---|---|
   |**Projektdetails**|
   |Abonnement|Wählen Sie Ihr Abonnement aus.|
   |Resource group|Wählen Sie **CreateSQLEndpointTutorial** aus.|
   |**Instanzendetails**|
   |Name des virtuellen Computers|Geben Sie **myVM** ein.|
   |Region|Wählen Sie **(USA) USA, Osten** aus.|
   |Verfügbarkeitsoptionen|Wählen Sie im Dropdownmenü „Verfügbarkeitszone“ die Option **Keine Infrastrukturredundanz erforderlich** aus.|
   |Sicherheitstyp|Wählen Sie im Dropdownmenü „Sicherheitstyp“ die Option **Standard** aus.|
   |Abbildung|Wählen Sie **Windows Server 2022 Datacenter – x64 Gen2** aus.|
   |VM-Architektur|Wählen Sie **x64** aus.|
   |Mit Azure Spot-Rabatt ausführen|Übernehmen Sie die Standardeinstellung (deaktiviert)|
   |Größe|Übernehmen Sie den Standardwert **Standard_D2s_v3 – 2 vCPUs, 8 GiB Arbeitsspeicher.**|
   |**Administratorkonto**|
   |Authentifizierungsart|Wählen Sie **Kennwort** aus.|
   |Username|Geben Sie **Tenantadmin2** ein.|
   |Kennwort|Geben Sie **Superuser#170** ein.|
   |Kennwort bestätigen|Geben Sie erneut **Superuser#170** ein.|
   |**Regeln für eingehende Ports**|
   |Eingangsports auswählen|Wählen Sie **Keine**.|

4. Wählen Sie die Registerkarte **Netzwerk** aus, oder wählen Sie **Weiter: Datenträger** und anschließend **Weiter: Netzwerk** aus.
  
5. Geben Sie auf der Registerkarte **Netzwerk** die folgenden Informationen ein, bzw. wählen Sie sie aus:

   |Einstellung|Wert|
   |---|---|
   |**Netzwerkschnittstelle**|
   |Virtuelles Netzwerk|Wählen Sie **myVNet1a** aus.|
   |Subnet|Wählen Sie **mySubnet1a** aus.|
   |Öffentliche IP-Adresse|Wählen Sie **Keine** aus.|
   |NIC-Netzwerksicherheitsgruppe|Wählen Sie **Basic** aus.|
   |Öffentliche Eingangsports|Wählen Sie **Keine**.|
  
6. Klicken Sie auf **Überprüfen + erstellen**.

7. Überprüfen Sie die Einstellungen, und wählen Sie dann die Option **Erstellen**.

### Erstellen eines Azure SQL-Servers und eines privaten Endpunkts

>**Hinweis**: In diesem Abschnitt erstellen Sie einen SQL-Server in Azure.

1. Wählen Sie im Azure-Portal im Menü die Option + **Ressource erstellen** > **Datenbanken** > **SQL-Datenbank** aus.
   
2. Geben Sie unter **SQL-Datenbank erstellen** auf der Registerkarte **Grundlagen** die folgenden Informationen ein, bzw. wählen Sie sie aus:

   |Einstellung|Wert|
   |---|---|
   |**Projektdetails**|
   |Subscription|Wählen Sie Ihr Abonnement aus.|
   |Resource group|Wählen Sie **CreateSQLEndpointTutorial** aus.|
   |**Datenbankdetails**|
   |Datenbankname|Geben Sie **mysqldatabase** ein.|
   |Server|Wählen Sie **Neu erstellen**.|  

3. Geben Sie unter **Neuen SQL-Datenbank-Server erstellen** diese Informationen ein, oder wählen Sie sie aus:
  
   |Einstellung|Wert|
   |---|---|
   |**Serverdetails**|
   |Servername|Geben Sie **mysqlserver1a** ein. Wenn dieser Name vergeben ist, erstellen Sie einen eindeutigen Namen.|
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
   |Möchten Sie einen Pool für elastische SQL-Datenbanken verwenden?|Wählen Sie **Nein** aus.|
   |Compute und Speicher|Wählen Sie Standardeinstellungen oder **Datenbank konfigurieren** aus, um Compute- und Speichereinstellungen zu konfigurieren.|
   |**Redundanz für Sicherungsspeicher**|
   |Redundanz für Sicherungsspeicher|Wählen Sie **Lokal redundanter Sicherungsspeicher** aus.|
   
5. Wählen Sie die Registerkarte **Netzwerk** oder die Schaltfläche **Weiter: Netzwerk**.

6. Geben Sie auf der Registerkarte **Netzwerk** die folgenden Informationen ein, bzw. wählen Sie sie aus:

   |Einstellung|Wert|
   |---|---|
   |**Netzwerkkonnektivität**|
   |Konnektivitätsmethode|Wählen Sie **Privater Endpunkt** aus.|

7. Wählen Sie unter **Private Endpunkte** die Option **+ Privaten Endpunkt hinzufügen** aus.

8. Geben Sie unter **Privaten Endpunkt erstellen** diese Informationen ein, oder wählen Sie sie aus:

   |Einstellung|Wert|
   |---|---|
   |Subscription|Wählen Sie Ihr Abonnement aus.|
   |Resource group|Wählen Sie **CreateSQLEndpointTutorial** aus.|
   |Standort|Wählen Sie **USA, Osten** aus.|
   |Name|Geben Sie **myPrivateSQLendpoint** ein.|
   |Zielunterressource|Behalten Sie den standardmäßigen Standard-**SqlServer** bei.|
   |**Netzwerk**|
   |Virtuelles Netzwerk|Wählen Sie **myVNet1a** aus.|
   |Subnet|Wählen Sie **mySubnet1a** aus.|
   |**Private DNS-Integration**|
   |Integrieren in eine private DNS-Zone|Übernehmen Sie den Standardwert **Ja**.|
   |Private DNS-Zone|Behalten Sie die Standardeinstellung **(Neu) privatelink.database.windows.net** bei.|

 9. Klickan Sie auf **OK**.

 10. Klicken Sie auf **Überprüfen + erstellen**.

 11. Klicken Sie auf **Erstellen**.

### Deaktivieren des öffentlichen Zugriffs auf logische Azure SQL-Server

>**Hinweis**: Gehen Sie für dieses Szenario davon aus, dass Sie den gesamten öffentlichen Zugriff auf Ihren Azure SQL-Server deaktivieren und nur Verbindungen aus Ihrem virtuellen Netzwerk zulassen möchten.

1. Geben Sie im Suchfeld des Azure-Portals **mysqlserver** oder den Servernamen ein, den Sie in den vorherigen Schritten eingegeben haben.

2. Wählen Sie auf der Seite **Netzwerk** die Registerkarte **Öffentlicher Zugriff** aus, und wählen Sie dann **Deaktivieren** für **Öffentlicher Netzwerkzugriff** aus.

   ![image](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/44ff5c24-70cf-49ed-b2ab-5e210c478b3a)


4. Wählen Sie **Speichern**.

### Testen der Verbindung mit dem privaten Endpunkt

>**Hinweis**: In diesem Abschnitt verwenden Sie den virtuellen Computer, den Sie in den vorherigen Schritten erstellt haben, um über den privaten Endpunkt eine Verbindung mit dem SQL-Server herzustellen.

1. Wählen Sie **Ressourcengruppen** im linken Navigationsbereich aus.

2. Wählen Sie **CreateSQLEndpointTutorial** aus.

3. Wählen Sie **myVM** aus.

4. Wählen Sie auf der Seite „Übersicht“ für **myVM** die Option „Verbinden“ und dann **Bastion** aus.

5. Geben Sie den Benutzernamen **Tenantadmin2** und das Kennwort **Superuser#170** ein, die Sie beim Erstellen des virtuellen Computers festgelegt haben.

   **Wichtig:** Wechseln Sie zu den Edge-Einstellungen/Popups und Umleitungen, und schalten Sie die Option „Blockiert“ auf **Aus** um, bevor Sie „Verbinden“ auswählen.

7. Wählen Sie die Schaltfläche **Verbinden** aus.
  
8. Öffnen Sie Windows PowerShell auf dem Server, nachdem Sie eine Verbindung hergestellt haben.

9. Geben Sie `nslookup sqlserver-name.database.windows.net.` ein, und ersetzen Sie **sqlserver-name** durch den Namen des SQL-Servers, den Sie in den vorherigen Schritten erstellt haben. Sie erhalten eine Meldung ähnlich der folgenden:

   ````  
   Server:  UnKnown
   Address:  168.63.129.16
   
   Non-authoritative answer:
   Name:    mysqlserver1a.privatelink.database.windows.net
   Address:  10.1.0.5
   Aliases:  mysqlserver1a.database.windows.net
   ````
    
>**Hinweis**: Als Name für den SQL-Server wird die private IP-Adresse 10.1.0.5 zurückgegeben. Diese Adresse befindet sich in dem Subnetz **mySubnet1a** des virtuellen Netzwerks **myVNet1a**, das Sie zuvor erstellt haben.

9. Installieren Sie [SQL Server Management Studio](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?preserve-view=true&view=sql-server-2017) auf **myVM**.
 
10. Öffnen Sie **SQL Server Management Studio**.

11. Geben Sie unter **Mit Server verbinden** diese Informationen ein, oder wählen Sie sie aus:

    |Einstellung|Wert|
    |---|---|
    |Servertyp|Wählen Sie **Datenbank-Engine** aus.|
    |Servername|Geben Sie **sqlserver1a.database.windows.net** ein.|
    |Authentifizierung|Wählen Sie **SQL Server-Authentifizierung** aus.|
    |Benutzername|Geben Sie **Tenantadmin2** ein.|
    |Kennwort|Geben Sie **Superuser#170** ein.|
    |Kennwort speichern|Wählen Sie **Ja** aus.|
   
12. Wählen Sie **Verbinden** aus.

13. Durchsuchen Sie Datenbanken im linken Menü.

14. (Optional) Erstellen Sie die Informationen unter mysqldatabase, bzw. rufen Sie sie ab.

15. Schließen Sie die Remotedesktopverbindung mit myVM.
  
> **Ergebnisse**: Sie haben über das Azure-Portal eine Verbindung mit einem Azure SQL-Server über einen privaten Azure-Endpunkt hergestellt.
