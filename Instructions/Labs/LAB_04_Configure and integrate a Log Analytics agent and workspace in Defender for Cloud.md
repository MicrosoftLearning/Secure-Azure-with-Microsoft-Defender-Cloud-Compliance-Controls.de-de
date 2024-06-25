---
lab:
  title: 'Übung 04: Konfigurieren und Integrieren eines Log Analytics-Agents und -Arbeitsbereichs mit Defender für Cloud'
  module: Module 05 - Configure and integrate a Log Analytics agent and workspace in Defender for Cloud
---


>**Hinweis**: Für dieses Lab benötigen Sie ein [Azure-Abonnement](https://azure.microsoft.com/en-us/free/?azure-portal=true), in dem Sie über Administratorzugriff verfügen. 


Defender für Cloud erfasst Daten von Ihren Azure-VMs, VM-Skalierungsgruppen, IaaS-Containern und Nicht-Azure-Computern (auch lokal), um sie auf Sicherheitslücken und Bedrohungen zu überwachen. Einige Defender-Pläne erfordern Überwachungskomponenten, um Daten aus Ihren Workloads zu sammeln. Wenn der Log Analytics-Agent aktiviert ist, stellt Defender for Cloud den Agent auf allen unterstützten und neu erstellten Azure-VMs bereit. 

---

## Qualifikationsaufgaben

- Verwenden Sie die Standardeinstellungen des Log Analytics-Agents für Ihren Agent-Typ.

- Wählen Sie Ihren Arbeitsbereich aus.
  
- Definieren Sie die Ebene der zu speichernden Sicherheitsereignisdaten auf der Arbeitsbereichsebene.

## Übungsanweisungen 

### Konfigurieren Sie die Integration mit dem Log Analytics-Agent.

>**Hinweis**: Wenn der Log Analytics-Agent aktiviert ist, stellt Defender for Cloud den Agent auf allen unterstützten und neu erstellten Azure-VMs bereit. 

1. Starten Sie eine Browsersitzung, und melden Sie sich beim [Azure-Portal-Menü](https://portal.azure.com/) an.
   
2. Öffnen Sie im Menü von Defender für Cloud **Umgebungseinstellungen**.

4. Wählen Sie Ihr Abonnement aus.

5. Wählen Sie in der Spalte für Einstellungen und die Überwachungsabdeckung der Defender-Pläne die Option **Einstellungen und Überwachung** aus.

7. Klicken Sie in der Log Analytics-Zeile in der Spalte „Konfiguration“ auf  **Konfiguration bearbeiten**.

8. Führen Sie in der Konfigurationsvorlage für die automatische Bereitstellung die folgenden Aktionen aus:

   - Klicken Sie unter „Arbeitsbereichsauswahl“ auf **Benutzerdefinierter Arbeitsbereich**.

   - Klicken Sie auf das **Dropdownmenü** und **wählen Sie** Ihren zuvor erstellten Arbeitsbereich aus.

   - Klicken Sie unter **Speicher für Sicherheitsereignisse** auf das **Dropdownmenü** und wählen Sie **Alle Ereignisse** aus.

   - Klicken Sie unten in der Vorlage für die automatische Bereitstellung auf **Übernehmen**.
   
![image](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/c1c812e7-b5ca-4caa-b8e6-34a6e4b325fd)




> **Ergebnisse**: Sie haben den Log Analytics-Agent und den Arbeitsbereich in Microsoft Defender for Cloud konfiguriert.
