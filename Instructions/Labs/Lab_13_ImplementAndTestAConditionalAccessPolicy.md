---
lab:
  title: "Lab\_3.6: Implementieren und Testen einer Richtlinie für bedingten Zugriff"
  learning path: '02'
  module: Module 02 - Implement an Authentication and Access Management Solution
---

# Lab 3.6: Implementieren und Testen einer Richtlinie für bedingten Zugriff

## Labszenario

Ihre Organisation muss den Benutzerzugriff auf seine internen Anwendungen einschränken können. Sie müssen eine Richtlinie für bedingten Zugriff von Microsoft Entra bereitstellen.

**Hinweis** : Für Richtlinien für bedingten Zugriff können Sie die Sicherheitsstandardwerte deaktivieren, die wichtigsten Punkte, die Sie sich merken sollten, aus der Schulung stammen.  Weitere Informationen zu Den Sicherheitsstandardeinstellungen finden Sie unter diesem Link: <https://docs.microsoft.com/en-us/azure/active-directory/fundamentals/concept-fundamentals-security-defaults>

#### Geschätzte Dauer: 30 Minuten

### Übung 1 – Festlegen einer Richtlinie für bedingten Zugriff, um den Zugriff auf debraB auf Yammer zu blockieren

#### Aufgabe 1 – Bestätigen Sie, dass DebraB Zugriff auf Yammer


1. Starten Sie ein neues InPrivate-Browserfenster.
2. Rufen Sie [https://www.office.com](https://www.office.com) auf. 
3. Melden Sie sich bei Aufforderung als DebraB an:

   | Einstellung | Wert |
   | :--- | :--- |
   | Username | DebraB@ |
   | Kennwort | Geben Sie das Administratorkennwort des Mandanten ein(Verweisen Sie auf die Registerkarte "Laborressourcen", um das Administratorkennwort des Mandanten abzurufen). |
    
4. Wählen Sie auf dem **Sway-Symbol** aus, um zu sehen, dass es ordnungsgemäß geladen wird.

#### Eine Richtlinie für bedingten Zugriff erstellen.

Der bedingte Zugriff von Microsoft Entra ist ein erweitertes Feature von Microsoft Entra ID, mit dem Sie detaillierte Richtlinien angeben können, die steuern, wer auf Ihre Ressourcen zugreifen kann. Mithilfe des bedingten Zugriffs können Sie Ihre Anwendungen schützen, indem Sie den Zugriff der Benutzer auf Grundlage von Faktoren wie Gruppen, Gerätetyp, Standort und Rolle einschränken.

1. Navigieren Sie zum Azure-Portal, und melden Sie sich mit dem Konto eines globalen Administrators für das Verzeichnis an.

2. Öffnen Sie das Portalmenü und wählen Sie dann  **Microsoft Entra ID** aus.

3. Wählen Sie im Menü „Identität“ die Option Schutz aus.

4. Wählen Sie auf dem Blatt „Sicherheit“ im linken Navigationsbereich **Bedingter Zugriff** aus.

5. Klicken Sie auf der **Übersicht (Vorschau)** auf **+Neue Richtlinie** erstellen.

   ![Screenshot des Blatts „Bedingter Zugriff“ mit hervorgehobener Option „Neue Richtlinie“](./media/lp2-mod1-conditional-access-new-policy.png)

6. Geben Sie **im **Feld "Name**" "Block Sway" für "DebraB**" ein.

   **Hinweis** : Mithilfe dieser Benennung können Sie die Richtlinie und deren Funktion schnell erkennen.

7. Wählen Sie unter ZuweisungenBenutzer die Option 0 Benutzer und Gruppen ausgewählt aus.

8. Wählen Sie auf der Registerkarte EinschließenBenutzer und Gruppen auswählen und dann Benutzer und Gruppen aus.

9. Wählen Sie im Bereich „Auswählen“ die Option **Office 365** und dann **Auswählen** aus.

10. Wählen Sie unter **Zielressourcen** die Option **Keine Zielressourcen ausgewählt** aus.

11. Überprüfen Sie, ob **Cloud-Apps** ausgewählt sind, und wählen Sie ****dann "Apps** auswählen" und dann im Abschnitt "Keine"** aus.

12. Suchen Sie im Bereich "Auswählen" nach **Sway, und wählen Sie **Sway**** und dann "Auswählen" aus****.

13. Klicken Sie unter **Gewähren** im Abschnitt **Zugriffssteuerungen** auf **0 Steuerungen ausgewählt**.

14. Wählen Sie im Bereich „Gewähren“ die Option **Zugriff blockieren** und dann **Auswählen** aus.

   Diese Richtlinie wird nur für die Übung konfiguriert und dient zum schnellen Veranschaulichen einer Richtlinie für bedingten Zugriff.

15. Wählen Sie unter **Richtlinie aktivieren** die Option **Ein** und dann **Erstellen** aus.

   ![Screenshot einer neuen Richtlinie für bedingten Zugriff mit hervorgehobenen Richtlinieneinstellungen](./media/lp2-mod3-create-conditional-access-policy.png)

#### Aufgabe 2: Testen der Richtlinie für bedingten Zugriff.

Sie sollten Ihre Richtlinien für bedingten Zugriff testen, um sicherzustellen, dass sie erwartungsgemäß funktionieren.

1. Öffnen Sie eine neue Browserregisterkarte, und navigieren Sie zu [https://sway.office.com](https://sway.office.com).
    - Melden Sie sich bei Aufforderung als DebraB an:

   | Einstellung | Wert |
   | :--- | :--- |
   | Username | DebraB@ |
   | Kennwort | Geben Sie das Administratorkennwort des Mandanten ein(Verweisen Sie auf die Registerkarte "Laborressourcen", um das Administratorkennwort des Mandanten abzurufen). |
     
2. Stellen Sie sicher, dass Sie nicht auf Microsoft Sway zugreifen können.

   ![Screenshot des blockierten Zugriffs auf die Ressource aufgrund einer aktivierten Richtlinie für bedingten Zugriff](./media/lp2-mod3-test-conditional-access-policy.png)

3. Wenn Sie angemeldet sind, schließen Sie die Registerkarte, warten Sie ein bis zwei Minuten, und wiederholen Sie dann den Vorgang.
    
   **Hinweis** : Wenn Ihr Sway automatisch als DebraB angemeldet ist, müssen Sie sich manuell abmelden.  Sie haben Anmeldeinformationen/Zugriff zwischengespeichert.  Sobald Sie sich abmelden und sich anmelden, sollte Ihre Yammer Sitzung den Zugriff verweigern.

4. Schließen Sie die Registerkarte, und kehren Sie zum Blatt „Bedingter Zugriff“ zurück.

5. Wählen Sie das **Block Sway für die DebraB-Richtlinie** aus.

6. Wählen Sie unter **Richtlinie aktivieren** die Option **Aus** und dann **Speichern** aus.

### Übung 2 – Testen von Richtlinien für bedingten Zugriff mit "Was wäre".

#### Video: Verwenden des What-If-Features zum Testen von Richtlinien für bedingten Zugriff

1. Öffnen Sie das Portalmenü und wählen Sie dann  **Microsoft Entra ID** aus.

1. Wählen Sie im Menü „Identität“ die Option Schutz aus.

1. Wählen Sie auf dem Blatt „Sicherheit“ im linken Navigationsbereich **Bedingter Zugriff** aus.

1. Wählen Sie im Navigationsbereich **Datenrichtlinien**.

1. Wählen Sie "Was wäre wenn"** aus**.

1. Wählen Sie unter **Benutzer- oder Workloadidentität** "Kein Benutzer" oder "Dienstprinzipal" aus **.**

1. Wählen Sie **"DebraB** " als Benutzer aus.

1. Cloud-Apps, Aktionen oder Authentifizierungskontext 

1. Wählen Sie **"Was wäre" aus**. Sie erhalten einen Bericht am unteren Rand der Kachel für **Richtlinien, die angewendet** werden, und **Richtlinien, die nicht angewendet** werden.

Auf diese Weise können Sie die Richtlinien und deren Affektivität testen, bevor Sie die Richtlinien aktivieren.

### Konfigurieren von Steuerelementen für Anmeldehäufigkeit mithilfe einer Richtlinie für bedingten Zugriff

#### Konfigurieren Sie im Microsoft Entra Admin Center den bedingten Zugriff.

Im Rahmen der größeren Sicherheitskonfiguration Ihres Unternehmens müssen Sie eine Richtlinie für bedingten Zugriff testen, mit der die Anmeldehäufigkeit gesteuert werden kann.

1. Navigieren Sie zum Azure-Portal, und melden Sie sich mit dem Konto eines globalen Administrators für das Verzeichnis an.

2. Öffnen Sie das Portalmenü und wählen Sie dann  **Microsoft Entra ID** aus.

3. Wählen Sie im Menü „Identität“ die Option Schutz aus.

4. Wählen Sie auf dem Blatt „Sicherheit“ im linken Navigationsbereich **Bedingter Zugriff** aus.

5. Wählen Sie im Menü „Sicherungsrichtlinie“ im Dropdownmenü **Sicherungsrichtlinie auswählen** die Option **Neu erstellen** aus.

   ![Screenshot des Blatts „Bedingter Zugriff“ mit hervorgehobener Option „Neue Richtlinie“](./media/lp2-mod1-conditional-access-new-policy.png)

6. Geben Sie im Feld **Name** die Bezeichnung **Anmeldehäufigkeit** ein.

7. Wählen Sie unter ZuweisungenBenutzer die Option 0 Benutzer und Gruppen ausgewählt aus.

8. Wählen Sie auf der Registerkarte EinschließenBenutzer und Gruppen auswählen und dann Benutzer und Gruppen aus.

9. Wählen Sie im Bereich „Auswählen“ Ihr Administratorkonto und dann die Option Auswählen aus.

10. Wählen Sie **Cloud-Apps oder -aktionen** aus.

11. Vergewissern Sie sich, dass **Cloud-Apps** ausgewählt ist, und wählen Sie dann **Apps auswählen** aus.

12. Wählen Sie im Bereich „Auswählen“ die Option **Office 365** und dann **Auswählen** aus.

13. Wählen Sie unter **Zugriffssteuerungen** die Option **Sitzung** aus.

14. Wählen Sie im Bereich Sitzung die Option Anmeldehäufigkeit aus.

15. Geben Sie im Wertfeld die Zahl **30** ein.

16. Wählen Sie das Menü „Einheiten“, dann **Tage** und anschließend **Auswählen** aus.

17. Wählen Sie unter **Richtlinie aktivieren** die Option **Nur Bericht** und dann **Erstellen** aus.

   ![Screenshot einer neuen Richtlinie für bedingten Zugriff mit hervorgehobenen Richtlinieneinstellungen](./media/lp2-mod3-create-session-conditional-access-policy.png)

   Der reine Berichtsmodus ist ein neuer Status von Richtlinien für bedingten Zugriff, mit dem Administratoren die Auswirkungen von Richtlinien für bedingten Zugriff auswerten können, bevor sie die jeweiligen Richtlinien in ihrer Umgebung aktivieren. Durch die Einführung des reinen Berichtsmodus ergeben sich die folgenden Vorteile:
    
- Richtlinien für bedingten Zugriff können im reinen Berichtsmodus aktiviert werden.
- Bei der Anmeldung werden Richtlinien im reinen Berichtsmodus ausgewertet, aber nicht erzwungen.
- Die Ergebnisse werden auf den Registerkarten Bedingter Zugriff und Nur melden der Anmeldeprotokolldetails protokolliert.
- Kunden mit einem Azure Monitor-Abonnement können die Auswirkungen ihrer Richtlinien für bedingten Zugriff mithilfe der Arbeitsmappe für Erkenntnisse zum bedingten Zugriff überwachen.
