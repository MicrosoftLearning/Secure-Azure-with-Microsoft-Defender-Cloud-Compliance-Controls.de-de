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

1. Geben Sie in das Suchfeld oben auf dem Portal **Datensammlungsregel** ein. Wählen Sie **Datensammlungsregeln** in den Suchergebnissen  aus.
  
2. Wählen Sie auf der Seite mit den **Datensammlungsregeln** die Option **Erstellen** aus.
  
   ![image](https://github.com/user-attachments/assets/99b9ac51-f2f4-466f-80bb-79d74874b573)

3. Geben Sie auf der Seite **Grundlagen** der **Regel zur Datensammlung erstellen** die folgenden Einstellungen an (lassen Sie die anderen auf ihren Standardwerten):

    |Einstellung|Wert|
    |---|---|
    |**Regeldetails**|
    |Regelname|**dcr-1**|
    |Subscription|Wählen Sie Ihr Abonnement aus.|
    |Resource group|**az-rg-1**|
    |Region|**USA, Osten**|
    |Plattformtyp|**Windows**|
    |Datensammlungsendpunkt|Belassen Sie die Standardeinstellung auf „Keine“|

    ![image](https://github.com/user-attachments/assets/35c527cf-499d-44b9-966f-0114b8643ef2)

4. Klicken Sie auf die Schaltfläche am Ende der Seite **Grundlagen** mit der Bezeichnung **Weiter: Ressourcen > fortfahren.**
   
5. Wählen Sie auf der Seite **Ressourcen** die Option **+ Ressourcen hinzufügen** aus.

    ![image](https://github.com/user-attachments/assets/6aabf2c9-bea2-47c1-9b0b-bf131cdec4e3)

6. Aktivieren Sie in der Vorlage **Bereich auswählen** das Kontrollkästchen **Abonnement** im Bereich **Umfang**.

    ![image](https://github.com/user-attachments/assets/2215e8cd-5047-4fc6-91ba-b2c645571bbd)

7. Klicken Sie unten in der Vorlage **Wählen Sie einen Bereich aus** auf **Anwenden**.
  
8. Wählen Sie unten auf der Seite **Ressourcen** die Option **Weiter: Sammeln und liefern >** aus.

    ![image](https://github.com/user-attachments/assets/717226c3-5ce0-454f-93a4-11b0e67d5a23)

9. Klicken Sie auf der Seite **Sammeln und Bereitstellen** auf **+ Datenquelle hinzufügen.**

    ![image](https://github.com/user-attachments/assets/0809cf5b-a460-40d1-8508-e42ba7ce78c1)

10. Wählen Sie auf der Vorlage **Datenquelle hinzufügen** unter **Datenquellentyp** die folgenden Einstellungen aus.
    
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

    ![image](https://github.com/user-attachments/assets/5bc891ea-8cef-4baa-95c4-a432364179b1)

12. Wählen Sie unten in der Vorlage **Datenquelle hinzufügen** die Option **Weiter: Ziel >** aus.
   
13. Wählen Sie in der Vorlage **Datenquelle hinzufügen** auf der Registerkarte **Ziel** die folgenden Einstellungen aus.
    
    |Einstellung|Wert|
    |---|---|
    |**Datenquelle hinzufügen**|
    |Destination|**+ Ziel hinzufügen**|
    |Zieltyp|**Azure Monitor-Protokolle**|
    |Subscription|Wählen Sie Ihr Abonnement aus.|
    |Zieldetails|**azwrkspc1a (az-rg-1**)|

    ![image](https://github.com/user-attachments/assets/e00c17c8-5a70-4caa-8504-92f482cc5e57)

14. Wählen Sie unten in der Vorlage **Datenquelle hinzufügen** die Option **Datenquelle hinzufügen** aus.

    ![image](https://github.com/user-attachments/assets/4277089c-971c-4334-a49d-6ac6bfe93ff4)

15. Wählen Sie unten auf der Seite **Sammeln und liefern** die Option **Überprüfen + erstellen** aus.

    ![image](https://github.com/user-attachments/assets/0235fed9-6309-444c-9269-b9dbd1118b63)

16. Wählen Sie unten auf der Seite **Überprüfen + erstellen** die Option **Erstellen** aus.

> **Ergebnisse**: Sie haben eine Regel für die Datensammlung erstellt und den Azure Monitor-Agent installiert.
