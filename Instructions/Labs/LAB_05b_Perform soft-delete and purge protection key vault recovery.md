---
lab:
  title: "Übung\_05b\_– Konfigurieren der Azure Key Vault-Wiederherstellungsverwaltung mit Schutz durch vorläufiges Löschen und Bereinigungsschutz"
  module: Module 05 - Perform soft-delete and purge protection key vault recovery
---


>**Hinweis**: Für dieses Lab benötigen Sie ein [Azure-Abonnement](https://azure.microsoft.com/en-us/free/?azure-portal=true), in dem Sie über Administratorzugriff verfügen. 


Sie verwenden den Bereinigungsschutz, um das Löschen Ihres Schlüsseltresors, Ihrer Schlüssel, Geheimnisse und Zertifikate durch böswillige Insider*innen verhindern. Stellen Sie sich dieses Features als einen Papierkorb mit einem Zeitschloss vor. Sie können Elemente während des konfigurierbaren Aufbewahrungszeitraums jederzeit wiederherstellen. Sie können einen Schlüsseltresor erst dann dauerhaft löschen oder bereinigen, wenn der Aufbewahrungszeitraum abgelaufen ist. Nach Ablauf des Aufbewahrungszeitraums wird der Schlüsseltresor oder das Schlüsseltresorobjekt automatisch bereinigt.

---

## Qualifikationsaufgabe

- Überprüfen Sie, ob vorläufiges Löschen für einen Schlüsseltresor aktiviert ist, und aktivieren Sie das vorläufige Löschen.

- Listen Sie vorläufig gelöschte Schlüsseltresore auf, stellen Sie sie wieder her, oder bereinigen Sie sie.

- Listen Sie vorläufig gelöschte Geheimnisse, Schlüssel und Zertifikate auf, stellen Sie sie wieder her, oder bereinigen Sie sie.

## Übungsanweisungen 

### Überprüfen, ob vorläufiges Löschen für einen Schlüsseltresor aktiviert ist, und Aktivieren des vorläufigen Löschens

1. Starten Sie eine Browsersitzung, und melden Sie sich beim [Azure-Portal-Menü](https://portal.azure.com/) an.
   
2. Wählen Sie Ihren Schlüsseltresor aus.

3. Klicken Sie auf das Blatt **Eigenschaften**.

4. Überprüfen Sie, ob das Optionsfeld neben „Vorläufiges Löschen“ auf **Bereinigungsschutz aktivieren** festgelegt ist.

5. Wenn für den Schlüsseltresor vorläufiges Löschen nicht aktiviert ist, klicken Sie auf das Optionsfeld, um das vorläufige Löschen zu aktivieren, und klicken Sie dann auf **Speichern**.

![image](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/06131a60-7f00-4764-a424-87ea41a78394)


### Listen Sie vorläufig gelöschte Schlüsseltresore auf, stellen Sie sie wieder her, oder bereinigen Sie sie.

1. Starten Sie eine Browsersitzung, und melden Sie sich beim [Azure-Portal-Menü](https://portal.azure.com/) an.
   
2. Klicken Sie oben auf der Seite auf die Suchleiste.

3. Suchen Sie den Dienst **Key Vault**. Klicken Sie nicht auf einen bestimmten Schlüsseltresor.

4. Klicken Sie oben im Bildschirm auf „Gelöschte Tresore verwalten“.

5. Auf der rechten Seite des Bildschirms wird ein Kontextbereich geöffnet.

6. Wählen Sie Ihr Abonnement aus.

7. Wenn Ihr Schlüsseltresor vorläufig gelöscht wurde, wird er im Kontextbereich auf der rechten Seite angezeigt.

8. Wenn zu viele Tresore angezeigt werden, klicken Sie unten im Kontextbereich auf „Weitere laden“, oder rufen Sie die Ergebnisse über die Befehlszeilenschnittstelle oder PowerShell ab.

9. Wenn Sie den Tresor gefunden haben, den Sie **wiederherstellen** oder **bereinigen** möchten, aktivieren Sie die **Checkbox** daneben.

10. Wählen Sie die Option „Wiederherstellen“ am unteren Rand des Kontextbereichs aus, wenn Sie den Schlüsseltresor wiederherstellen möchten.

11. Wählen Sie die Option „Bereinigen“ aus, wenn Sie den Schlüsseltresor dauerhaft löschen möchten.

![image](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/f41c0673-3832-4d3f-8b05-48e46e6c2282)


### Auflisten, Wiederherstellen oder Bereinigen vorläufig gelöschter Geheimnisse, Schlüssel und Zertifikate

1. Starten Sie eine Browsersitzung, und melden Sie sich beim [Azure-Portal-Menü](https://portal.azure.com/) an.
   
2. Wählen Sie Ihren Schlüsseltresor aus.

3. Wählen Sie das Blatt des Geheimnistyps aus, den Sie verwalten möchten (Schlüssel, Geheimnisse oder Zertifikate).

4. Klicken Sie oben auf dem Bildschirm auf „Gelöschte Schlüssel (Geheimnisse, Zertifikate) verwalten“.

5. Auf der rechten Seite des Bildschirms wird ein Kontextbereich angezeigt.

6. Wenn das Geheimnis, der Schlüssel oder das Zertifikat in der Liste nicht angezeigt wird, wurde es bzw. er nicht vorläufig gelöscht.

7. Wählen Sie das Geheimnis, den Schlüssel oder das Zertifikat aus, den oder das Sie verwalten möchten.

8. Wählen Sie unten im Kontextbereich „Wiederherstellen“ oder „Bereinigen“ aus.

![image](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/dab95f78-1642-4883-b56f-70e1e5320d45)


  > **Ergebnisse**: Sie haben die Azure Key Vault-Wiederherstellungsverwaltung mit vorläufigem Löschen und Bereinigungsschutz im Azure-Portal durchgeführt.
