---
lab:
  title: "15: Konfigurieren einer Registrierungsrichtlinie für die Multi-Faktor-Authentifizierung von Azure\_AD"
  learning path: '02'
  module: Module 02 - Implement an Authentication and Access Management Solution
---

# Lab 15: Konfigurieren einer Registrierungsrichtlinie für die Multi-Faktor-Authentifizierung von Azure AD

## Labszenario

Mit der Multi-Faktor-Authentifizierung von Azure AD können Sie über die Verwendung eines Benutzernamens und Kennworts hinaus Ihre Identität verifizieren. Sie stellt eine zweite Sicherheitsebene für Benutzeranmeldungen dar. Damit Benutzer auf MFA-Aufforderungen reagieren können, müssen sie sich zuerst bei Azure AD Multi-Factor Authentication registrieren. Sie müssen die MFA-Registrierungsrichtlinie Ihrer Azure AD-Organisation so konfigurieren, dass sie allen Benutzern zugewiesen wird.

#### Geschätzte Dauer: 10 Minuten

### Übung 1: Einrichten der MFA-Registrierungsrichtlinie

#### Aufgabe 1: Richtlinienkonfiguration

1. Melden Sie sich mit einem globalen Administratorkonto bei [https://portal.azure.com]( https://portal.azure.com) an.

2. Öffnen Sie das Portal-Menü, und wählen Sie  **Azure Active Directory** aus.

3. Wählen Sie auf der Seite „Azure Active Directory“ unter **Verwalten** die Option **Sicherheit** aus.

4. Wählen Sie auf der Seite „Sicherheit“ im linken Navigationsbereich **Identity Protection** aus.

5. Wählen Sie auf der Seite „Identity Protection“ im linken Navigationsbereich unter **Schützen** die Option **MFA-Registrierungsrichtlinie** aus.

    ![Screenshot der Seite „MFA-Registrierungsrichtlinie“ mit hervorgehobenem Auswahlpfad](./media/lp2-mod4-browse-to-mfa-registration-policy.png)

6. Unter **Zuweisungen**

7. Wählen Sie unter **Zuweisungen** die Option **Alle Benutzer** aus, und überprüfen Sie die verfügbaren Optionen.

8. Zur Auswahl stehen **Alle Benutzer** oder **Einzelne Benutzer und Gruppen auswählen**, falls Sie den Rollout einschränken möchten.

9. Außerdem können Sie festlegen, dass Benutzer von der Richtlinie ausgeschlossen werden sollen.

10. Beachten Sie, dass unter **Steuerungen** die Option **Azure AD MFA-Registrierung als erforderlich festlegen** ausgewählt ist und nicht geändert werden kann.


#### Aufgabe 2: Konfigurieren der Azure AD Identity Protection-Richtlinie für die MFA-Registrierung

**Hinweis**: Für Azure AD Identity Protection ist eine Azure AD Premium P2-Lizenz erforderlich. 

1. Navigieren Sie im Azure-Portal in der Suchleiste zu **Azure AD Identity Protection**.

1. Wählen Sie unter **Schützen** im Menü **MFA-Registrierungsrichtlinie** aus.

1. Wählen Sie in **Zuweisungen** unter „Benutzer“ den Eintrag **Alle Benutzer** aus, und wählen Sie dann einen Benutzer aus, für den die MFA gelten soll.

1. Ändern Sie **Richtlinienerzwingung** von **Deaktiviert** in **Aktiviert**.

1. Wählen Sie **Speichern** aus.

Auf diese Weise muss der Benutzer die MFA-Registrierung beim nächsten Anmeldeversuch abschließen.

1. Navigieren Sie in einem privaten Browser zu `https://login.microsoftonline.com`. Geben Sie einen Benutzernamen und ein Kennwort ein.  Beachten Sie die zusätzlichen Sicherheitsinformationen, die der Benutzer eingeben muss.
