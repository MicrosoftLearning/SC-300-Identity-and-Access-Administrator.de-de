---
lab:
  title: '18: Zugriffsrichtlinien für Defender for Cloud Apps'
  learning path: '03'
  module: Module 03 - Implement Access Management for Apps
---

# 18: Zugriffs- und Sitzungsrichtlinien für Defender for Cloud Apps

## Labszenario

Mit Microsoft Defender for Cloud Apps können wir zusätzliche Richtlinien für den bedingten Zugriff erstellen, die speziell für die von uns überwachten Cloud-Apps gelten.  Das Erstellen dieser Richtlinien kann über das Steuerungsmenü im Microsoft Defender for Cloud Apps-Portal erfolgen.

#### Geschätzte Dauer: 20 Minuten

### Übung 1: Erstellen und Testen der App-Steuerungsrichtlinie für bedingten Zugriff

#### Aufgabe 1: Bestätigen, dass PradeepG uneingeschränkten Zugriff auf FORMS hat

1. Starten Sie ein neues **InPrivate-Browserfenster**.
2. Stellen Sie eine Verbindung mit [https://forms.microsoft.com](https://forms.microsoft.com)her.
3. Wählen Sie oben rechts auf der Seite „Anmelden“ aus.
4. Melden Sie sich als Pradeep Gupta an.
   - Benutzername = PradeepG@<<<your lab hoster provided domain>>>
   - Kennwort = das Kennwort auf der Registerkarte „Ressourcen“
5. Vergewissern Sie sich, dass Microsoft Forms geöffnet wird und keine Warnmeldungen angezeigt werden.
6. Schließen Sie das InPrivate-Browserfenster.

#### Aufgabe 2: Konfigurieren von Microsoft Entra ID für Microsoft Defender for Cloud Apps

1. Navigieren Sie zu [https://entra.microsoft.com](https://entra.microsoft.com), und wechseln Sie zu Microsoft Entra ID.

2. Wählen Sie unter **Identität** die Option **Schutz** aus.

3. Wählen Sie dann **Bedingter Zugriff** aus.

4. Wählen Sie **+Neue Richtlinie erstellen** aus.

5. Geben Sie einen Richtliniennamen ein, z. B. **Monitor Pradeep using Forms**.

6. Wählen Sie auf der Registerkarte **Zuweisungen** die Option **0 Benutzer und Gruppen ausgewählt** aus, und wählen Sie **Bestimmte Benutzer eingeschlossen** aus. Wählen Sie dann **Benutzer und Gruppen auswählen** aus, und markieren Sie **Benutzer und Gruppen**.

7. Wählen Sie das Konto **Pradeep Gupta** für den Labmandanten und dann **Auswählen** aus.

8. Wählen Sie unter **Zielressourcen** die Option **Keine Zielressourcen ausgewählt** aus.

9. Wählen Sie **Apps auswählen**, dann **Microsoft Forms** und anschließend **Auswählen** aus. 

10. Wählen Sie unter **Zugriffssteuerungen** die Optionen **Sitzung** und **0 Steuerelemente ausgewählt** aus.

11. Wählen Sie das Feld **App-Steuerung für bedingten Zugriff verwenden** aus, ändern Sie die Standardeinstellung **Nur überwachen** nicht, und wählen Sie **Auswählen** aus.

12. Wählen Sie unter **Richtlinie aktivieren** die Option **Ein** und dann **Erstellen** aus.

#### Aufgabe 3: Anmelden bei Forms und Überprüfen, ob der bedingte Zugriff „Überwachen“ ist

1. Starten Sie ein neues **InPrivate-Browserfenster**.
2. Stellen Sie eine Verbindung mit [https://forms.microsoft.com](https://forms.microsoft.com)her.
3. Wählen Sie oben rechts auf der Seite „Anmelden“ aus.
4. Melden Sie sich als Pradeep Gupta an.
   - Benutzername = PradeepG@<<<your lab hoster provided domain>>>
   - Kennwort = das Kennwort auf der Registerkarte „Ressourcen“
5. Vergewissern Sie sich, dass Pradeep Zugriff hat und dass Sie eine neue Nachricht erhalten:
   - Ihr Unternehmen überwacht die Nutzung dieser Anwendung.
6. Schließen Sie das InPrivate-Browserfenster.

### Übung 2: Einrichten von Warnungen in Microsoft Defender for Cloud Apps

#### Aufgabe 1: Zugreifen auf Microsoft Defender for Cloud Apps und Erstellen der App-Steuerung für bedingten Zugriff

Beim Registrieren Ihrer Anwendung wird eine Vertrauensstellung zwischen Ihrer App und Microsoft Identity Platform erstellt. Die Vertrauensstellung ist unidirektional: Ihre App vertraut Microsoft Identity Platform und nicht umgekehrt.

1. Melden Sie sich bei [https://security.microsoft.com](https://security.microsoft.com) mit einem globalen Administratorkonto an.

1. Führen Sie im linken Menü einen Bildlauf nach unten durch, und wählen Sie **Weitere Ressourcen** aus.

1. Suchen Sie im Fenster **Weitere Ressourcen** die Option **Öffnen** unter **Microsoft Defender for Cloud Apps**, und wählen Sie sie aus.  Dadurch gelangen Sie zum **Microsoft Defender for Cloud Apps-Portal** innerhalb des Microsoft 365-Kontos.

1. Wählen Sie im Portalmenü **Microsoft Defender for Cloud Apps** den Dropdownpfeil für **Steuerung** aus, und wählen Sie **Richtlinien** aus.

1. Klicken Sie auf **+ Richtlinie erstellen**. Wählen Sie **Zugriffsrichtlinie** aus.

1. Geben Sie einen Namen für die Richtlinie ein, z. B. **Monitor Microsoft Forms access**.

1. Sie können für **Kategorie** die Option **Zugriffssteuerung** belassen.

1. Wählen Sie unter **Aktivitäten, die mit Folgendem übereinstimmen** die Dropdownliste für **Intune-konform, in Microsoft Entra Hybrid eingebunden** aus, und heben Sie die Auswahl von **In Microsoft Entra Hybrid eingebunden** auf.

1. Wählen Sie die Dropdownliste für **Apps auswählen** aus.  Wählen Sie **Microsoft Forms** aus.

1. Lassen Sie **Aktionen** als **Test**.

1. Lassen Sie unter **Benachrichtigungen** die Option **Warnung erstellen...** aktiviert, und wählen Sie **Warnung als E-Mail senden** aus.

1. Geben Sie die E-Mail-Adresse des Labadministrators ein, und wählen Sie auf der Tastatur die **EINGABETASTE** aus.

1. Wählen Sie **Erstellen** aus, um die Zugriffsrichtlinie zu erstellen.

#### Aufgabe 2: Anmelden bei Forms als Pradeep, um eine Aktivität auszulösen

1. Starten Sie ein neues **InPrivate-Browserfenster**.
2. Stellen Sie eine Verbindung mit [https://forms.microsoft.com](https://forms.microsoft.com)her.
3. Wählen Sie oben rechts auf der Seite „Anmelden“ aus.
4. Melden Sie sich als Pradeep Gupta an.
   - Benutzername = PradeepG@<<<your lab hoster provided domain>>>
   - Kennwort = das Kennwort auf der Registerkarte „Ressourcen“
5. Vergewissern Sie sich, dass Pradeep Zugriff hat und dass Sie eine neue Nachricht erhalten:
   - Ihr Unternehmen überwacht die Nutzung dieser Anwendung.
6. Schließen Sie das InPrivate-Browserfenster.

#### Aufgabe 3: Überprüfen der Aktivität in Defender for Cloud Apps

1. Kehren Sie zum Browser zurück, der Defender for Cloud Apps ausführt.
2. Aktualisieren Sie den Browser, um sicherzustellen, dass die neuesten Daten heruntergeladen werden.
3. Wählen Sie im Menü **Untersuchen** die Option **Aktivitätsprotokoll** aus.
4. Wählen Sie mit **App: Filter** in der Liste **Microsoft Forms** aus.
5. Beachten Sie die Anmeldedatensätze für Pradeep.
