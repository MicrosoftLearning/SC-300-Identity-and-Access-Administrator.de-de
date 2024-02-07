---
lab:
  title: '18: Zugriffsrichtlinien für Defender for Cloud Apps'
  learning path: '03'
  module: Module 03 - Implement Access Management for Apps
---

# 18: Zugriffs- und Sitzungsrichtlinien für Defender for Cloud Apps

## Labszenario

Mit Microsoft Defender for Cloud-Apps können wir zusätzliche Richtlinien für den bedingten Zugriff erstellen, die speziell für die von uns überwachten Cloud-Apps gelten.  Das Erstellen dieser Richtlinien kann über das Menü „Steuerung“ im Microsoft Defender for Cloud Apps-Portal erfolgen.

#### Geschätzte Dauer: 20 Minuten

### Übung 1: Erstellen und Testen der App-Steuerungsrichtlinie für bedingten Zugriff

#### Aufgabe 1: Bestätigen, dass PradeepG bedingungslosen Zugriff auf FORMS hat

1. Öffnen Sie ein neues **InPrivate-Browserfenster**.
2. Stellen Sie eine Verbindung mit [https://forms.microsoft.com](https://forms.microsoft.com) her.
3. Wählen Sie die Anmeldung rechts oben auf der Seite aus.
4. Melden Sie sich als „Pradeep Gupta“ an.
   - Benutzername = PradeepG@<<<your lab hoster provided domain>>>
   - Kennwort = das Kennwort von der Registerkarte „Ressourcen“
5. Vergewissern Sie sich, dass Microsoft Forms geöffnet wird und keine Warnmeldungen angezeigt werden.
6. Schließen Sie das InPrivate-Browserfenster.

#### Aufgabe 2: Konfigurieren von Azure AD für die Verwendung mit Defender for Cloud Apps.

1. Navigieren Sie zu [portal.azure.com](portal.azure.com), und wechseln Sie zu Azure Active Directory.

2. Wählen Sie unter **Verwalten** die Option **Sicherheit** aus.

3. Wählen Sie unter **Schützen** die Option **Bedingter Zugriff** aus.

4. Wählen Sie in der Dropdownliste **+ Neue Richtlinie** und dann **Neue Richtlinie erstellen** aus.

5. Geben Sie einen Richtliniennamen ein, wie etwa **Monitor Pradeep using Forms**.

6. Wählen Sie unter **Users or workload identities** die Option **Bestimmte Benutzer eingeschlossen**, dann **Benutzer und Gruppen auswählen** aus, und markieren Sie die **Benutzer und Gruppen**.

7. Wählen Sie das Konto **Pradeep Gupta** für den Labmandanten und dann **Auswählen** aus.

8. Wählen Sie unter **Cloud-Apps oder -Aktionen** die Option **Keine Cloud-Apps, Aktionen oder Authentifizierungskontexte ausgewählt** aus.

9. Wählen Sie **Apps auswählen**, dann **Microsoft Forms** und schließlich **Auswählen** aus. 

10. Wählen Sie unter **Zugriffskontrollen** die Option **Sitzung** und ** 0 Steuerelemente ausgewählt** aus.

11. Wählen Sie das Feld **App-Steuerung für bedingten Zugriff verwenden** aus, belassen Sie die Standardeinstellung **Nur überwachen**, und wählen Sie **Auswählen** aus.

12. Wählen Sie unter **Richtlinie aktivieren** die Option **Aktiviert** und dann **Erstellen** aus.

#### Aufgabe 3: Anmelden Forms und Überprüfen, ob der bedingte Zugriff überwacht wird

1. Öffnen Sie ein neues **InPrivate-Browserfenster**.
2. Stellen Sie eine Verbindung mit [https://forms.microsoft.com](https://forms.microsoft.com) her.
3. Wählen Sie die Anmeldung rechts oben auf der Seite aus.
4. Melden Sie sich als „Pradeep Gupta“ an.
   - Benutzername = PradeepG@<<<your lab hoster provided domain>>>
   - Kennwort = das Kennwort von der Registerkarte „Ressourcen“
5. Vergewissern Sie sich, dass Pradeep Zugriff hat und dass Sie eine neue Nachricht erhalten:
   - Ihr Unternehmen überwacht die Nutzung dieser Anwendung.
6. Schließen Sie das InPrivate-Browserfenster.

### Übung 2: Einrichten von Warnungen in Microsoft Defender for Cloud Apps

#### Aufgabe 1: Zugreifen auf Microsoft Defender for Cloud Apps und Erstellen der App-Steuerung für bedingten Zugriff

Bei der Registrierung Ihrer Anwendung wird eine Vertrauensstellung zwischen Ihrer App und Microsoft Identity Platform erstellt. Die Vertrauensstellung ist unidirektional: Ihre App vertraut Microsoft Identity Platform und nicht umgekehrt.

1. Melden Sie sich mit einem globalen Administratorkonto bei [https://security.microsoft.com](https://security.microsoft.com) an.

1. Scrollen Sie im linken Menü nach unten, und wählen Sie **Weitere Ressourcen** aus.

1. Suchen Sie im Fenster **Weitere Ressourcen** die Option **Öffnen** unter **Microsoft Defender for Cloud Apps**, und wählen Sie sie aus.  Dadurch gelangen Sie zum **Microsoft Defender for Cloud Apps-Portal** innerhalb des Microsoft 365-Kontos.

1. Wählen Sie im Portalmenü von **Microsoft Defender for Cloud Apps** den Dropdownpfeil für **Steuerung** aus, und wählen Sie **Richtlinien** aus.

1. Wählen Sie **+ Richtlinie erstellen** aus. Wählen Sie **Zugriffsrichtlinie** aus.

1. Geben Sie einen Namen für die Richtlinie ein, wie etwa **Monitor Microsoft Forms access**.

1. Sie können die Einstellung der **Kategorie** als **Zugriffssteuerung** belassen.

1. Wählen Sie unter **Activities matching all of the following** die Dropdownliste für **Intune compliant, In Hybrid-Azure AD eingebunden** aus, und heben Sie die Auswahl von **In Hybrid-Azure AD eingebunden** auf.

1. Wählen Sie die Dropdownliste für **Apps auswählen** aus.  Wählen Sie **Microsoft Forms** aus.

1. Belassen Sie **Aktionen** als **Test**.

1. Belassen Sie unter **Benachrichtigungen** die Option **Warnung für jedes mit...** aktiviert, und wählen Sie **Sent alert as email** aus.

1. Geben Sie die E-Mail-Adresse des Labadministrators ein, und drücken Sie die **Eingabetaste** auf der Tastatur.

1. Wählen Sie **Erstellen** aus, um die Zugriffsrichtlinie zu erstellen.

#### Aufgabe 2: Melden Sie sich bei Forms als Pradeep an, um Aktivitäten auszulösen

1. Öffnen Sie ein neues **InPrivate-Browserfenster**.
2. Stellen Sie eine Verbindung mit [https://forms.microsoft.com](https://forms.microsoft.com) her.
3. Wählen Sie die Anmeldung rechts oben auf der Seite aus.
4. Melden Sie sich als „Pradeep Gupta“ an.
   - Benutzername = PradeepG@<<<your lab hoster provided domain>>>
   - Kennwort = das Kennwort von der Registerkarte „Ressourcen“
5. Vergewissern Sie sich, dass Pradeep Zugriff hat und dass Sie eine neue Nachricht erhalten:
   - Ihr Unternehmen überwacht die Nutzung dieser Anwendung.
6. Schließen Sie das InPrivate-Browserfenster.

#### Aufgabe 3: Überprüfen der Aktivität in Defender for Cloud Apps

1. Kehren Sie zum Browser zurück, in dem Defender for Cloud Apps ausgeführt wird.
2. Aktualisieren Sie den Browser, um sicherzustellen, dass die neuesten Daten heruntergeladen werden.
3. Wählen Sie im Menü **Untersuchen** die Option **Aktivitätsprotokoll** aus.
4. Verwenden Sie **App: Filter**, und wählen Sie **Microsoft Forms** in der Liste aus.
5. Beachten Sie die Anmeldedatensätze für Pradeep.
