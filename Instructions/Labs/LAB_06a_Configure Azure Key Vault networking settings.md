---
lab:
  title: 'Übung 06a: Konfigurieren von Azure Key Vault-Netzwerkeinstellungen'
  module: Module 07 - Configure Azure Key Vault networking settings
---


>**Hinweis**: Für dieses Lab benötigen Sie ein [Azure-Abonnement](https://azure.microsoft.com/en-us/free/?azure-portal=true), in dem Sie über Administratorzugriff verfügen. 


Sie können das Azure-Portal verwenden, um die Azure Key Vault-Netztechnologieeinstellungen für die Verwendung mit anderen Anwendungen und Azure-Diensten zu konfigurieren. 

---

## Qualifikationsaufgaben

- Erstellen eines Schlüsseltresors über das Azure-Portal.

- Fügen Sie einer Firewall und virtuellen Netzwerkregeln ein vorhandenes virtuelles Netzwerk hinzu.

- Konfigurieren Sie ein virtuelles Netzwerk und ein Subnetz, um den Zugriff auf einen Schlüsseltresor zu ermöglichen.

## Übungsanweisungen 

### Verwenden Sie das Azure-Portal, um einen Azure Key Vault zu erstellen.

1. Starten Sie eine Browsersitzung, und melden Sie sich beim [Azure-Portal-Menü](https://portal.azure.com/) an.
  
2. Geben Sie am oben im Portal **Schlüsseltresore** in das Suchfeld ein. Wählen Sie **Schlüsseltresore** in den Suchergebnissen aus.

3. Wählen Sie in der Liste „Ergebnisse“ die Option **Schlüsseltresore** aus.

4. Klicken Sie im Abschnitt „Schlüsseltresore“ auf **Erstellen**.

5. Geben Sie auf der Registerkarte **Grundlagen** unter **Schlüsseltresor erstellen** diese Informationen ein, oder wählen Sie diese aus:
   
   |Einstellung|Wert|
   |---|---|
   |**Projektdetails**|
   |Subscription|Wählen Sie Ihr Abonnement aus.|
   |Resource group|Geben Sie **az-rg-1** ein.|
   |**Instanzendetails**|
   |Name des Schlüsseltresors|Der Name des Tresors darf nur alphanumerische Zeichen und Bindestriche enthalten und nicht mit einer Zahl beginnen. *Beispiel: az-securevault150*|
   |Region|Wählen Sie **USA, Osten** aus.|
   |Tarif|Belassen Sie die Standardeinstellung auf Standard.|
   |Aufbewahrungsdauer für gelöschte Tresore in Tagen|Belassen Sie die Standardeinstellung bei 90.|

6. Wählen Sie die Registerkarte **Überprüfen + erstellen** aus, oder wählen Sie unten auf der Seite die blaue Schaltfläche „Überprüfen + Erstellen“ aus.
  
7. Klicken Sie auf **Erstellen**.

### Konfigurieren von Einstellung für Key Vault-Firewalls und virtuelle Netzwerke.

1. Geben Sie im Suchfeld im Azure-Portal **Schlüsseltresore** ein.

2. Navigieren Sie zum zuvor erstellten Schlüsseltresor.

3. Wählen Sie **Einstellungen,** dann **Netzwerke,** und dann die Registerkarte **Firewalls und virtuelle Netzwerke**.
   
4. Wählen Sie unter „Zugriff zulassen von“ die Option **Öffentlichen Zugriff von bestimmten virtuellen Netzwerken und IP-Adressen zulassen** aus.

5. Wählen Sie im Abschnitt „Virtuelle Netzwerke“ die Option + **Virtuelles Netzwerk hinzufügen** und dann + **Vorhandene virtuelle Netzwerke hinzufügen** aus.

6. Wählen Sie in der Vorlage **Netzwerke hinzufügen** Ihr zuvor erstelltes virtuelles Netzwerk aus der Dropdownliste **Virtuelle Netzwerke** und der Dropdownliste **Subnetze** aus.

7. Wählen Sie unten in der Vorlage **Netzwerke hinzufügen** die Option **Aktivieren** und dann **Hinzufügen**. 

8. Wählen Sie unten auf der Seite **Firewalls und virtuelle Netzwerke** die Option **Anwenden.**

  > **Ergebnisse**: Sie haben im Azure-Portal einen Schlüsseltresor erstellt und Einstellungen für eine Key Vault-Firewall und virtuelle Netzwerke konfiguriert.
