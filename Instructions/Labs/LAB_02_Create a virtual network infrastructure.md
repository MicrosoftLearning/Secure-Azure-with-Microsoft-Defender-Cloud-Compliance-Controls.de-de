---
lab:
  title: 'Übung 02: Erstellen einer virtuellen Netzwerkinfrastruktur'
  module: Module 03 - Filter network traffic with a network security group using the Azure portal
---


>**Hinweis**: Für dieses Lab benötigen Sie ein [Azure-Abonnement](https://azure.microsoft.com/en-us/free/?azure-portal=true), in dem Sie über Administratorzugriff verfügen. 


Sie können eine Netzwerksicherheitsgruppe verwenden, um eingehenden und ausgehenden Netzwerkdatenverkehr von und zu Azure-Ressourcen in einem virtuellen Azure-Netzwerk zu filtern. Netzwerksicherheitsgruppen enthalten Sicherheitsregeln, die Netzwerkdatenverkehr nach IP-Adresse, Port und Protokoll filtern. Wenn eine Netzwerksicherheitsgruppe einem Subnetz zugeordnet ist, werden Sicherheitsregeln auf Ressourcen angewendet, die in diesem Subnetz bereitgestellt werden.

## Architekturdiagramm

![image](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/1bfec315-129b-48a9-9c35-1f21c837068f)

---

## Qualifikationsaufgaben

- Erstellen Sie eine Netzwerksicherheitsgruppe und Sicherheitsregeln.
  
- Erstellen Sie Anwendungssicherheitsgruppen.
  
- Erstellen Sie ein virtuelles Netzwerk, und weisen Sie eine Netzwerksicherheitsgruppe zu einem Subnetz zu.
  
- Stellen Sie virtuelle Computer bereit, und weisen Sie ihre Netzwerkschnittstellen zu den Anwendungssicherheitsgruppen zu.
  
- Testen Sie Datenverkehrsfilter.

## Übungsanweisungen 

### Erstellen Sie eine Azure-Ressourcengruppe und das virtuelle Netzwerk.

>**Hinweis**: Mit dem folgenden Verfahren wird ein virtuelles Netzwerk mit einem Ressourcensubnetz erstellt.

1. Starten Sie eine Browsersitzung, und melden Sie sich beim [Azure-Portal-Menü](https://portal.azure.com/) an.             
   
2. Geben Sie im Suchfeld oben im Portal **Virtuelle Netzwerke** ein. Wählen Sie in den Suchergebnissen **Virtuelle Netzwerke** aus.

3. Wählen Sie auf der Seite „Virtuelle Netzwerke“ die Option + **Erstellen** aus.

4. Geben Sie unter **Virtuelles Netzwerk erstellen** auf der Registerkarte **Grundlagen** die folgenden Informationen ein, oder wählen Sie sie aus:
   
   |Einstellung|Wert|
   |---|---|
   |**Projektdetails**|
   |Subscription|Wählen Sie Ihr Abonnement aus.|
   |Resource group|Wählen Sie **Neu erstellen** aus, geben Sie **az-rg-1** ein, und wählen Sie **OK** aus.|
   |**Instanzendetails**|
   |Name des virtuellen Netzwerks|Geben Sie **vnet-1** ein.|
   |Region|Wählen Sie **USA, Osten** aus.|  
    
5. Wählen Sie **Weiter** aus, um zur Registerkarte **Sicherheit** zu gelangen.
  
6. Wählen Sie **Weiter** aus, um zur Registerkarte **IP-Adressen** zu gelangen.

7. Wählen Sie im Feld für den Adressraum unter **Subnetze** das **Standardsubnetz** aus.

8. Wählen Sie im Feld für den Adressraum unter **Subnetze** das Standardsubnetz aus.

9. Geben Sie unter **Subnetz bearbeiten** die folgenden Informationen ein, oder wählen Sie sie aus:

   |Einstellung|Wert|
   |---|---|
   |**Subnetzdetails**|
   |Subnetzvorlage|Übernehmen Sie den Standardwert **Default**.|
   |Name|Geben Sie **Subnetz-1** ein.|
   |Startadresse|Übernehmen Sie den Standardwert **10.0.0.0**.|
   |Subnetzgröße|Übernehmen Sie den Standardwert **/24 (256 Adressen)**.

![image](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Defender-for-Cloud-regulatory-compliance-controls/assets/91347931/73c40ee1-1452-4b7d-8328-004c795a7b1e)


10. Wählen Sie **Speichern**.

11. Wählen Sie am unteren Bildschirmrand **Überprüfen + erstellen** aus, und wenn die Validierung erfolgreich ist, wählen Sie **Erstellen** aus.

### Mithilfe einer Anwendungssicherheitsgruppe können Sie Server mit ähnlichen Funktionen gruppieren, wie etwa Webserver.

Mithilfe einer Anwendungssicherheitsgruppe (ASG) können Sie Server mit ähnlichen Funktionen gruppieren (z. B. Webserver).

1. Geben Sie im Suchfeld oben im Portal **Anwendungssicherheitsgruppe** ein. Wählen Sie in den Suchergebnissen **Anwendungssicherheitsgruppen** aus.
   
2. Klicken Sie auf **Erstellen**.

3. Geben Sie auf der Registerkarte **Grundlagen** unter **Anwendungssicherheitsgruppe erstellen** die folgenden Informationen ein, oder wählen Sie sie aus:
   
   |Einstellung|Wert|
   |---|---|
   |**Projektdetails**|
   |Subscription|Wählen Sie Ihr Abonnement aus.|
   |Resource group|Wählen Sie **az-rg-1** aus.|
   |**Instanzendetails**|
   |Name|Geben Sie **asg-web** ein.|
   |Region|Wählen Sie **USA, Osten** aus.|  
    
4. Klicken Sie auf **Überprüfen + erstellen**.

5. Klicken Sie auf **Erstellen**.

6. Wiederholen Sie die vorherigen Schritte, und geben Sie die folgenden Werte an:
    
   |Einstellung|Wert|
   |---|---|
   |**Projektdetails**|
   |Subscription|Wählen Sie Ihr Abonnement aus.|
   |Resource group|Wählen Sie **az-rg-1** aus.|
   |**Instanzendetails**|
   |Name|Geben Sie **asg-mgmt** ein.|
   |Region|Wählen Sie **USA, Osten** aus.|

7. Klicken Sie auf **Überprüfen + erstellen**.

8. Klicken Sie auf **Erstellen**.

### Erstellen Sie eine Netzwerksicherheitsgruppe, um den Netzwerkdatenverkehr in Ihrem virtuellen Netzwerk zu schützen.

Eine Netzwerksicherheitsgruppe (NSG) schützt den Netzwerkdatenverkehr in Ihrem virtuellen Netzwerk.

1. Geben Sie im Suchfeld oben im Portal **Netzwerksicherheitsgruppen** ein. Wählen Sie in den Suchergebnissen **Netzwerksicherheitsgruppen** aus.

>**Hinweis**: In den Suchergebnissen für Netzwerksicherheitsgruppen wird möglicherweise „Netzwerksicherheitsgruppen (klassisch)“ angezeigt. Wählen Sie Netzwerksicherheitsgruppen aus.
   
2. Wählen Sie **+ Erstellen** aus.

3. Geben Sie auf der Registerkarte **Grundlagen** unter **Netzwerksicherheitsgruppe erstellen** die folgenden Informationen ein, oder wählen Sie sie aus:
   
   |Einstellung|Wert|
   |---|---|
   |**Projektdetails**|
   |Subscription|Wählen Sie Ihr Abonnement aus.|
   |Resource group|Wählen Sie **az-rg-1** aus.|
   |**Instanzendetails**|
   |Name|Geben Sie **nsg-1** ein|
   |Region|Wählen Sie **USA, Osten** aus.|  
    
4. Klicken Sie auf **Überprüfen** + erstellen.

5. Klicken Sie auf **Erstellen**.

### Zuordnen einer Netzwerksicherheitsgruppe zu einem Subnetz

>**Hinweis**: In dieser Aufgabe ordnen Sie die Netzwerksicherheitsgruppe dem Subnetz des zuvor erstellten virtuellen Netzwerks zu.

1. Geben Sie im Suchfeld oben im Portal **Netzwerksicherheitsgruppen** ein. Wählen Sie in den Suchergebnissen **Netzwerksicherheitsgruppen** aus.
   
2. Wählen Sie **nsg-1** aus.

3. Wählen Sie **Subnetze** im Abschnitt **Einstellungen** von **nsg-1** aus.

4. Klicken Sie auf der Seite **Subnetze** auf **+ Zuordnen**:

 ![image](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Defender-for-Cloud-regulatory-compliance-controls/assets/91347931/3b2004f6-963f-43df-9d05-3999d2e97d76)

5. Wählen Sie unter **Subnetz zuordnen** die Option **vnet-1 (az-rg-1)** für **Virtuelles Netzwerk** aus.

6. Wählen Sie **subnet-1** als **Subnetz** aus, und klicken Sie dann auf **OK**.

### Erstellen Sie Sicherheitsregeln für die Netzwerksicherheitsgruppe mit dem Subnetz des zuvor erstellten virtuellen Netzwerks.

1. Wählen Sie im Abschnitt **Einstellungen** von **nsg-1** die Option **Eingangssicherheitsregeln** aus.
   
2. Klicken Sie auf der Seite **Eingangssicherheitsregeln** auf **+ Hinzufügen**:

3. Erstellen Sie eine Sicherheitsregel, die für die Anwendungssicherheitsgruppe **asg-web** die Ports 80 und 443 zulässt. Geben Sie auf der Seite **Eingangssicherheitsregel hinzufügen** die folgenden Informationen ein, oder wählen Sie sie aus:

   |Einstellung|Wert|
   |---|---|
   |`Source`|Übernehmen Sie den Standardwert **Beliebig**.|
   |Quellportbereiche|Übernehmen Sie den Standardwert **(*)**.|
   |Destination|Wählen Sie **Anwendungssicherheitsgruppe** aus.|
   |Ziel-Anwendungssicherheitsgruppen|Wählen Sie **asg-web** aus|
   |Dienst|Übernehmen Sie den Standardwert **Benutzerdefiniert**|
   |Zielportbereiche|Geben Sie **80,443** ein|
   |Protocol|Wählen Sie **TCP** aus.|
   |Aktion|Übernehmen Sie den Standardwert **Zulassen**|
   |Priorität|Übernehmen Sie den Standardwert **100**|
   |Name|Geben Sie **allowweball** ein|

4. Wählen Sie **Hinzufügen**.

5. Vervollständigen Sie die vorherigen Schritte mit den folgenden Informationen:

   |Einstellung|Wert|
   |---|---|
   |`Source`|Übernehmen Sie den Standardwert **Beliebig**.|
   |Quellportbereiche|Übernehmen Sie den Standardwert **(*)**.|
   |Destination|Wählen Sie **Anwendungssicherheitsgruppe** aus.|
   |Ziel-Anwendungssicherheitsgruppe|Wählen Sie **asg-mgmt** aus|
   |Dienst|Wählen Sie **RDP** aus.|
   |Zielportbereiche|Übernehmen Sie den Standardwert **3389**|
   |Protokoll|Übernehmen Sie die Standardeinstellung **TCP**|
   |Aktion|Übernehmen Sie den Standardwert **Zulassen**|
   |Priorität|Übernehmen Sie den Standardwert **110**|
   |Name|Geben Sie  *allowrdpall* ein|
   
6. Wählen Sie **Hinzufügen** aus.

### Erstellen Sie zwei virtuelle Computer (VMs) im zuvor erstellten virtuellen Netzwerk.

1. Suchen Sie im Portal nach **Virtuelle Computer**, und klicken Sie darauf.

2. Wählen Sie unter **VM** die Option **+ Erstellen** und dann **Azure-VM** aus.
   
3. Geben Sie unter **Virtuellen Computer erstellen** auf der Registerkarte **Grundlagen** die folgenden Informationen ein, bzw. wählen Sie sie aus:

   |Einstellung|Wert|
   |---|---|
   |**Projektdetails**|
   |Abonnement|Wählen Sie Ihr Abonnement aus.|
   |Resource group|Wählen Sie **az-rg-1** aus.|
   |**Instanzendetails**|
   |Name des virtuellen Computers|Geben Sie **vm-1** ein|
   |Region|Wählen Sie **USA, Osten** aus.|
   |Verfügbarkeitsoptionen|Wählen Sie im Dropdownmenü „Verfügbarkeitszone“ die Option **Keine Infrastrukturredundanz erforderlich** aus.|
   |Sicherheitstyp|Wählen Sie im Dropdownmenü „Sicherheitstyp“ die Option **Standard** aus.|
   |Abbildung|Wählen Sie im Dropdownmenü „Bild“ die Option **Windows Server 2022 Datacenter: Azure Edition – x64 Gen2** aus.|
   |VM-Architektur|Übernehmen Sie den Standardwert **x64**|
   |Mit Azure Spot-Rabatt ausführen|Übernehmen Sie die Standardeinstellung (deaktiviert)|
   |Größe|Übernehmen Sie die Standardeinstellung **Standard_D2s_v3 – 2 vCPUs, 8 GiB Arbeitsspeicher**|
   |**Administratorkonto**|
   |Authentifizierungsart|Wählen Sie **Kennwort** aus.|
   |Username|Geben Sie **Tenantadmin1** ein|
   |Kennwort|Geben Sie **Superuser#150** ein|
   |Kennwort bestätigen|Geben Sie erneut **Superuser#150** ein|
   |**Regeln für eingehende Ports**|
   |Öffentliche Eingangsports|Wählen Sie **Keine** aus.|
 
4. Wählen Sie **Weiter: Datenträger** und dann **Weiter: Netzwerk aus.

5. Geben Sie auf der Registerkarte **Netzwerk** die folgenden Informationen ein, bzw. wählen Sie sie aus:

   |Einstellung|Wert|
   |---|---|
   |**Netzwerkschnittstelle**|
   |Virtuelles Netzwerk|Wählen Sie **vnet-1** aus|
   |Subnet|Wählen Sie **Standard (10.0.0.0/24)** aus|
   |Öffentliche IP-Adresse|Übernehmen Sie den Standardwert einer neuen öffentlichen IP-Adresse|
   |NIC-Netzwerksicherheitsgruppe|Wählen Sie **Keine** aus.|
   
6. Wählen Sie die Registerkarte **Überprüfen + erstellen** oder unten auf der Seite die blaue Schaltfläche **Überprüfen + erstellen** aus.

7. Klicken Sie auf **Erstellen**. Die Bereitstellung der VM kann einige Minuten dauern.
  
   - Erstellen des zweiten virtuellen Computers

   - Wiederholen Sie die vorherigen Schritte, um eine zweite VM namens **vm-2** zu erstellen.

   - Warten Sie, bis die Bereitstellung der VMs abgeschlossen ist, bevor Sie mit dem nächsten Abschnitt fortfahren.

### Zuordnen von Netzwerkschnittstellen zu einer Anwendungssicherheitsgruppe

>**Hinweis**: Als Sie die VMs erstellt haben, hat Azure eine Netzwerkschnittstelle für jede VM erstellt und an die VM angefügt. Fügen Sie die Netzwerkschnittstellen der einzelnen virtuellen Computer einer der Anwendungssicherheitsgruppen hinzu, die Sie zuvor erstellt haben:

1. Geben Sie im Suchfeld oben im Portal den Suchbegriff **Virtueller Computer** ein. Wählen Sie in den Suchergebnissen **Virtuelle Computer** aus.

2. Wählen Sie **vm-1** aus
 
3. Wählen Sie im Abschnitt **vm-1** die Option **Netzwerk** aus.

4. Wählen Sie die Registerkarte **Anwendungssicherheitsgruppen** und dann **Anwendungssicherheitsgruppen konfigurieren** aus.

5. Wählen Sie in der Vorlage **Anwendungssicherheitsgruppen konfigurieren** aus dem Dropdownmenü **Anwendungssicherheitsgruppen** die Option **asg-mgmt** aus, und klicken Sie dann oben auf der Vorlagenseite auf das Symbol **Speichern**.

![image](https://github.com/MicrosoftLearning/Secure-Azure-with-Microsoft-Defender-Cloud-Compliance-Controls/assets/91347931/dd17aeba-8e16-431b-b921-527367fea484)

6. Wiederholen Sie vorherige Schritte für **vm-2**, und wählen Sie dabei im Pulldownmenü **Anwendungssicherheitsgruppen** die Option **asg-web** aus.

> **Ergebnisse**: Sie haben eine virtuelle Netzwerkinfrastruktur erstellt und Netzwerkdatenverkehr mit einer Netzwerksicherheitsgruppe mithilfe des Azure-Portals gefiltert.

> **Hinweis**: Entfernen Sie die Ressourcen nicht aus diesem Lab, da sie für die folgenden Übungen erforderlich sind: „Übung 03b – Aktivieren des Just-in-Time-Zugriffs auf VMs“, „Übung 05a – Konfigurieren von Key Vault-Firewalls und virtuellen Netzwerken“ und „Übung 05b – Konfigurieren der Azure Key Vault-Wiederherstellungsverwaltung mit Schutz durch vorläufiges Löschen und Bereinigungsschutz“.
