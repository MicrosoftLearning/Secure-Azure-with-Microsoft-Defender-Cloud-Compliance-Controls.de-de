---
lab:
  title: Übung 92 - Erstellen eines Arbeitsbereichs
  module: Module 02 - Create a Log Analytics workspace for Microsoft Defender for Cloud
---


>**Hinweis**: Für dieses Lab benötigen Sie ein [Azure-Abonnement](https://azure.microsoft.com/en-us/free/?azure-portal=true), in dem Sie über Administratorzugriff verfügen. 


Wenn Sie Protokolle und Daten sammeln, werden diese Informationen in einem Arbeitsbereich gespeichert. Ein Arbeitsbereich verfügt über eine eindeutige Arbeitsbereichs-ID und Ressourcen-ID. Der Arbeitsbereichsname muss innerhalb einer Ressourcengruppe eindeutig sein. Nachdem Sie einen Arbeitsbereich erstellt haben, konfigurieren Sie Datenquellen und Lösungen, um die Daten dort zu speichern. 

---

## Qualifikationsaufgabe

- Erstellen eines Log Analytics-Arbeitsbereichs
- Ordnen Sie den Arbeitsbereich einer vorhandenen Ressourcengruppe zu.
- Geben Sie eine bestimmte Region an, um den Arbeitsbereich bereitzustellen.

## Übungsanweisungen 

### Erstellen Sie über das Menü Log Analytics-Arbeitsbereiche einen Arbeitsbereich.

1. Starten Sie eine Browsersitzung, und melden Sie sich beim [Azure-Portal-Menü](https://portal.azure.com/) an.
   
2. Geben Sie im Azure-Portalmenü im Suchfeld **Log Analytics** ein. Sobald Sie mit der Eingabe beginnen, wird die Liste auf der Grundlage Ihrer Eingabe gefiltert. Wählen Sie **Log Analytics-Arbeitsbereiche** aus.

4. Klicken Sie auf **Erstellen**.

5. Geben Sie auf der Registerkarte **Grundlagen** unter **Log Analytics-Arbeitsbereich erstellen** diese Informationen ein, oder wählen Sie sie aus:
   
   |Einstellung|Wert|
   |---|---|
   |**Projektdetails**|
   |Subscription|Wählen Sie Ihr Abonnement aus.|
   |Resource group|Geben Sie **azure-rg-1** ein. Klicken Sie auf **OK**.|
   |**Instanzendetails**|
   |Name|Geben Sie **azwrkspc1a** ein.|
   |Region|Wählen Sie **USA, Osten** aus.|

6. Wählen Sie die Registerkarte **Überprüfen + erstellen** aus, oder wählen Sie unten auf der Seite die blaue Schaltfläche „Überprüfen + Erstellen“ aus.
  
8. Klicken Sie auf **Erstellen**.

> **Ergebnisse:** Sie haben einen Log Analytics-Arbeitsbereich erstellt, um Daten von Azure-Ressourcen sowie Diagnose- oder Protokolldaten aus Azure Storage zu sammeln.
