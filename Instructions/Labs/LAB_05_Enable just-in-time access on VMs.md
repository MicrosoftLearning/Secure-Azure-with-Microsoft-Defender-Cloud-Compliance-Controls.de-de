---
lab:
  title: 'Übung 05: Aktivieren des Just-in-Time-Zugriffs auf VMs'
  module: Module 06 - Explore just-in-time VM access
---


>**Hinweis**: Für dieses Lab benötigen Sie ein [Azure-Abonnement](https://azure.microsoft.com/en-us/free/?azure-portal=true), in dem Sie über Administratorzugriff verfügen. 


Mithilfe des Just-in-Time-Zugriffs (JIT) von Microsoft Defender for Cloud können Sie Ihre virtuellen Azure-Computer (VMs) vor nicht autorisiertem Netzwerkzugriff schützen. Firewalls enthalten häufig Zulassungsregeln, die Ihre VMs anfällig für Angriffe machen. Mit JIT können Sie den Zugriff auf Ihre VMs nur bei Bedarf, an den benötigten Ports und für die benötigte Zeitspanne erlauben. 

---

## Qualifikationsaufgaben

- Aktivieren Sie JIT auf Ihren VMs im Azure-Portal.

- Fordern Sie im Azure-Portal Zugriff auf eine VM an, für die JIT aktiviert ist.

## Übungsanweisungen 

### Aktivieren von JIT auf Ihren VMs über virtuelle Azure-Computer

>**Hinweis**: Sie können JIT auf einer VM über die Seiten für virtuelle Azure-Computer des Azure-Portals aktivieren.

1. Starten Sie eine Browsersitzung und melden Sie sich beim [Azure-Portal-Menü](https://portal.azure.com/) an.
  
2. Geben Sie im Suchfeld oben im Portal den Begriff **Virtuelle Computer** ein. Wählen Sie in den Suchergebnissen **Virtuelle Computer** aus.

3. Wählen Sie **vm-1** aus.
 
4. Wählen Sie **Konfiguration** aus dem Abschnitt **Einstellungen** von vm-1 aus.
   
5. Wählen Sie unter **Just-In-Time-VM-Zugriff** die Option **Just-In-Time aktivieren** aus.

6. Klicken Sie unter **Just-In-Time-Zugriff auf VMs** auf den Link **Microsoft Defender for Cloud öffnen**.

7. Standardmäßig gelten für den Just-in-Time-Zugriff auf die VM die folgenden Einstellungen:

   - Windows-Computer
   
     - RDP-Port: 3389
     - Maximal erlaubte Zugriffsdauer: drei Stunden
     - Zulässige Quell-IP-Adressen: beliebige

   - Linux-Computer
     - SSH-Port: 22
     - Maximal erlaubte Zugriffsdauer: drei Stunden
     - Zulässige Quell-IP-Adressen: beliebige
   
8. Standardmäßig gelten für den Just-in-Time-Zugriff auf die VM die folgenden Einstellungen:

   - Klicken Sie auf der Registerkarte **Konfiguriert** mit der rechten Maustaste auf die VM, zu der Sie einen Port hinzufügen möchten, und wählen Sie „Bearbeiten“ aus.

   ![image](https://github.com/user-attachments/assets/aa4ded55-c5b1-4d40-b5a0-a4c33b9eb81b)
   
   - Unter **JIT-VM-Zugriffskonfiguration** können Sie die vorhandenen Einstellungen eines bereits geschützten Ports bearbeiten oder einen neuen benutzerdefinierten Port hinzufügen.
   - Wenn Sie die Bearbeitung der Ports abgeschlossen haben, wählen Sie **Speichern** aus.   

### Fordern Sie Zugriff auf eine JIT-fähige VM über die Seite „Verbinden“ des virtuellen Azure-Computers an.

>**Hinweis**: Wenn JIT für eine VM aktiviert ist, müssen Sie zum Herstellen der Verbindung entsprechend Zugriff anfordern. Sie können Zugriff auf jede der unterstützten Arten anfordern, unabhängig davon, wie Sie JIT aktiviert haben.
   
1. Öffnen Sie im Azure-Portal die Seiten mit den virtuellen Computern.

2. Wählen Sie die VM aus, mit der Sie eine Verbindung herstellen möchten, und öffnen Sie die Seite **Verbinden**.

   - Azure prüft, ob JIT auf diesem virtuellen Computer aktiviert ist.

        - Wenn JIT für den virtuellen Computer nicht aktiviert ist, werden Sie aufgefordert, es zu aktivieren.
    
        - Wenn JIT aktiviert ist, wählen Sie **Zugriff anfordern** aus, um eine Zugriffsanforderung mit der anfordernden IP-Adresse, dem Zeitbereich und den Ports zu übergeben, die für diese VM konfiguriert wurden.
    
   ![image](https://github.com/user-attachments/assets/f5d0b67c-7731-4261-b0eb-a56c505dadd4)

> **Ergebnisse**: Sie haben verschiedene Methoden zum Aktivieren von JIT auf Ihren VMs und zum Anfordern von Zugriff auf VMs untersucht, bei denen JIT in Microsoft Defender for Cloud aktiviert ist.
