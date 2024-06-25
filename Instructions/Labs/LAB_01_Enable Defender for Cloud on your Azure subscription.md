---
lab:
  title: 'Übung 01: Aktivieren von Defender for Cloud für Ihr Azure-Abonnement'
  module: Module 02 - Enable Defender for Cloud on your Azure subscription
---


>**Hinweis**: Für dieses Lab benötigen Sie ein [Azure-Abonnement](https://azure.microsoft.com/en-us/free/?azure-portal=true), in dem Sie über Administratorzugriff verfügen. 


Das Hauptziel dieser Übung besteht darin, praktische Erfahrungen beim Konfigurieren und Aktivieren von Microsoft Defender for Cloud in einem Azure-Abonnement zu bieten. Dadurch können Sie Ihre Cloudressourcen überwachen und vor Sicherheitsbedrohungen schützen. 

---

## Qualifikationsaufgaben

- Führen Sie ein Upgrade Ihres Abonnements für Microsoft Defender for Cloud durch.
  
- Stellen Sie den Microsoft Monitoring Agent auf den erforderlichen Computern bereit, um eine umfassende Abdeckung zu gewährleisten.

## Übungsanweisungen

### Aktualisieren von Microsoft Defender für die Cloud

1. Melden Sie sich im [Menü des Azure-Portals](https://portal.azure.com/) an.

2. Geben Sie im Azure-Portal oben im Textfeld Ressourcen, Dienste und Dokumente durchsuchen Microsoft Defender für Cloud ein, und drücken Sie die EINGABETASTE.

3. Wechseln Sie auf dem Blatt **Erste Schritte** von **Microsoft Defender for Cloud** zur Registerkarte **Upgrade**. Führen Sie einen Bildlauf nach unten durch, bis der Abschnitt **Abonnements und Arbeitsbereiche auswählen, die mit erweiterten Sicherheitsfeatures geschützt werden sollen** sichtbar ist.

4. Aktivieren Sie den Microsoft Defender-Plan, indem Sie Ihr **Abonnement** und den **Log Analytics-Arbeitsbereich** auswählen, den Sie in Modul 02 erstellt haben.

5. Klicken Sie unten auf der Seite auf die große blaue Schaltfläche **Upgrade**.
   
    ![image](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/256bd584-b04f-4d5b-81a7-c83dd1af3b4f)
   
6. Wechseln Sie auf dem **Microsoft Defender for Cloud**-Blatt **Erste Schritte** zur Registerkarte **Agents installieren**, und führen Sie einen Bildlauf nach unten durch.

    ![image](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/8120ec8f-23dc-4636-bc45-b415c7894b8c)

7. Aktivieren Sie das Kontrollkästchen, das dem Abonnement zugeordnet ist, in dem Agents installiert werden sollen, und klicken Sie auf **Agents installieren**.

### Alternative Aktionen zum Upgrade Ihres Abonnements für Microsoft Defender for Cloud.

1. Navigieren Sie zu **Microsoft Defender for Cloud** und klicken Sie im linken Navigationsbereich unter dem Abschnitt Verwaltung auf **Umgebungseinstellungen**.
   
2. Klicken Sie auf dem Microsoft Defender for Cloud-Blatt **Umgebungseinstellungen** auf **Alle erweitern**, führen Sie einen Bildlauf nach unten durch, bis Ihr Abonnement angezeigt wird, und klicken Sie auf das entsprechende Abonnement.

3. Wählen Sie auf dem Blatt **Einstellungen, Defender-Pläne** die Option **Alle Pläne aktivieren** aus, und klicken Sie auf **Speichern**.

   ![image](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Defender-for-Cloud-regulatory-compliance-controls/assets/91347931/4b684851-98ae-4720-a3e3-afa99aab8c43)




   

   
> **Ergebnisse**: Sie haben ein Upgrade für Defender for Cloud in Ihrem Azure-Abonnement durchgeführt und aktiviert.
