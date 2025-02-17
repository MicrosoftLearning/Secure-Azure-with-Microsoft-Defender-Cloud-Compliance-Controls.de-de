---
lab:
  title: Übung 03 – Erstellen Sie einen Log Analytics-Arbeitsbereich
  module: Module 04 - Create a Log Analytics workspace
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
   
2. Geben Sie in das Suchfeld oben im Portal **Protokollanalyse-Arbeitsbereiche** ein. Wählen Sie in den Suchergebnissen **Protokollanalyse-Arbeitsbereiche** aus.

3. Wählen Sie auf der Seite **Protokollanalyse-Arbeitsbereiche** die Option **+ Erstellen** aus.

4. Geben Sie auf der Seite **Grundlagen** unter **Log Analytics-Arbeitsbereich erstellen** diese Informationen ein, oder wählen Sie sie aus:
   
   |Einstellung|Wert|
   |---|---|
   |**Projektdetails**|
   |Subscription|Wählen Sie Ihr Abonnement aus.|
   |Resource group|Geben Sie **az-rg-1** ein.|
   |**Instanzendetails**|
   |Name|Geben Sie **azwrkspc1a** ein.|
   |Region|Wählen Sie **USA, Osten** aus.|

5. Wählen Sie unten auf der Seite die Registerkarte **Überprüfen + erstellen** aus.
  
6. Klicken Sie auf **Erstellen**.

> **Ergebnisse:** Sie haben einen Log Analytics-Arbeitsbereich erstellt, um Daten von Azure-Ressourcen zu sammeln.
