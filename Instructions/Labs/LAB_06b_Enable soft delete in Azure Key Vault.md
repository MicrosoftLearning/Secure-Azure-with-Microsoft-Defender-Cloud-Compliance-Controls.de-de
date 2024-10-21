---
lab:
  title: Übung 06b – Aktivieren des vorläufigen Löschens in Azure Key Vault
  module: Module 07 - Configure Azure Key Vault networking settings
---


>**Hinweis**: Für dieses Lab benötigen Sie ein [Azure-Abonnement](https://azure.microsoft.com/en-us/free/?azure-portal=true), in dem Sie über Administratorzugriff verfügen. 


Wenn Sie einen Schlüsseltresor löschen und vorläufiges Löschen nicht aktiviert ist, werden alle Geheimnisse, Schlüssel und Zertifikate, die im Schlüsseltresor gespeichert sind, dauerhaft gelöscht. Das versehentliche Löschen eines Schlüsseltresors kann zu dauerhaftem Datenverlust führen. Vorläufiges Löschen ermöglicht es Ihnen, einen versehentlich gelöschten Schlüsseltresor innerhalb des konfigurierbaren Aufbewahrungszeitraums wiederherzustellen.

---

## Qualifikationsaufgaben

- Überprüfen Sie, ob vorläufiges Löschen für einen Schlüsseltresor aktiviert ist, und aktivieren Sie das vorläufige Löschen.

## Übungsanweisungen 

### Überprüfen, ob vorläufiges Löschen für einen Schlüsseltresor aktiviert ist, und Aktivieren des vorläufigen Löschens

1. Starten Sie eine Browsersitzung, und melden Sie sich beim [Azure-Portal-Menü](https://portal.azure.com/) an.
   
2. Wählen Sie Ihren Schlüsseltresor aus.

3. Wählen Sie auf dem Blatt **Einstellungen** die Option **Eigenschaften** aus.

4. Überprüfen Sie, ob das Optionsfeld neben „vorläufiges Löschen“ auf **Löschschutz aktivieren (eine obligatorische Aufbewahrungsfrist für gelöschte Tresore und Tresorobjekte erzwingen)** festgelegt ist.

5. Wenn die Funktion des vorläufigen Löschens im Schlüsseltresor nicht aktiviert ist, klicken Sie auf das Optionsfeld **Löschschutz aktivieren (eine obligatorische Aufbewahrungsfrist für gelöschte Tresore und Tresorobjekte erzwingen)**, um das vorläufige Löschen zu aktivieren, und klicken Sie auf **Speichern.**

![image](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/06131a60-7f00-4764-a424-87ea41a78394)

> **Ergebnisse**: Sie haben die Funktion für vorläufiges Löschen erfolgreich aktiviert und sichergestellt, dass gelöschte Ressourcen (standardmäßig) 90 Tage lang aufbewahrt werden und wiederhergestellt werden können, wodurch die Löschung über das Azure-Portal effektiv rückgängig gemacht wird.
