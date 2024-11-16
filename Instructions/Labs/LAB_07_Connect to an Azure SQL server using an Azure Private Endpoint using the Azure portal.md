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
   |Subscription|Wählen Sie Ihr Abonnement aus.|
   |Resource group|Wählen Sie **az-rg-1** aus.|
   |**Instanzendetails**|
   |Name des virtuellen Netzwerks|Geben Sie **vnet-2** ein.|
   |Region|Wählen Sie **(USA) USA, Osten** aus.|  
    
5. Wählen Sie **Weiter** aus, um zur Registerkarte **Sicherheit** zu gelangen.
  
6. Wählen Sie **Azure Bastion aktivieren** im Abschnitt "Azure Bastion" auf der Registerkarte "Sicherheit" aus.

>**Hinweis**: Azure Bastion ist ein kostenpflichtiger Dienst, der eine sichere RDP/SSH-Verbindung zu Ihren virtuellen Maschinen über TLS bereitstellt. Beim Herstellen einer Verbindung über Azure Bastion benötigen Ihre virtuellen Computer keine öffentliche IP-Adresse. 

7. Geben Sie die folgenden Informationen in das Feld **Azure Bastion** ein oder wählen Sie sie aus:

   |Einstellung|Wert|
   |---|---|
   |Azure Bastion-Host |Geben Sie **az-bastionhost-1a** ein.|
   |Öffentlicher Azure Bastion-IP-Adressenname|Wählen Sie **Öffentliche IP-Adresse erstellen** aus.|
   |Öffentliche IP-Adresse hinzufügen|Wählen Sie **OK** aus.|

8. Wählen Sie **Weiter** aus, um zur Registerkarte **IP-Adressen** zu gelangen.

9. Klicken Sie im vorhandenen konfigurierten **IPv4-Adressraum** in der Spalte **Subnetze** auf den Eintrag **Standard**.

10. Geben Sie in der Vorlage **Subnetz bearbeiten** die folgenden Informationen ein, oder wählen Sie sie aus:

    |Einstellung|Wert|
    |---|---|
    |Subnetzzweck|Belassen Sie die Standardeinstellung auf „Standard“.|
    |Name|**subnet-2**|
    |Einschließen eines IPv4-Adressraums|Behalten Sie die Standardeinstellung mit dem Häkchen bei.|
    |IPv4-Adressbereich|Belassen Sie die Standardeinstellung auf 10.0.0.0/16.|
    |Startadresse|10.0.0.0.|
    |Größe|Belassen Sie die Standardeinstellung auf /24 (256 Adressen).|
    |Subnetzadressbereich|10.0.0.0-10.0.0.255|

11. Wählen Sie unten auf der Seite **Subnetz bearbeiten** die Option **Speichern** aus.

12. Wählen Sie unten auf der Seite **IP-Adressen** die Option **Überprüfen + erstellen** aus.

13. Wählen Sie unten auf der Seite **Überprüfen + erstellen** die Option **Erstellen** aus.

>**Hinweis:** Es kann bis zu 15 Minuten dauern, bis die Instanziierung der Bastion-Bereitstellung vollständig abgeschlossen ist.
 
### Erstellen Sie eine VM.

>**Hinweis**: In dieser Aufgabe erstellen Sie einen virtuellen Computer zum Testen des privaten Endpunkts.

1. Suchen Sie im Portal nach **Virtuelle Computer** und klicken Sie darauf.

2. Wählen Sie unter **VM** die Option **+ Erstellen** und dann **Azure-VM** aus.

3. Geben Sie diese Informationen auf der Seite **Grundlagen** ein oder wählen Sie sie aus, wenn Sie eine virtuelle Maschine erstellen:

   |Einstellung|Wert|
   |---|---|
   |Abonnement|Wählen Sie Ihr Abonnementaus.|
   |Resource group|Wählen Sie **az-rg-1** aus.|
   |**Instanzendetails**|
   |Name des virtuellen Computers|Geben Sie **vm-3** ein.|
   |Region|Wählen Sie **(USA) USA, Osten** aus.|
   |Verfügbarkeitsoptionen|Wählen Sie im Dropdownmenü „Verfügbarkeitszone“ die Option **Keine Infrastrukturredundanz erforderlich** aus.|
   |Sicherheitstyp|Wählen Sie im Dropdownmenü „Sicherheitstyp“ die Option **Standard** aus.|
   |Abbildung|Wählen Sie **Windows Server 2022 Datacenter – x64 Gen2** aus.|
   |VM-Architektur|Wählen Sie **x64** aus.|
   |Mit Azure Spot-Rabatt ausführen|Lassen Sie die Standardeinstellung deaktiviert.|
   |Größe|Behalten Sie die Standardeinstellung bei: Standard_D2s_v3-2 vcpus, 8 GiB Arbeitsspeicher.|
   |**Administratorkonto**|
   |Benutzername|Geben Sie **Tenantadmin2** ein.|
   |Kennwort|Geben Sie **Superuser#170** ein.|
   |Kennwort bestätigen|Geben Sie erneut **Superuser#170** ein.|
   |**Regeln für eingehende Ports**|
   |Öffentliche Eingangsports|Wählen Sie **Keine**.|
   |Eingangsports auswählen|Die Standardeinstellung ist abgeblendet.|

4. Wählen Sie **Weiter: Datenträger** und dann **Weiter: Netzwerk** aus.
  
5. Geben Sie auf der Seite **Netzwerk** folgende Informationen ein oder wählen Sie sie aus:

   |Einstellung|Wert|
   |---|---|
   |**Netzwerkschnittstelle**|
   |Virtuelles Netzwerk|Wählen Sie **vnet-2** aus.|
   |Subnet|Belassen Sie die Standardeinstellung auf subnet-2 (10.0.0.0/24).|
   |Öffentliche IP-Adresse|Belassen Sie die Standardeinstellung als (new) vm-3-ip.|
   |NIC-Netzwerksicherheitsgruppe|Behalten Sie die Standardeinstellung „Keine“ bei.|
   |Löschen Sie die NIC beim Löschen des virtuellen Computers|Lassen Sie die Standardeinstellung „Beschleunigten Netzwerkbetrieb aktivieren“ aktiviert.|
   |Lastenausgleich|Behalten Sie die Standardeinstellung „Keine“ bei.|
  
6. Klicken Sie auf **Überprüfen + erstellen**.

7. Überprüfen Sie die Einstellungen, und wählen Sie dann die Option **Erstellen**.

### Erstellen eines Azure SQL-Servers und eines privaten Endpunkts

>**Hinweis**: In diesem Abschnitt erstellen Sie einen SQL-Server in Azure.

1. Geben Sie in das Suchfeld oben auf der Portalseite **SQL-Datenbank** ein. Wählen Sie in den Suchergebnissen **SQL-Datenbanken** aus.

2. Klicken Sie auf der Seite **SQL-Datenbanken** auf **+ Erstellen**.
   
3. Geben Sie unter **SQL-Datenbank erstellen** auf der Registerkarte **Grundlagen** die folgenden Informationen ein, bzw. wählen Sie sie aus:

   |Einstellung|Wert|
   |---|---|
   |Subscription|Wählen Sie Ihr Abonnement aus.|
   |Resource group|Wählen Sie **az-rg-1** aus.|
   |**Datenbankdetails**|
   |Datenbankname|Geben Sie **az-sql-db1a** ein.|
   |Server|Wählen Sie **Neu erstellen**.|
   |**Serverdetails**|
   |Servername|Geben Sie **az-sql-svr1a** ein.|
   |Location|Behalten Sie die Standardeinstellung „USA, Osten“ bei.|
   |**Authentifizierung**|
   |Authentifizierungsmethode|Wählen Sie **SQL-Authentifizierung verwenden** aus.|  
   |Serveradministratoranmeldung|Geben Sie **Tenantadmin2** ein.|
   |Kennwort|Geben Sie **Superuser#170** ein.|
   |Kennwort bestätigen|Geben Sie **Superuser#170** ein.|

4. Klickan Sie auf **OK**.
    
   |Einstellung|Wert|
   |---|---|
   |**Datenbankdetails**|
   |Möchten Sie einen Pool für elastische SQL-Datenbanken verwenden?|Behalten Sie die Standardeinstellung bei, also „Nein“.|
   |Workloadumgebung|Behalten Sie die Standardeinstellung „Entwicklung“ bei.|
   |Compute + Speicher|Behalten Sie die Standardeinstellung „Universell – Serverlos“ bei.|
   |**Redundanz für Sicherungsspeicher**|
   |Redundanz für Sicherungsspeicher|Wählen Sie **Lokal redundanter Sicherungsspeicher** aus.|
   
5. Wählen Sie die Registerkarte **Netzwerk** oder die Schaltfläche **Weiter: Netzwerk**.

6. Geben Sie auf der Registerkarte **Netzwerk** die folgenden Informationen ein, bzw. wählen Sie sie aus:

   |Einstellung|Wert|
   |---|---|
   |**Netzwerkkonnektivität**|
   |Konnektivitätsmethode|Wählen Sie **Privater Endpunkt** aus.|
   |Verbindungsrichtlinie|Behalten Sie die Standardeinstellung bei, d. h. „Standard – Verwendet die Umleitungsrichtlinie für alle Clientverbindungen, die innerhalb von Azure (außer Verbindungen mit privaten Endpunkten) und den Proxy für alle Clientverbindungen, die außerhalb von Azure hergestellt werden.|
   |Verschlüsselungsverbindungen|Belassen Sie die Standardeinstellung TLS.12|

7. Wählen Sie im Abschnitt **Private Endpunkte** die Option **Privaten Endpunkt hinzufügen** aus.

8. Klicken Sie auf **Überprüfen + erstellen**.

9. Klicken Sie auf **Erstellen**.

10. Geben Sie unter **Privaten Endpunkt erstellen** diese Informationen ein, oder wählen Sie sie aus:

       |Einstellung|Wert|
       |---|---|
       |Subscription|Wählen Sie Ihr Abonnement aus.|
       |Resource group|Wählen Sie **az-rg-1** aus.|
       |Location|Wählen Sie **USA, Osten** aus.|
       |Name|Geben Sie **az-pe1a** ein.|
       |Zielunterressource|Belassen Sie die Standardeinstellung bei SqlServer.|
       |**Netzwerk**|
       |Virtuelles Netzwerk|Wählen Sie **vnet-2** aus.|
       |Subnet|Wählen Sie **subnet-2** aus.|
       |**Private DNS-Integration**|
       |Integrieren in eine private DNS-Zone|Lassen Sie die Standardeinstellung auf „Ja“.|
       |Private DNS-Zone|Behalten Sie die Standardeinstellung (Neu) privatelink.database.windows.net bei|

12. Wählen Sie **OK** aus.

13. Klicken Sie auf **Überprüfen + erstellen**.

14. Klicken Sie auf **Erstellen**.

>**Hinweis**: Die Bereitstellung von Azure SQL Server und privaten Endpunkten kann bis zu 10 Minuten dauern, bis die vollständige Instanziierung abgeschlossen ist.

### Erlauben Sie bestimmten öffentlichen Internet-IP-Adressen den Zugriff auf Ihren logischen Azure SQL-Server.

>**Hinweis**: Gehen Sie für diese Aufgabe davon aus, dass Sie den gesamten öffentlichen Zugriff auf Ihren Azure SQL-Server deaktivieren und nur Verbindungen aus Ihrem virtuellen Netzwerk zulassen möchten. Die Einstellung „Öffentlicher Zugriff“ ist möglicherweise standardmäßig auf **Deaktiviert** gesetzt.

1. Geben Sie im Suchfeld des Azure-Portals **az-sql-svr1a** oder den Servernamen ein, den Sie in den vorherigen Schritten eingegeben haben.
   
2. Wählen Sie **Netzwerk** aus dem Abschnitt **Sicherheit** von **az-sql-svr1a** aus.
  
3. Wechseln Sie auf der Seite **Netzwerk** zur Registerkarte **Öffentlicher Zugriff**.
  
4. Prüfen Sie, ob **Öffentlicher Netzwerkzugriff** deaktiviert ist. Falls dies deaktiviert ist, wählen Sie unter „Öffentlicher Netzwerkzugriff“ die Option **Ausgewählte Netzwerke** aus.

>**Hinweis**: Von den IP-Adressen, die wie im nachstehenden Abschnitt mit Firewallregeln konfiguriert sind, ausgehende Verbindungen erhalten Zugriff auf diese Datenbank. Standardmäßig sind öffentliche IP-Adressen unzulässig.

5. Wechseln Sie ggf. zum Abschnitt **Firewallregeln** auf der Seite **Netzwerk** und wählen Sie **+ Client-IPv4-Adresse hinzufügen** aus, wenn Ihre Client-IP-Adresse nicht bereits in den Feldern **Regelname**, **Start-IPv4-Adresse** und **End-IPv4-Adresse** eingefügt ist.

   ![image](https://github.com/user-attachments/assets/fff5bfb1-53fd-40ea-9a31-5a095e7f3dbc) 

7. Wählen Sie **Speichern**.

### Testen der Verbindung mit dem privaten Endpunkt

>**Hinweis**: In diesem Abschnitt verwenden Sie den virtuellen Computer, den Sie in den vorherigen Schritten erstellt haben, um über den privaten Endpunkt eine Verbindung mit dem SQL-Server herzustellen.

1. Geben Sie im Suchfeld des Azure-Portals **vm-3** ein und treffen Sie in der Dropdownliste „Ressourcen“ Ihre Auswahl.

2. Wählen Sie auf der Seite **Übersicht** von vm-1 die Option **Verbinden** und dann **Bastion** aus.

3. Geben Sie den Benutzernamen **Tenantadmin2** und das Kennwort **Superuser#170** ein, die Sie beim Erstellen des virtuellen Computers festgelegt haben.

   **Wichtig:** Wechseln Sie zu Edge-Einstellungen, und navigieren Sie zu **Popups und Umleitungen.** Wählen Sie die radiale Option mit der Bezeichnung**Popups immer zulassen und umleiten von https://portal.azure.com aus,** und klicken Sie dann auf **Fertig.**

4. Wählen Sie die Schaltfläche **Verbinden** aus.
  
5. Öffnen Sie Windows PowerShell auf dem Server, nachdem Sie eine Verbindung hergestellt haben.

6. Um die Namensauflösung des privaten Endpunkts zu überprüfen, geben Sie den folgenden Befehl im Terminalfenster ein:

   ```bash
   nslookup server-name.database.windows.net

>**Note**: Replace **sqlserver-name** with the name of the SQL server you created in the previous steps. For example, enter **nslookup az-sql-srv1a.database.windows.net** You’ll receive a message similar to the one shown below:

   ````
   
   Server: Unbekannte Adresse:  168.63.129.16
   
   Nicht autoritative Antwort: Name:    az-sql-srv1a.privatelink.database.windows.net Address:  10.1.0.5 Aliases:  az-sql-srv1a.database.windows.net
   ````
   
>**Note**: A  private IP address of 10.1.0.5 is returned for the SQL server name. This address is in **az-sql-srv1a** subnet of **vnet-2** virtual network you created previously.

7. Install [SQL Server Management Studio (SSMS)](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?preserve-view=true&amp;view=sql-server-2017) on **vm-3.**
 
8. Open **SQL Server Management Studio.**

9. In **Connect to server,** enter or select this information:

    |Setting|Value|
    |---|---|
    |Server type|Leave the default setting as Database Engine.|
    |Server name|Enter **az-sql-srv1a.database.windows.net.**|
    |Authentication|Select **SQL Server Authentication.**|
    |User name|Enter **Tenantadmin2**.|
    |Password|Enter **Superuser#170**.|
    |Remember password|Select **Yes.**|
    |Connectivity Security|
    |Encryption|Leave the default setting as Mandatory.|
   
10. Select **Connect.**

11. Browse databases from left menu.

12. Close the remote desktop connection to vm-3.
  
> **Results**: You have connected to an Azure SQL server using an Azure Private Endpoint using the Azure portal.
