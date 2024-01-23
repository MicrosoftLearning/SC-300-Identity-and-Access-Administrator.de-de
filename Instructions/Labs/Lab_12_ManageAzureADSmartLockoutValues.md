---
lab:
  title: '12: Verwalten der Werte für Azure AD Smart Lockout'
  learning path: '02'
  module: Module 02 - Implement an Authentication and Access Management Solution
---

# Lab 12: Verwalten der Werte für Azure AD Smart Lockout

## Labszenario

Sie müssen die zusätzlichen Kennwortschutzeinstellungen für Ihre Organisation konfigurieren.

#### Geschätzte Dauer: 5 Minuten

### Übung 1: Verwalten der Werte für Azure AD Smart Lockout

#### Aufgabe: Hinzufügen von Smart Lockouts

Die Werte für Azure AD Smart Lockout können auf die Anforderungen Ihrer Organisation abgestimmt werden. Wenn Sie die Smart Lockout-Einstellungen mit spezifischen Werten für Ihre Organisation konfigurieren möchten, benötigen Sie mindestens Azure AD Premium P1-Lizenzen für Ihre Benutzer.

1. Navigieren Sie zu [https://portal.azure.com](https://portal.azure.com), und melden Sie sich mit dem Konto eines globalen Administrators für das Verzeichnis an.

2. Öffnen Sie das Portal-Menü, und wählen Sie  **Azure Active Directory** aus.

3. Wählen Sie auf der Seite „Azure Active Directory“ unter **Verwalten** die Option **Sicherheit** aus.

4. Wählen Sie auf der Seite „Sicherheit“ im linken Navigationsbereich **Authentifizierungsmethoden** aus.

5. Wählen Sie im linken Navigationsbereich die Option **Kennwortschutz** aus.

    ![Screenshot der Seite „Authentifizierungsmethoden“ mit hervorgehobener Auswahl für das Navigieren zur Kennwortauthentifizierung](./media/lp2-mod3-browse-to-password-protection.png)

6. Legen Sie in den Einstellungen für den Kennwortschutz im Feld **Sperrdauer in Sekunden** den Wert auf **120** fest.

7. Wählen Sie neben **Modus** die Option **Erzwungen** aus.

8. Speichern Sie die Änderungen.

    **HINWEIS**: Wenn der Schwellenwert von Smart Lockout ausgelöst wird, wird das Konto gesperrt und die folgende Meldung angezeigt:
    - Ihr Konto wurde vorübergehend gesperrt, um eine unbefugte Nutzung zu verhindern. Versuchen Sie es später noch mal. Wenden Sie sich an Ihren Administrator, wenn das Problem weiterhin besteht.

9. Dies kann getestet werden, indem Sie einen Benutzer in Ihrem Azure AD-Mandanten auswählen, in einem privaten Browser zu <login.microsoftonline.com> navigieren und ein falsches Kennwort eingeben, bis das Konto die Benachrichtigung erhält, dass es gesperrt ist.
