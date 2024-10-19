---
lab:
  title: 'Übung 04 – Erstellen Sie eine Datenerfassungsregel, und installieren Sie den Azure Monitor-Agent'
  module: Module 05 - Create a data collection rule and install the Azure Monitor Agent
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

### Erstellen und definieren Sie eine Datensammlungsregel.

>**Hinweis**: Erstellen Sie Ihre Datensammlungsregel in der gleichen Region wie Ihr Zielarbeitsbereich für Protokollanalyse oder Azure Monitor. Sie können die Datensammlungsregel Computern oder Containern aus einer beliebigen Abonnement- oder Ressourcengruppe im Mandanten zuordnen.

1. Geben Sie im Suchfeld oben im Portal **Datensammlungsregeln** ein. Wählen Sie in den Suchergebnissen **Datensammlungsregeln** aus.
  
2. Wählen Sie **+ Erstellen** aus.

![image](https://github.com/user-attachments/assets/99b9ac51-f2f4-466f-80bb-79d74874b573)

3. Geben Sie auf der Seite **Grundlagen** des Blatts **Datenerfassungsregel erstellen** die folgenden Einstellungen an (belassen Sie die anderen mit ihren Standardwerten):

    |Einstellung|Wert|
    |---|---|
    |**Regeldetails**|
    |Regelname|**dcr-1**|
    |Abonnement|Name des Abonnements, das Sie für diese Übung verwenden|
    |Resource group|**az-rg-1**|
    |Region|**USA, Osten**|
    |Plattformtyp|**Windows**|
    |Datensammlungsendpunkt|*Lassen Sie den Standardwert auf Keine*|

![image](https://github.com/user-attachments/assets/35c527cf-499d-44b9-966f-0114b8643ef2)

4. Klicken Sie auf die Schaltfläche mit dem Text **Weiter: Ressourcen >** , um fortzufahren.
   
5. Wählen Sie auf der Seite **Ressourcen** die Option **+ Ressourcen hinzufügen** aus.
  
>**Hinweis**: Der Azure Monitor-Agent wird automatisch auf den virtuellen Computern (Ressourcen) installiert, die zum Sammeln von Daten ausgewählt sind.

![image](https://github.com/user-attachments/assets/47174eb4-4343-49a2-b49d-e9dee76787e4)

6. Aktivieren Sie in der Vorlage **Bereich auswählen** das Feld **Abonnement** im **Bereich**.

![image](https://github.com/user-attachments/assets/2215e8cd-5047-4fc6-91ba-b2c645571bbd)

7. Klicken Sie unten in der Vorlage **Bereich auswählen** auf **Anwenden**.
  
8. Wählen Sie unten auf der Seite **Ressourcen** die Option **Weiter: Sammeln und übermitteln >** aus. 

![image](https://github.com/user-attachments/assets/717226c3-5ce0-454f-93a4-11b0e67d5a23)

9. Klicken Sie auf der Seite **Sammeln und liefern** auf **+ Datenquelle hinzufügen**.

![image](https://github.com/user-attachments/assets/0809cf5b-a460-40d1-8508-e42ba7ce78c1)

10. Wählen Sie in der Vorlage **Datenquelle hinzufügen** unter **Datenquellentyp** die folgenden Einstellungen aus.
    
    |Einstellung|Wert|
    |---|---|
    |**Datenquelle hinzufügen**|
    |Wählen Sie den Typ der Datenquelle und die zu erfassenden Daten für Ihre Ressource(n) aus|
    |Datenquellentyp*|**Windows-Ereignisprotokolle**|
    |Konfigurieren Sie die zu sammelnden Ereignisprotokolle und -ebenen|
    |Application|**Kritisch**, **Fehler**, **Warnung**|
    |Sicherheit|**Überwachungserfolg**, **Überwachungsfehler**|
    |System|**Kritisch**, **Fehler**, **Warnung**|

![image](https://github.com/user-attachments/assets/5bc891ea-8cef-4baa-95c4-a432364179b1)

11. Wählen Sie unten in der Vorlage **Datenquelle hinzufügen** die Option **Weiter: Ziel** aus.
   
12. Wählen Sie in der Vorlage **Datenquelle hinzufügen** auf der Registerkarte **Ziel** die folgenden Einstellungen aus.
    
    |Einstellung|Wert|
    |---|---|
    |**Datenquelle hinzufügen**|
    |Destination|**+ Ziel hinzufügen**|
    |Zieltyp|**Azure Monitor-Protokolle**|
    |Subscription|Wählen Sie Ihr Abonnement aus.|
    |Zieldetails|**azwrkspc1a (az-rg-1**)

![image](https://github.com/user-attachments/assets/e00c17c8-5a70-4caa-8504-92f482cc5e57)

13. Wählen Sie unten in der Vorlage **Datenquelle hinzufügen** die Option **Datenquelle hinzufügen** aus.

![image](https://github.com/user-attachments/assets/4277089c-971c-4334-a49d-6ac6bfe93ff4)

14. Wählen Sie unten auf der Seite **Sammeln und liefern** die Option **Überprüfen + erstellen** aus.

![image](https://github.com/user-attachments/assets/0235fed9-6309-444c-9269-b9dbd1118b63)

15. Wählen Sie unten auf der Seite **Überprüfen + erstellen** die Option **Erstellen** aus.

> **Ergebnisse**: Sie haben eine Datensammlungsregel erstellt und den Azure Monitor-Agent installiert.
