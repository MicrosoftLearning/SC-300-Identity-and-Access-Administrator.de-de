---
lab:
  title: "22: Erstellen und Verwalten eines Ressourcenkatalogs in der Azure\_AD-Berechtigungsverwaltung"
  learning path: '04'
  module: Module 04 - Plan and Implement and Identity Governance Strategy
---

# Lab 22: Erstellen und Verwalten eines Ressourcenkatalogs in der Azure AD-Berechtigungsverwaltung

## Labszenario

Ein Katalog ist ein Container für Ressourcen und Zugriffspakete. Sie erstellen einen Katalog, wenn Sie zugehörige Ressourcen und Zugriffspakete gruppieren möchten. Der Benutzer, der den Katalog erstellt, ist der erste Katalogbesitzer. Ein Katalogbesitzer kann weitere Katalogbesitzer hinzufügen. Sie müssen einen Katalog in Ihrer Organisation erstellen und konfigurieren.

#### Geschätzte Dauer: 15 Minuten

### Übung 1: Aufbauen von Ressourcen in der Berechtigungsverwaltung

#### Aufgabe 1: Erstellen eines Katalogs

1. Melden Sie sich mit einem globalen Administratorkonto bei [https://portal.azure.com](https://portal.azure.com) an.

    **Wichtig**: Um die Azure AD-Nutzungsbedingungen verwenden und konfigurieren zu können, benötigen Sie Folgendes:
    - Eines der folgenden Abonnements: Azure AD Premium P1, P2, EMS E3 oder EMS E5.
    - Sollten Sie über keines dieser Abonnements verfügen, können Sie Azure AD Premium beziehen oder die Azure AD Premium-Testversion aktivieren.
    - Eines der folgenden Administratorkonten für das Verzeichnis, das Sie konfigurieren möchten:
        - Globaler Administrator
        - Sicherheitsadministrator
        - Administrator für den bedingten Zugriff

2. Öffnen Sie **Azure Active Directory**, und wählen Sie  **Identity Governance** aus.

3. Wählen Sie im Menü links unter **Berechtigungsverwaltung** die Option **Kataloge** aus.

4. Wählen Sie im oberen Menü die Option **+ Neuer Katalog** aus.

    ![Screenshot der Seite „Kataloge“ in Identity Governance mit hervorgehobenem Menü „Neuer Katalog“ ](./media/lp4-mod1-identity-governance-new-catalog.png)

5. Geben Sie im Bereich „Neuer Katalog“ im Feld **Name** die Bezeichnung **Marketing** ein.

6. Geben Sie im Feld **Beschreibung** die Angabe **Für Benutzer der Marketingabteilung** ein. Benutzern werden diese Informationen in den Details eines Zugriffspakets angezeigt.

7. Wählen Sie unter **Aktiviert** die Option „Nein“ aus.

- - Die Option **Für externe Benutzer aktiviert** ermöglicht Benutzern in ausgewählten externen Verzeichnissen das Anfordern von Zugriffspaketen in diesem Katalog. An dieser Einstellung werden keine Änderungen vorgenommen.

9. Sie können den Katalog für die sofortige Verwendung aktivieren oder deaktivieren, wenn Sie ihn bis zur beabsichtigten Verwendung stagen oder als nicht verfügbar belassen möchten. Für diese Übung muss der Katalog nicht aktiviert werden.

    ![Screenshot des Bereichs „Neuer Katalog“ mit hervorgehobenen Optionen für „Name“, „Beschreibung“, „Aktiviert“ und „Erstellen“](./media/lp4-mod1-new-catalog-marketing.png)

10. Wählen Sie „Erstellen“ aus.

#### Aufgabe 2: Hinzufügen von Ressourcen zu einem Katalog

Um Ressourcen in ein Zugriffspaket einschließen zu können, müssen die Ressourcen in einem Katalog vorhanden sein. Bei den Typen von Ressourcen, die Sie hinzufügen können, handelt es sich um Gruppen, Anwendungen und SharePoint Online-Websites. Die Gruppen können in der Cloud erstellte Microsoft 365-Gruppen oder in der Cloud erstellte Azure AD-Sicherheitsgruppen sein. Die Anwendungen können Azure AD-Unternehmensanwendungen sein, einschließlich SaaS-Anwendungen und Ihrer eigenen Anwendungen, die mit Azure AD verbunden sind. Die Websites können SharePoint Online-Websites oder SharePoint Online-Websitesammlungen sein.

1. Wählen Sie auf der Seite „Identity Governance“ bei Bedarf die Option **Kataloge** aus.

2. Wählen Sie in der Liste **Kataloge** den Eintrag **Marketing** aus.

3. Wählen Sie im linken Navigationsbereich unter **Verwalten** die Option **Ressourcen** aus.

4. Wählen Sie im Menü die Option **+ Ressourcen hinzufügen** aus.

5. Überprüfen Sie auf der Seite „Ressourcen zum Katalog hinzufügen“ die verfügbaren Optionen.  Fügen Sie die folgenden Elemente hinzu:

   | Ressourcentyp | Wert |
   | :------------- | :---------- |
   |  **Gruppen und Teams** | Einzelhandel |
   |  **Anwendungen** | Feld |
   |  **Anwendungen** | Salesforce |
   |  **SharePoint-Websites** | Marke SharePoint <<<Auswahl aus Ihrer Liste der verfügbaren SharePoint-Websites |

6. Sie verfügen möglicherweise nicht über Ressourcen in Gruppen und Teams, Anwendungen oder SharePoint-Websites. Wählen Sie eine beliebige Ressourcenkategorie und dann eine Ressource aus dieser Kategorie aus.

7. Für diese Übung kann eine beliebige verfügbare Ressource ausgewählt werden.

    ![Hinzufügen von Ressourcen zu einem Katalog](./media/catalog-add-resources.png)

8. Wählen Sie abschließend **Hinzufügen** aus. Diese Ressourcen können jetzt in Zugriffspakete im Katalog aufgenommen werden.

#### Aufgabe 3: Hinzufügen weiterer Katalogbesitzer

Der Benutzer, der einen Katalog erstellt hat, ist der erste Katalogbesitzer. Wenn Sie die Verwaltung eines Katalogs delegieren möchten, fügen Sie der Rolle „Katalogbesitzer“ Benutzer hinzu. Dadurch können die Aufgaben der Katalogverwaltung gemeinsam wahrgenommen werden.

1. Navigieren Sie ggf. im Azure-Portal zu **Azure Active Directory**, wählen Sie **Identity Governance** und dann **Kataloge** aus, und wählen Sie anschließend **Marketing** aus.

2. Wählen Sie auf der Seite „Marketingkatalog“ im linken Navigationsmenü **Rollen und Administratoren** aus.

    ![Screenshot der Seite „Rollen und Administratoren“ für den Katalog „Marketing“](./media/lp4-mod1-catalog-roles-and-admins.png)

3. Überprüfen Sie die verfügbaren Rollen im oberen Menü, und wählen Sie dann **+ Add catalog owner** aus.

4. Wählen Sie im Bereich „Mitglieder auswählen“ **Adele Vance** und dann **Auswählen** aus.

5. Überprüfen Sie die neu hinzugefügte Rolle in der Liste „Rollen und Administratoren“.

#### Aufgabe 4: Bearbeiten eines Katalogs

Sie können den Namen und die Beschreibung eines Katalogs bearbeiten. Benutzern werden diese Informationen in den Details eines Zugriffspakets angezeigt.

1. Wählen Sie auf der Seite „Marketing“ im linken Navigationsbereich die Option **Übersicht** aus.

2. Wählen Sie im oberen Menü die Option **Bearbeiten** aus.

3. Überprüfen Sie die Einstellung, und wählen Sie unter **Eigenschaften** > **Aktiviert** die Option **Ja** aus.

    ![Screenshot der aktivierten Eigenschaften](./media/lp4-mod1-edit-marketing-catalog.png)

4. Wählen Sie **Speichern** aus.

#### Aufgabe 5: Erstellen von Zugriffsüberprüfungen für Gastbenutzer

1. Zugriffsüberprüfungen können den Zugriffslebenszyklus verwalten.Azure AD Identity Governance bietet ein Übersichtsdashboard mit dem Status von Zugriffsüberprüfungen. Wählen Sie **Zugriffsüberprüfungen** im Menü **Identity Governance** aus.

1. Im Menü „Zugriffsüberprüfung“ können Sie **Zugriffsüberprüfungen** auswählen, um eine Zugriffsüberprüfung für Gastbenutzer zu konfigurieren.  Sie wählen **+ Neue Zugriffsüberprüfung** aus, um ihre Gastbenutzerzugriffsüberprüfung zu erstellen.  Die Kachel wird geöffnet, um die Zugriffsüberprüfung für Gastbenutzer zu konfigurieren.

1. Wählen Sie **Teams + Gruppen** für **Zu überprüfende Elemente auswählen**.

1. Wählen Sie unter **Select review scope** die Option **All Microsoft 365 groups with guest users** aus.

1. Wählen Sie unter **Select user scope** die Option **Nur Gastbenutzer** aus.

1. Wählen Sie **Weiter: Überprüfungen** aus.

1. Auf der nächsten Kachel konfigurieren Sie, wer den Zugriff überprüft und genehmigt, wie oft der Zugriff überprüft wird und wann der Zugriff abläuft.

1. Wählen Sie unter **Prüfer auswählen** die Option **Gruppenbesitzer** als Prüfer aus. **Hinweis**: Gastbenutzern sollte es nicht erlaubt sein, ihren eigenen Zugriff zu überprüfen; dies ist eine bewährte Praxis für Identity Governance.

1. Geben Sie eine **Dauer (in Tagen)** ein, der Standardwert ist 3, wählen Sie eine **Häufigkeit der Überprüfung** und ein **Startdatum** für die Überprüfung aus.

1. Wählen Sie **Weiter: Einstellungen** aus, und konfigurieren Sie die Einstellungen dafür, wie die Überprüfung stattfindet und was geschieht, wenn der Gastbenutzer antwortet oder nicht antwortet.  Es empfiehlt sich, **Ergebnisse automatisch auf Ressource anwenden** zu aktivieren und **Zugriff entfernen** für **Wenn Prüfer nicht reagieren** auszuwählen. 

1. Wählen Sie **Weiter: Überprüfen + erstellen** und dann **Erstellen** aus, um die neue **Zugriffsüberprüfung** zu erstellen.


#### Aufgabe 6: Löschen eines Katalogs

Sie können einen Katalog nur löschen, wenn er keine Zugriffspakete enthält.

1. Wählen Sie auf der Seite „Übersicht“ des Katalogs „Marketing“ im oberen Menü die Option „Löschen“ aus.

2. Überprüfen Sie die Informationen im Dialogfeld „Löschen“, und wählen Sie dann **Nein** aus.

    **Hinweis**: Wir behalten den Katalog für die Verwendung in der nächsten Übung bei.
