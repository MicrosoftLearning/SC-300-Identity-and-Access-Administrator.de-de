---
lab:
  title: '20: Implementieren der Zugriffsverwaltung für Apps'
  learning path: '03'
  module: Module 03 - Implement Access Management for Apps
---

# Lab 20: Implementieren der Zugriffsverwaltung für Apps

## Labszenario

Ihre Organisation möchte, dass nur bestimmte Benutzer oder Gruppen Zugriff auf Unternehmensanwendungen haben. Sie müssen einer bestimmten Anwendung einen Benutzer zuweisen.

#### Geschätzte Dauer: 5 Minuten

### Übung 1: Konfigurieren einer Unternehmens-App

#### Aufgabe 1: Hinzufügen einer App zu Ihrem Azure AD-Mandanten

1. Melden Sie sich mit einem globalen Administratorkonto bei [https://portal.azure.com](https://portal.azure.com) an.

2. Öffnen Sie das Portal-Menü, und wählen Sie  **Azure Active Directory** aus.

3. Wählen Sie auf der Seite „Azure Active Directory“ unter **Verwalten** die Option **Unternehmensanwendungen** aus.

4. Wählen Sie im Bereich „Unternehmensanwendungen“ die Option **+ Neue Anwendung** aus.

    ![Screenshot der Seite „Unternehmensanwendungen“ mit hervorgehobener Option „Neue Anwendung“](./media/lp3-mod1-new-enterprise-application.png)

5. Geben Sie auf der Seite „Azure AD Katalog durchsuchen (Vorschau)“ im Feld **Anwendung suchen** den Begriff **GitHub** ein.

    ![Screenshot der Seite „Azure AD Katalog durchsuchen (Vorschau)“ mit hervorgehobenem Suchfeld](./media/lp3-mod1-azure-ad-gallery-search.png)

6. Wählen Sie in den Ergebnissen **GitHub Enterprise Cloud – Enterprise Account** aus.

7. Überprüfen Sie die Einstellungen unter **GitHub Enterprise Cloud – Enterprise Account**, und wählen Sie dann **Erstellen** aus.

8. Nachdem der Erstellung werden Sie zur Seite „GitHub Enterprise Cloud – Enterprise Account“ umgeleitet.

#### Aufgabe 2: Zuweisen von Benutzern zu einer App

1. Wählen Sie auf der Seite „GitHub Enterprise Cloud – Enterprise Account“ auf der Seite „Übersicht“ unter **Erste Schritte** die Option **1. Assign users and groups** aus.

2. Alternativ können Sie im Navigationsbereich auf der linken Seite unter **Verwalten** die Option **Benutzer und Gruppen** auswählen.

3. Wählen Sie auf der Seite „Benutzer und Gruppen“ die Menüoption **+ Benutzer/Gruppe hinzufügen** aus.

4. Wählen Sie auf der Seite „Zuweisung hinzufügen“ die Option **Benutzer und Gruppen** aus.

5. Wählen Sie im Bereich „Benutzer und Gruppen“ Ihr Administratorkonto und dann **Auswählen** aus.

    ![Screenshot einer Benutzerkontozuweisung zu einer App mit hervorgehobener Schaltfläche „Auswählen“ ](./media/lp3-mod1-add-app-assignment.png)

6. Wählen Sie **Zuweisen** aus.

