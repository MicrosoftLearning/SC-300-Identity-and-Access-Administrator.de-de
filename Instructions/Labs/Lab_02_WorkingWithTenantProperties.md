---
lab:
  title: '02: Arbeiten mit Mandanteneigenschaften'
  learning path: '01'
  module: Module 01 - Implement an Identity Management Solution
---

# Lab 02: Arbeiten mit Mandanteneigenschaften

## Labszenario

Sie müssen die verschiedenen Eigenschaften identifizieren und aktualisieren, die Ihrem Mandanten zugeordnet sind.

#### Geschätzte Dauer: 15 Minuten

### Übung 1: Erstellen einer benutzerdefinierten Subdomäne 

#### Aufgabe 1: Erstellen eines benutzerdefinierten Subdomänennamens

1. Navigieren Sie zu [https://portal.azure.com](https://portal.azure.com), und melden Sie sich mit dem Konto eines globalen Administrators für das Verzeichnis an.

1. Wählen Sie das Hamburger-Menüsymbol **Portalmenü anzeigen** und dann **Azure Active Directory** aus.

    ![Menü im Azure-Portal mit ausgewählter Option „Azure Active Directory“](./media/azure-portal-menu-aad.png)

1. Wählen Sie im Abschnitt **Verwalten** von **Azure AD** die Option **Benutzerdefinierte Domänennamen** aus.

1. Wählen Sie **Benutzerdefinierte Domäne hinzufügen**.

1. Erstellen Sie im Feld **Benutzerdefinierter Domänenname** eine benutzerdefinierte Unterdomäne für den Labmandanten, indem Sie **sales** dem Domänennamen **onmicrosoft.com** voranstellen.  Das Format sieht in etwa wie folgt aus:

    ```
    sales.labtenant.onmicrosoft.com
    ```

1. Wählen Sie **Domäne hinzufügen** aus, um die Unterdomäne hinzuzufügen.


### Übung 2: Ändern des Anzeigenamens des Mandanten

#### Aufgabe 1: Festlegen des Mandantennamens und des technischen Kontakts

1. Wählen Sie in Azure Active Directory im linken Navigationsbereich im Abschnitt **Verwalten** die Option **Eigenschaften** aus.

1. Ändern Sie die Mandanteneigenschaften für **Name** und **Technischer Kontakt** im Dialogfeld.

    | **Einstellung** | **Wert** |
    | :--- | :--- |
    | Name | Contoso Marketing |
    | Technischer Kontakt | `your Global admin account` |

1. Wählen Sie **Speichern** aus, um die Mandanteneigenschaften zu aktualisieren.

   **Sie werden feststellen, dass sich der Name unmittelbar nach Abschluss des Speichervorgangs ändert.**

#### Aufgabe 2: Überprüfen des Landes oder der Region und anderer Werte, die Ihrem Mandanten zugeordnet sind

1. Wählen Sie auf der Seite **Azure Active Directory** im Abschnitt „Verwalten“ die Option **Eigenschaften** aus.

2. Suchen Sie unter **Mandanteneigenschaften** nach **Land oder Region**, und überprüfen Sie die Informationen.

    **WICHTIG**: Das Land oder die Region wird beim Erstellen des Mandanten angegeben. Diese Einstellung kann später nicht mehr geändert werden.

3. Suchen Sie auf der Seite **Eigenschaften** unter **Mandanteneigenschaften** den **Standort**, und überprüfen Sie die Informationen.

    ![Screenshot der Seite mit den Azure Active Directory-Eigenschaften mit hervorgehobenen Einstellungen „Land oder Region“ und „Standort“](./media/azure-active-directory-properties-country-location.png)

#### Aufgabe 3: Suchen der Mandanten-ID

Azure-Abonnements weisen eine Vertrauensstellung mit Azure Active Directory (Azure AD) auf. Azure AD gilt als vertrauenswürdig für die Authentifizierung von Benutzern, Diensten und Geräten für das Abonnement. Jedem Abonnement ist eine Mandanten-ID zugeordnet. Es gibt verschiedene Möglichkeiten, die Mandanten-ID für Ihr Abonnement zu ermitteln.

1. Wählen Sie auf der Seite **Azure Active Directory** im Abschnitt „Verwalten“ die Option **Eigenschaften** aus.

2. Suchen Sie unter **Mandanteneigenschaften** die **Mandanten-ID**. Dies ist Ihr eindeutiger Mandantenbezeichner.

    ![Screenshot der Seite „Mandanteneigenschaften“ mit hervorgehobenem Feld „Mandanten-ID“](./media/portal-tenant-id.png)

### Übung 3: Festlegen Ihrer Datenschutzinformationen

#### Aufgabe 1: Hinzufügen Ihrer Datenschutzinformationen zu Azure AD, einschließlich der URL für den globalen Datenschutzkontakt und der Datenschutzerklärung

Microsoft empfiehlt Ihnen dringend, sowohl die Kontaktdaten Ihres globalen Ansprechpartners für den Datenschutz als auch die Datenschutzerklärung Ihrer Organisation hinzuzufügen, damit Ihre internen Mitarbeiter und externen Gäste Ihre Richtlinien lesen können. Da Datenschutzerklärungen individuell erstellt werden und auf das jeweilige Unternehmen zugeschnitten sind, wird dringend empfohlen, zu diesem Sachverhalt einen Anwalt hinzuziehen.

   **HINWEIS**: Informationen zum Anzeigen oder Löschen personenbezogener Daten finden Sie unter [https://docs.microsoft.com/microsoft-365/compliance/gdpr-dsr-azure](https://docs.microsoft.com/microsoft-365/compliance/gdpr-dsr-azure). Weitere Informationen zur DSGVO finden Sie unter [https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

Sie fügen die Datenschutzinformationen Ihrer Organisation im Bereich  **Eigenschaften** von Azure AD hinzu. So greifen Sie auf den Bereich „Eigenschaften“ zu und fügen Ihre Datenschutzinformationen hinzu

1. Wählen Sie auf der Seite **Azure Active Directory** im Abschnitt „Verwalten“ die Option **Eigenschaften** aus.

    ![Screenshot der Mandanteneigenschaften mit hervorgehobenen Kästchen für den technischen Kontakt, den globalen Kontakt und die Datenschutzerklärung](./media/properties-area.png)

2. Fügen Sie Ihre Datenschutzinformationen für Ihre Mitarbeiter hinzu:

- **Globaler Datenschutzkontakt** - `AllanD@` **Ihre Azure-Lab-Domäne**
     - Allan Deyoung ist ein integrierter Benutzer in Ihrem Azure-Labmandanten, der als IT-Administrator arbeitet. Wir verwenden ihn als Datenschutzkontakt.
     - Diese Person wird von Microsoft auch kontaktiert, wenn ein Verstoß gegen die Datenschutzbestimmungen vorliegt. Wenn keine Person hier aufgeführt wird, kontaktiert Microsoft Ihre globalen Administratoren.

- **URL zur Datenschutzerklärung** -  <https://github.com/MicrosoftLearning/SC-300-Identity-and-Access-Administrator/blob/master/Allfiles/Labs/Lab2/SC-300-Lab_ContosoPrivacySample.pdf>

     - Die PDF-Beispieldatei „Datenschutz“ wird in Ihrem Labverzeichnis bereitgestellt.
     – Geben Sie den Link zum Dokument Ihrer Organisation an, in dem beschrieben wird, wie Ihre Organisation die Daten von internen und externen Gästen schützt.

    **WICHTIG**: Wenn Sie weder Ihre eigene Datenschutzerklärung noch Ihren Datenschutzkontakt einfügen, sehen Ihre externen Gäste im Feld „Berechtigungen überprüfen“ einen Text, der besagt:  **<Name Ihrer Organisation>\>** hat keine Links zu den Bestimmungen zu Ihrer Überprüfung angegeben. Diese Meldung wird beispielsweise einem Gastbenutzer angezeigt, wenn er über die B2B-Zusammenarbeit eine Einladung für den Zugang zu einer Organisation erhält.

    ![Das Feld „B2B Collaboration-Überprüfungsberechtigungen“ mit Nachricht](./media/active-directory-no-privacy-statement-or-contact.png)

3. Wählen Sie **Speichern** aus.

#### Aufgabe 2: Überprüfen Ihrer Datenschutzerklärung

1. Kehren Sie zur Azure-Startseite – Dashboard zurück.
2. Wählen Sie oben rechts in der Benutzeroberfläche Ihren Benutzernamen aus.
3. Wählen Sie im Dropdownmenü **Konto anzeigen** aus.

     **Im Browser wird automatisch eine neue Browserregisterkarte geöffnet.**

4. Wählen Sie links im Menü die Option **Einstellungen und Datenschutz** aus.
5. Wählen Sie **Datenschutz** aus.
6. Wählen Sie unter **Organization's notice** den Eintrag **Anzeigen** neben der Datenschutzerklärung der Contoso Marketing-Organisation aus.

     **Eine neue Browserregisterkarte wird mit der PDF-Datenschutzerklärungsdatei geöffnet, die Sie mit der Anzeige verknüpft haben.**

7. Überprüfen Sie die Datenschutzerklärung.
8. Schließen Sie die Browserregisterkarte mit der darin angezeigten PDF-Datei.
9. Schließen Sie die Browserregisterkarte, auf der die **Mein Konto**-Einträge angezeigt werden.
