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

## Übungsanweisungen 

### Erstellen Sie eine Azure-Ressourcengruppe und das virtuelle Netzwerk.

>**Hinweis**: Mit dem folgenden Verfahren wird ein virtuelles Netzwerk mit einem Ressourcensubnetz erstellt.

1. Starten Sie eine Browsersitzung, und melden Sie sich beim [Azure-Portal-Menü](https://portal.azure.com/) an.             
   
2. Geben Sie im Suchfeld oben im Portal **Virtuelle Netzwerke** ein. Wählen Sie in den Suchergebnissen **Virtuelle Netzwerke** aus.

3. Wählen Sie auf der Seite **Virtuelle Netzwerke** die Option **+ Erstellen** aus.

4. Geben Sie unter **Virtuelles Netzwerk erstellen** auf der Registerkarte **Grundlagen** die folgenden Informationen ein, oder wählen Sie sie aus:
   
   |Einstellung|Wert|
   |---|---|
   |**Projektdetails**|
   |Subscription|Wählen Sie Ihr Abonnement aus.|
   |Resource group|Geben Sie **az-rg-1** ein.|
   |**Instanzendetails**|
   |Name des virtuellen Netzwerks|Geben Sie **vnet-1** ein.|
   |Region|Wählen Sie **(USA) USA, Osten** aus.|  
    
5. Wählen Sie **Weiter** aus, um zur Registerkarte **Sicherheit** zu gelangen.
  
6. Wählen Sie **Weiter** aus, um zur Registerkarte **IP-Adressen** zu gelangen.

7. Wählen Sie im Feld für den Adressraum unter **Subnetze** das **Standardsubnetz** aus.

8. Geben Sie in der Vorlage **Subnetz bearbeiten** die folgenden Informationen ein, oder wählen Sie sie aus:

   |Einstellung|Wert|
   |---|---|
   |**Subnetzdetails**|
   |Subnetzzweck|Belassen Sie die Standardeinstellung auf „Standard“.|
   |Name|Geben Sie **subnet-1** ein.|
   |Startadresse|Belassen Sie die Standardeinstellung auf 10.0.0.0/16.|
   |Größe|Behalten Sie die Standardeinstellungen als „/24 (256 addresses)“ bei.|

    ![image](https://github.com/user-attachments/assets/82076f64-6a7f-4235-942d-d83e32ed6ea1)

10. Wählen Sie **Speichern**.

11. Wählen Sie am unteren Bildschirmrand **Überprüfen + erstellen** aus, und wenn die Validierung erfolgreich ist, wählen Sie **Erstellen** aus.

     ![image](https://github.com/user-attachments/assets/c53a04e4-d760-4e28-b998-1d48a56702f1)

### Mithilfe einer Anwendungssicherheitsgruppe können Sie Server mit ähnlichen Funktionen gruppieren, wie etwa Webserver.

Mithilfe einer Anwendungssicherheitsgruppe (ASG) können Sie Server mit ähnlichen Funktionen gruppieren (z. B. Webserver).

1. Geben Sie im Suchfeld oben im Portal **Anwendungssicherheitsgruppen** ein. Wählen Sie in den Suchergebnissen **Anwendungssicherheitsgruppen** aus.

2. Auf der Seite **Anwendungssicherheitsgruppen** wählen Sie **+ Erstellen.**

3. Geben Sie auf der Seite **Grundlagen** von **Erstellen einer Anwendungssicherheitsgruppe** die folgenden Informationen ein oder wählen sie aus:
   
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

2. Wählen Sie auf der Seite **Netzwerksicherheitsgruppen** die Option **+ Erstellen** aus.

3. Geben Sie auf der Registerkarte **Grundlagen** unter **Netzwerksicherheitsgruppe erstellen** die folgenden Informationen ein, oder wählen Sie sie aus:
   
   |Einstellung|Wert|
   |---|---|
   |**Projektdetails**|
   |Subscription|Wählen Sie Ihr Abonnement aus.|
   |Resource group|Wählen Sie **az-rg-1** aus.|
   |**Instanzendetails**|
   |Name|Geben Sie **nsg-1** ein.|
   |Region|Wählen Sie **USA, Osten** aus.|  
    
4. Klicken Sie auf **Überprüfen + erstellen**.

5. Klicken Sie auf **Erstellen**.

### Zuordnen einer Netzwerksicherheitsgruppe zu einem Subnetz

>**Hinweis**: In dieser Aufgabe ordnen Sie die Netzwerksicherheitsgruppe dem Subnetz des zuvor erstellten virtuellen Netzwerks zu.

1. Geben Sie im Suchfeld oben im Portal **Netzwerksicherheitsgruppen** ein. Wählen Sie in den Suchergebnissen **Netzwerksicherheitsgruppen** aus.
   
2. Wählen Sie **nsg-1** aus.

3. Wählen Sie **Subnetze** im Abschnitt **Einstellungen** von **nsg-1** aus.

4. Wählen Sie auf der Seite **nsg-1 | Subnetze** die Option „+ **Verknüpfen:**“ aus.

   ![image](https://github.com/user-attachments/assets/bfc18dd3-3345-4c05-9981-4f479d5f7c7e)

6. Wählen Sie unter **Subnetz zuordnen** die Option **vnet-1 (az-rg-1)** für **Virtuelles Netzwerk** aus.

7. Wählen Sie **subnet-1** als **Subnetz** aus, und klicken Sie dann auf **OK**.

### Erstellen Sie Sicherheitsregeln für die Netzwerksicherheitsgruppe mit dem Subnetz des zuvor erstellten virtuellen Netzwerks.

1. Wählen Sie im Abschnitt **Einstellungen** von **nsg-1** die Option **Eingangssicherheitsregeln** aus.
   
2. Auf der Seite **nsg-1 | Eingehende Sicherheitsregeln** wählen Sie + **Hinzufügen.**

3. Erstellen Sie eine Sicherheitsregel, die für die Anwendungssicherheitsgruppe **asg-web** die Ports 80 und 443 zulässt. Geben Sie auf der Seite **Eingangssicherheitsregel hinzufügen** die folgenden Informationen ein, oder wählen Sie sie aus:

   |Einstellung|Wert|
   |---|---|
   |`Source`|Übernehmen Sie den Standardwert **Beliebig**.|
   |Source port ranges|Belassen Sie die Standardeinstellung Portbereiche.|
   |Destination|Wählen Sie **Anwendungssicherheitsgruppe** aus.|
   |Ziel-Anwendungssicherheitsgruppen|Wählen Sie **asg-web** aus.|
   |Dienst|Belassen Sie die Standardeinstellung auf Benutzerdefiniert.|
   |Zielportbereiche|Geben Sie **80,443** ein.|
   |Protocol|Wählen Sie **TCP** aus.|
   |Aktion|Belassen Sie die Standardeinstellungen auf Zulassen.|
   |Priorität|Belassen Sie die Standardeinstellung bei 100.|
   |Name|Geben Sie **allowweball** ein.|

4. Wählen Sie **Hinzufügen**.

5. Vervollständigen Sie die vorherigen Schritte mit den folgenden Informationen:

   |Einstellung|Wert|
   |---|---|
   |`Source`|Übernehmen Sie den Standardwert **Beliebig**.|
   |Source port ranges|Belassen Sie die Standardeinstellung Portbereiche.|
   |Destination|Wählen Sie **Anwendungssicherheitsgruppe** aus.|
   |Ziel-Anwendungssicherheitsgruppe|Wählen Sie **asg-mgmt** aus.|
   |Dienst|Wählen Sie **RDP** aus.|
   |Zielportbereiche|Belassen Sie die Standardeinstellung auf 3389.|
   |Protokoll|Belassen Sie die Standardeinstellung auf TCP.|
   |Aktion|Belassen Sie die Standardeinstellung auf Zulassen.|
   |Priorität|Belassen Sie die Standardeinstellung auf 110.|
   |Name|Geben Sie **allowrdpall** ein.|
   
6. Wählen Sie **Hinzufügen**.

### Erstellen Sie zwei virtuelle Computer (VMs) im zuvor erstellten virtuellen Netzwerk.

1. Geben Sie im Suchfeld oben im Portal den Begriff **Virtuelle Computer** ein. Wählen Sie in den Suchergebnissen **Virtuelle Computer** aus.

2. Wählen Sie unter **VM** die Option **+ Erstellen** und dann **Azure-VM** aus.
   
3. In **Erstellen Sie eine virtuelle Maschine,** geben Sie diese Informationen auf der Seite **Grundlagen** ein oder wählen sie aus:

   |Einstellung|Wert|
   |---|---|
   |**Projektdetails**|
   |Abonnement|Wählen Sie Ihr Abonnementaus.|
   |Resource group|Wählen Sie **az-rg-1** aus.|
   |**Instanzendetails**|
   |Name des virtuellen Computers|Geben Sie **vm-1** ein.|
   |Region|Wählen Sie **(USA) USA, Osten** aus.|
   |Verfügbarkeitsoptionen|Wählen Sie im Dropdownmenü „Verfügbarkeitszone“ die Option **Keine Infrastrukturredundanz erforderlich** aus.|
   |Sicherheitstyp|Wählen Sie im Dropdownmenü „Sicherheitstyp“ die Option **Standard** aus.|
   |Abbildung|Wählen Sie aus dem Dropdown-Menü Bild **Windows Server 2022 Datacenter: Azure Edition - x64 Gen2.**|
   |VM-Architektur|Belassen Sie die Standardeinstellung auf x64.|
   |Mit Azure Spot-Rabatt ausführen|Lassen Sie die Standardeinstellung deaktiviert.|
   |Größe|Behalten Sie die Standardeinstellung bei: Standard_D2s_v3-2 vcpus, 8 GiB Arbeitsspeicher.|
   |**Administratorkonto**|
   |Benutzername|Geben Sie **Tenantadmin1** ein.|
   |Kennwort|Geben Sie **Superuser#150** ein.|
   |Kennwort bestätigen|Geben Sie erneut **Superuser#150** ein.|
   |**Regeln für eingehende Ports**|
   |Öffentliche Eingangsports|Wählen Sie **Keine**.|
 
4. Wählen Sie **Weiter: Datenträger** und dann **Weiter: Netzwerk** aus.

5. Überprüfen Sie auf der Seite **Netzwerke** die folgenden Informationen oder geben Sie diese ein:

   |Einstellung|Wert|
   |---|---|
   |**Netzwerkschnittstelle**|
   |Virtuelles Netzwerk|Wählen Sie **vnet-1** aus.|
   |Subnet|Belassen Sie die Standardeinstellung auf subnet-1 (10.0.0.0/24).|
   |Öffentliche IP-Adresse|Belassen Sie die Standardeinstellung als (new) vm-1-ip.|
   |NIC-Netzwerksicherheitsgruppe|Wählen Sie **Keine**.|
   
6. Um fortzufahren, wählen Sie unten auf der Seite die Schaltfläche **Überprüfen + erstellen** aus.

7. Klicken Sie auf **Erstellen**. Die Bereitstellung der VM kann einige Minuten dauern.
  
   - Erstellen Sie die zweite virtuelle Maschine.

   - Wiederholen Sie die vorherigen Schritte, um eine zweite VM namens **vm-2** zu erstellen.

   - Warten Sie, bis die Bereitstellung der VMs abgeschlossen ist, bevor Sie mit dem nächsten Abschnitt fortfahren.

### Zuordnen von Netzwerkschnittstellen zu einer Anwendungssicherheitsgruppe

>**Hinweis**: Als Sie die VMs erstellt haben, hat Azure eine Netzwerkschnittstelle für jede VM erstellt und an die VM angefügt. Fügen Sie die Netzwerkschnittstellen der einzelnen virtuellen Computer einer der Anwendungssicherheitsgruppen hinzu, die Sie zuvor erstellt haben:

1. Geben Sie im Suchfeld oben im Portal den Begriff **Virtuelle Computer** ein. Wählen Sie in den Suchergebnissen **Virtuelle Computer** aus.

2. Wählen Sie **vm-1** aus.
 
3. Wählen Sie **Netzwerke** aus dem Abschnitt von **vm-1.**

4. Wählen Sie **Anwendungssicherheitsgruppen** aus dem Abschnitt **Netzwerke** von **vm-1. Wählen Sie **+ Anwendungssicherheitsgruppen hinzufügen** aus.

5. Wählen Sie in der Vorlage **Anwendungssicherheitsgruppen hinzufügen** die Option **asg-mgmt** aus der Vorlage **Anwendungssicherheitsgruppen** aus und klicken Sie dann auf die Schaltfläche **Hinzufügen** unten auf der Vorlagenseite.

   ![image](https://github.com/user-attachments/assets/9bb38a91-8aa6-427b-9b6d-b01c5333ad4c)

7. Wiederholen Sie die vorherigen Schritte für **vm-2** und wählen Sie **asg-web** in der Vorlage **Anwendungssicherheitsgruppen**.

> **Ergebnisse**: Sie haben eine virtuelle Netzwerkinfrastruktur erstellt und Netzwerkdatenverkehr mit einer Netzwerksicherheitsgruppe mithilfe des Azure-Portals gefiltert.

> **Hinweis**: Bitte entfernen Sie die Ressourcen aus diesem Labor nicht, da sie für die folgenden Übungen benötigt werden: Übung 05: Aktivieren des Just-in-Time-Zugriffs auf VMs, Übung 06a: Konfigurieren der Key Vault Firewall und virtueller Netzwerke.
