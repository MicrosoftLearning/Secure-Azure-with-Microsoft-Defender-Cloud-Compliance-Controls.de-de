---
lab:
  title: 'Übung 04 – Erstellen Sie eine Datenerfassungsregel, und installieren Sie den Azure Monitor-Agent'
  module: Module 05 - Collect guest operating system monitoring data from Azure and hybrid virtual machines using Azure Monitor Agent
---


>**Hinweis**: Für dieses Lab benötigen Sie ein [Azure-Abonnement](https://azure.microsoft.com/en-us/free/?azure-portal=true), in dem Sie über Administratorzugriff verfügen. 


Die Datensammlungsregeln (DCRs) legen fest, welche Daten erfasst werden sollen, während der Azure Monitor-Agent diese Regeln anwendet, um Protokolle und Metriken von virtuellen Computern in Azure, anderen Clouds oder vor Ort zu sammeln. Zusammen ermöglichen sie eine konsistente und zentralisierte Überwachung in verschiedenen Umgebungen.

---

## Qualifikationsaufgabe

- Erstellen und definieren Sie eine Datensammlungsregel.

- Wählen Sie Zielressourcen für die Datensammlung aus.

- Sie installieren den Azure Monitor-Agent.
  
- Konfigurieren Sie Datenquellen und -ziele.

- Wählen Sie Datenquellentypen und -daten für die Sammlung aus.

- Wählen Sie ein Ziel für die Datenübermittlung aus.

## Übungsanweisungen 

### Erstellen und definieren Sie eine Datensammlungsregel und installieren Sie den Azure Monitor-Agent.

>**Hinweis**: Erstellen Sie die Datensammlungsregel in derselben Region wie Ihren Log Analytics- oder Azure Monitor-Arbeitsbereich. Sie können es mit Maschinen oder Containern aus jeder Abonnement- oder Ressourcengruppe innerhalb des Mandanten verknüpfen. Der Azure Monitor-Agent wird automatisch auf virtuellen Azure-Ressourcen installiert.

1. Starten Sie eine Browsersitzung, und melden Sie sich beim [Azure-Portal-Menü](https://portal.azure.com/) an.
  
3. Geben Sie in das Suchfeld oben auf dem Portal **Datensammlungsregel** ein. Wählen Sie **Datensammlungsregeln** in den Suchergebnissen  aus.
  
4. Wählen Sie auf der Seite mit den **Datensammlungsregeln** die Option **Erstellen** aus.
  
    ![image](https://github.com/user-attachments/assets/a472bc6f-fa96-4615-a67c-c99e8b9ce7a4)

5. Geben Sie auf der Seite **Grundlagen** der **Regel zur Datensammlung erstellen** die folgenden Einstellungen an (lassen Sie die anderen auf ihren Standardwerten):

    |Einstellung|Wert|
    |---|---|
    |**Regeldetails**|
    |Regelname|**dcr-1**|
    |Abonnement|Wählen Sie Ihr Abonnement aus.|
    |Ressourcengruppe|**az-rg-1**|
    |Region|**USA, Osten**|
    |Plattformtyp|**Windows**|
    |Datensammlungsendpunkt|Belassen Sie die Standardeinstellung auf „Keine“|

   ![image](https://github.com/user-attachments/assets/6c63c48f-f7a9-4fb2-8fc0-e22084cd5013)

6. Klicken Sie auf die Schaltfläche am Ende der Seite **Grundlagen** mit der Bezeichnung **Weiter: Ressourcen > fortfahren.**
   
7. Wählen Sie auf der Seite **Ressourcen** die Option **+ Ressourcen hinzufügen** aus.

   ![image](https://github.com/user-attachments/assets/7e45996b-478b-4be4-9df3-df6127da6cb4)

8. Aktivieren Sie in der Vorlage **Bereich auswählen** das Kontrollkästchen **Abonnement** im Bereich **Umfang**.

   ![image](https://github.com/user-attachments/assets/0d228e47-039e-4418-ae66-025957e368bc)

9. Klicken Sie unten in der Vorlage **Wählen Sie einen Bereich aus** auf **Anwenden**.
  
10. Wählen Sie unten auf der Seite **Ressourcen** die Option **Weiter: Sammeln und liefern >** aus.

    ![image](https://github.com/user-attachments/assets/95556211-654f-4810-98a0-5cd8fac13bff)  

11. Klicken Sie auf der Seite **Sammeln und Bereitstellen** auf **+ Datenquelle hinzufügen.**

    ![image](https://github.com/user-attachments/assets/8274b0c1-8617-4889-9aef-78e050f2bd00)

12. Wählen Sie auf der Vorlage **Datenquelle hinzufügen** unter **Datenquellentyp** die folgenden Einstellungen aus:
    
    |Einstellung|Wert|
    |---|---|
    |**Datenquelle hinzufügen**|
    |Wählen Sie den Datenquellentyp und die Daten aus, die für Ihre Ressourcen gesammelt werden sollen.|
    |Datenquellentyp*|**Windows-Ereignisprotokolle**|
    |Wählen Sie „Basic“ aus, um die Sammlung von Ereignisprotokollen zu aktivieren.|
    |Konfigurieren Sie die Ereignisprotokolle und Ebenen für die Erfassung:|
    |Application|**Kritisch**, **Fehler**, **Warnung**|
    |Sicherheit|**Erfolgreiche Überwachung**, **Fehlgeschlagene Überwachung**|
    |System|**Kritisch**, **Fehler**, **Warnung**|

    ![image](https://github.com/user-attachments/assets/33039994-0613-40f4-9c55-03f795b38b9b)

13. Wählen Sie unten in der Vorlage **Datenquelle hinzufügen** die Option **Weiter: Ziel >** aus.

14. Wählen Sie in der Vorlage **Datenquelle hinzufügen** auf der Registerkarte **Ziel** die folgenden Einstellungen aus.
    
    |Einstellung|Wert|
    |---|---|
    |**Datenquelle hinzufügen**|
    |Destination|**+ Ziel hinzufügen**|
    |Zieltyp|**Azure Monitor-Protokolle**|
    |Subscription|Wählen Sie Ihr Abonnement aus.|
    |Zieldetails|**azwrkspc1a (az-rg-1**)|

     ![image](https://github.com/user-attachments/assets/dc2d2906-4a57-4df9-a33c-fd6ae34a8457)

15. Wählen Sie unten in der Vorlage **Datenquelle hinzufügen** die Option **Datenquelle hinzufügen** aus.

16. Wählen Sie unten auf der Seite **Sammeln und liefern** die Option **Überprüfen + erstellen** aus.

    ![image](https://github.com/user-attachments/assets/4277089c-971c-4334-a49d-6ac6bfe93ff4)

17. Wählen Sie unten auf der Seite **Überprüfen + erstellen** die Option **Erstellen** aus.

    ![image](https://github.com/user-attachments/assets/b532f92e-af10-4b4d-bb52-10d15ad38d4a)

> **Ergebnisse**: Sie haben eine Regel für die Datensammlung erstellt und den Azure Monitor-Agent installiert.
