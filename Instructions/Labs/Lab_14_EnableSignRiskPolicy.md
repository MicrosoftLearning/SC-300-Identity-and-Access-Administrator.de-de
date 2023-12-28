---
lab:
  title: Aktivieren von Anmelde- und Benutzerrisikorichtlinien
  learning path: '02'
  module: Module 02 - Implement an Authentication and Access Management Solution
---

# Übung: Aktivieren von Anmelde- und Benutzerrisikorichtlinien

## Labszenario

Als zusätzliche Sicherheitsebene müssen Sie die Anmelde- und Benutzerrisikorichtlinien Ihrer Microsoft Entra-Organisation aktivieren und konfigurieren.

#### Geschätzte Dauer: 10 Minuten


### Übung zum Aktivieren der Anmelderisiko-Richtlinie

#### Aufgabe 1 – Konfigurieren der Richtlinie

1. Melden Sie sich mit dem globalen Administratorkonto beim Azure-Portal an.

2. Öffnen Sie das Portalmenü und wählen Sie dann  **Microsoft Entra ID** aus.

3. Wählen Sie im linken Menü unter **"Identität"** die Option "Schutz **" aus**.

4. Wählen Sie auf dem Blatt „Sicherheit“ im linken Navigationsbereich **Identity Protection** aus.

5. Wählen Sie auf dem Blatt „Identity Protection“ im linken Navigationsbereich „Benutzerrisiko-Richtlinie“ aus.

    ![Screenshot der Seite „Benutzerrisiko-Richtlinie“ mit hervorgehobenem Auswahlpfad](./media/lp2-mod4-browse-to-identity-protection.png)

6. Wählen Sie unter **Zuweisungen** die Option **Alle Benutzer** aus, und überprüfen Sie die verfügbaren Optionen.

7. Zur Auswahl stehen **Alle Benutzer** oder **Einzelne Benutzer und Gruppen auswählen**, falls Sie den Rollout einschränken möchten.

8. Außerdem können Sie festlegen, dass Benutzer von der Richtlinie ausgeschlossen werden sollen.

9. Wählen Sie unter **Benutzerrisiko** die Option **Niedrig und darüber** aus.

10. Wählen Sie im Bereich „Benutzerrisiko“ die Option **Hoch** aus, und klicken Sie dann auf **Fertig**.

11. Wählen Sie unter **Steuerungen** > **Zugriff** die Option **Zugriff blockieren** aus.

12. Überprüfen Sie die verfügbaren Optionen im Zugriffsbereich.

    Die Empfehlung von Microsoft lautet, den Zugriff zuzulassen und eine Kennwortänderung anzufordern.

13. Aktivieren Sie das Kontrollkästchen **Kennwortänderung anfordern**, und klicken Sie dann auf **Fertig**.

14. Wählen Sie unter **Richtlinie erzwingen** die Option **Ein** aus, und klicken Sie dann auf **Speichern**.

#### Aktivieren der Anmelderisiko-Richtlinie

1. Wählen Sie auf dem Blatt „Identity Protection“ im linken Navigationsbereich **Anmelderisiko-Richtlinie** aus.

2. Wie die Benutzerrisiko-Richtlinie kann die Anmelderisiko-Richtlinie Benutzern und Gruppen zugewiesen werden und gestattet Ihnen das Ausschließen von Benutzern aus der Richtlinie.

3. Wählen Sie unter **Anmelderisiko** die Option **Mittel und darüber** aus.

4. Wählen Sie im Bereich „Anmelderisiko“ die Option **Hoch** aus, und klicken Sie dann auf **Fertig**.

5. Wählen Sie unter **Steuerungen** > **Zugriff** die Option **Zugriff blockieren** aus.

6. Aktivieren Sie das Kontrollkästchen **Multi-Factor Authentication erforderlich**, und wählen Sie dann **Fertig** aus.

7. Wählen Sie unter **Richtlinie erzwingen** die Option **Ein** aus, und klicken Sie dann auf **Speichern**.
