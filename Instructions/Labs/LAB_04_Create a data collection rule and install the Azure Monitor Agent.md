---
lab:
  title: Übung 04 - Erstellen einer Datensammlungsregel und Installieren des Azure Monitor Agent
  module: Module 05 - Create a data collection rule and install the Azure Monitor Agent
---


>**Hinweis**: Für dieses Lab benötigen Sie ein [Azure-Abonnement](https://azure.microsoft.com/en-us/free/?azure-portal=true), in dem Sie über Administratorzugriff verfügen. 


Datensammlungsregeln (DCRs) legen die zu erfassenden Daten fest, während der Azure Monitor-Agent diese Regeln anwendet, um Protokolle und Metriken von virtuellen Maschinen in Azure, anderen Clouds oder lokal zu erfassen. Zusammen ermöglichen sie eine konsistente und zentralisierte Überwachung über verschiedene Umgebungen hinweg.

---

## Qualifikationsaufgabe

- Erstellen und Definieren einer Datensammlungsregel.

- Wählen Sie Zielressourcen für die Datensammlung aus.
  
- Konfigurieren Sie Datenquellen und -ziele.

- Wählen Sie Datenquellentypen und zu erfassende Daten aus.

- Wählen Sie ein Ziel für die Datenübermittlung aus.

## Übungsanweisungen 

### Erstellen und Definieren einer Datensammlungsregel.

>**Hinweis**: Erstellen Sie Ihre Datensammlungsregel in der gleichen Region wie Ihr Zielarbeitsbereich für Protokollanalyse oder Azure Monitor. Sie können die Datensammlungsregel Computern oder Containern aus einer beliebigen Abonnement- oder Ressourcengruppe im Mandanten zuordnen. 
   
1. Geben Sie im Suchfeld oben im Portal Datensammlungsregeln ein. Wählen Sie in den Suchergebnissen Datensammlungsregeln aus.

2. Wählen Sie **+ Erstellen** aus.

![image](https://github.com/user-attachments/assets/e428c441-9d8d-4460-acd9-a97e2aa2b5af)

3. Geben Sie auf der Registerkarte **Grundlagen** des Blades **Datensammlungsregel erstellen** die folgenden Einstellungen an (lassen Sie die anderen mit ihren Standardwerten):

    |Einstellung|Wert|
    |---|---|
    |**Regeldetails**|
    |Regelname|**dcr-1**|
    |Abonnement|den Namen des Iginte-Abonnements, das Sie in diesem Lab verwenden|
    |Resource group|**az-rg-1**|
    |Region|**USA, Osten**|
    |Plattformtyp|**Windows**|
    |Datensammlungsendpunkt|*Lassen Sie den Standardwert auf Keine*|

![image](https://github.com/user-attachments/assets/eee884f6-b20f-4d51-9310-6e755746ed9a)   

4. Klicken Sie auf die Schaltfläche mit dem Text **Weiter: Ressourcen >** , um fortzufahren.

5. Auf der Registerkarte Ressourcen wählen Sie **+ Ressourcen hinzufügen**.
  
>**Hinweis**: Der Azure Monitor-Agent wird automatisch auf den virtuellen Computern (Ressourcen) installiert, die zum Sammeln von Daten ausgewählt sind.
   
![image](https://github.com/user-attachments/assets/619106b4-7f5e-44dd-98c7-129689ab89c0)

6. Aktivieren Sie in der Vorlage Bereich auswählen das Kontrollkästchen **Abonnement einrichten** in der Bereichsauswahl und klicken Sie auf **Anwenden.**

![image](https://github.com/user-attachments/assets/c95b76cd-1515-47a5-b07b-02dcb28c0bf3)


8. Klicken Sie auf **Überprüfen + erstellen**.








> **Ergebnisse**: Sie haben eine Datensammlungsregel erstellt und den Azure Monitor-Agent installiert.
