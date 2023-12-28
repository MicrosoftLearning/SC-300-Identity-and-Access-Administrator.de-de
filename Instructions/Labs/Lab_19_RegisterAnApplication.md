---
lab:
  title: '19: Registrieren einer Anwendung'
  learning path: '03'
  module: Module 03 - Implement Access Management for Apps
---

# Lab 19: Registrieren einer Anwendung

#### Geschätzte Dauer: 30 Minuten

### Übung 1: Registrieren einer Anwendung

#### Aufgabe 1: App-Registrierung

Beim Registrieren Ihrer Anwendung wird eine Vertrauensstellung zwischen Ihrer App und Microsoft Identity Platform erstellt. Die Vertrauensstellung ist unidirektional: Ihre App vertraut Microsoft Identity Platform und nicht umgekehrt.

1. Melden Sie sich bei [https://entra.microsoft.com](https://entra.microsoft.com)  mit einem globalen Administratorkonto an.

2. Öffnen Sie das Portalmenü, und wählen Sie dann  **Microsoft Entra ID** aus.

3. Wählen Sie im Menü **Identität** unter **Anwendungen** **App-Registrierungen** aus.

4. Wählen Sie auf der Seite **App-Registrierungen** im Menü die Option **+ Neue Registrierung** aus.

5. Registrieren Sie auf dem Blatt **Anwendung registrieren** unter Verwendung der Standardwerte eine App mit dem Namen **Demo-App**. Der Umleitungs-URI muss nicht eingegeben werden.

    ![Screenshot mit der Seite „Anwendung registrieren“, wobei der Name und die Standardeinstellungen hervorgehoben sind](./media/lp3-mod3-register-an-application.png)

6. Wenn Sie fertig sind, werden Sie zur Seite **Demo-App** weitergeleitet.


#### Aufgabe 2: Konfigurieren von Plattformeinstellungen

Die Einstellungen für jeden Anwendungstyp (einschließlich Umleitungs-URIs) werden unter  **Plattformkonfigurationen**  im Azure-Portal konfiguriert. Bei einigen Plattformen (z. B.  **Web** - und  **Single-Page-Anwendungen**) müssen Sie manuell einen Umleitungs-URI angeben. Bei anderen Plattformen (z. B. mobile Anwendungen und Desktopanwendungen) stehen Umleitungs-URIs zur Auswahl, die beim Konfigurieren anderer Einstellungen für Sie generiert wurden.

So konfigurieren Sie Anwendungseinstellungen auf Basis der Zielplattform oder des Zielgeräts

Sie können Umleitungs-URIs für Ihre registrierten Anwendungen hinzufügen und ändern, indem Sie deren Plattformeinstellungen konfigurieren.

1. Wählen Sie im Microsoft Entra Admin Center unter  **App-Registrierungen** Ihre Anwendung aus.

2. Wählen Sie unter  **Verwalten** die Option  **Authentifizierung** aus.

3. Wählen Sie unter  **Plattformkonfigurationen** die Option  **+ Plattform hinzufügen** aus.

4. Wählen Sie unter  **Plattformen konfigurieren** die Kachel für Ihren Anwendungstyp (Plattform) aus, um die Einstellungen zu konfigurieren.

    ![Screenshot des Plattformkonfigurationsbereichs im Azure-Portal](./media/configure-platforms.png)

    | Plattform| Konfigurationseinstellungen|
    | :--- | :--- |
    | Web| Geben Sie einen  **Umleitungs-URI**  für Ihre App ein. Dabei handelt es sich um die Adresse, an die Microsoft Identity Platform den Client von Benutzer*innen umleitet und nach der Authentifizierung die Sicherheitstoken sendet. Wählen Sie diese Plattform für Standardwebanwendungen aus, die auf einem Server ausgeführt werden.|
    | Einseitige Anwendung| Geben Sie einen  **Umleitungs-URI**  für Ihre App ein. Dabei handelt es sich um die Adresse, an die Microsoft Identity Platform den Client von Benutzer*innen umleitet und nach der Authentifizierung die Sicherheitstoken sendet. Wählen Sie diese Plattform aus, wenn Sie eine clientseitige Web-App in JavaScript oder mit einem Framework wie Angular, Vue.js, React.js oder Blazor WebAssembly erstellen.|
    | iOS/macOS| Geben Sie die  **Bundle-ID** der App ein, die Sie in XCode in  *Info.plist*  oder in den Buildeinstellungen finden. Wenn Sie eine Paket-ID angeben, wird ein Umleitungs-URI für Sie generiert.|
    | Android| Geben Sie den  **Paketnamen** der App ein, den Sie in der Datei „AndroidManifest.xml“ finden. Generieren Sie den  **Signaturhash**, und geben Sie ihn ein. Bei der Angabe dieser Einstellungen wird ein Umleitungs-URI für Sie generiert.|
    | Mobile Anwendungen und Desktopanwendungen| Wählen Sie einen der  **vorgeschlagenen Umleitungs-URIs**  aus, oder geben Sie einen  **benutzerdefinierten Umleitungs-URI** an. Empfehlung für Desktopanwendungen: [https://login.microsoftonline.com/common/oauth2/nativeclient](https://login.microsoftonline.com/common/oauth2/nativeclient). Wählen Sie diese Plattform für mobile Anwendungen aus, die nicht die neueste Microsoft-Authentifizierungsbibliothek (Microsoft Authentication Library, MSAL) verwenden oder keinen Broker einsetzen. Wählen Sie diese Plattform auch für Desktopanwendungen aus.|

5. Wählen Sie  **Konfigurieren**  aus, um die Plattformkonfiguration abzuschließen.

#### Aufgabe 3: Hinzufügen von Anmeldeinformationen, Zertifikaten und geheimen Clientschlüsseln

Anmeldeinformationen werden von vertraulichen Clientanwendungen verwendet, die auf eine Web-API zugreifen. Beispiele für vertrauliche Clients sind Web-Apps, andere Web-APIs oder Anwendungen des Typs „Dienst“ oder „Daemon“. Mit den Anmeldeinformationen kann sich Ihre Anwendung selbst authentifizieren und benötigt zur Laufzeit keine Interaktion durch einen Benutzer.

Sie können Ihrer vertraulichen Client-App-Registrierung sowohl Zertifikate als auch geheime Clientschlüssel (Zeichenfolge) als Anmeldeinformationen hinzufügen.

![Screenshot des Azure-Portals mit dem Bereich „Zertifikate und Geheimnisse“ in der App-Registrierung](./media/portal-05-app-reg-04-credentials.png)

    **Note**: Sometimes called a *public key*, certificates are the recommended credential type, because as they provide a higher level of assurance than a client secret. When using a trusted public certificate, you can add the certificate using the Certificates & secrets feature. Your certificate must be one of the following file types: .cer, .pem, .crt.


    **Note**: The client secret, also known as an *application password*, is a string value your app can use in place of a certificate to identity itself. It's the easier of the two credential types to use. It's often used during development, but is considered less secure than a certificate. You should use certificates in your applications running in production.

1. Wählen Sie im Azure-Portal unter  **App-Registrierungen**  Ihre Anwendung aus.

2. Wählen Sie  **Zertifikate und Geheimnisse** und dann  **+ Neuer geheimer Clientschlüssel** aus.

3. Fügen Sie eine Beschreibung für Ihren geheimen Clientschlüssel hinzu.

4. Wählen Sie eine Dauer aus.

5. Klicken Sie auf **Hinzufügen**.

6. **Speichern Sie den Wert des geheimen Schlüssels in Editor**  für die Verwendung in Ihrem Clientanwendungscode. Auf der Seite „Zertifikat und Geheimnis“ wird der neue geheime Wert angezeigt. Es ist wichtig, diesen Wert zu kopieren, da er nur dieses eine Mal angezeigt wird. Wenn Sie die Seite aktualisieren und zurückkehren, wird er nur noch als maskierter Wert angezeigt.

7. Überspringen Sie die Abschnitte  **Umleitungs-URI hinzufügen**  und  **Plattformeinstellungen konfigurieren** . Sie müssen keinen Umleitungs-URI für eine Web-API konfigurieren, da keine Benutzer interaktiv angemeldet werden.

8. Überspringen Sie vorerst den Abschnitt  **Anmeldeinformationen hinzufügen** . Ihre API würde nur eigene Anmeldeinformationen benötigen, wenn sie auf eine nachgelagerte API zugreifen müsste. Ein solches Szenario wird in diesem Artikel nicht behandelt.

Nachdem Sie Ihre Web-API registriert haben, können Sie die Bereiche hinzufügen, mit denen der Code Ihrer API eine differenzierte Berechtigung für Nutzer Ihrer API bereitstellen kann.


#### Schritt 5: Hinzufügen eines Bereichs

Der Code in einer Clientanwendung fordert die Berechtigung zum Ausführen von Vorgängen an, die von Ihrer Web-API definiert werden, indem er zusammen mit seinen Anforderungen ein Zugriffstoken an die geschützte Ressource (die Web-API) übergibt. Ihre Web-API führt anschließend den angeforderten Vorgang nur dann aus, wenn das empfangene Zugriffstoken die für den Vorgang erforderlichen Bereiche (auch als Anwendungsberechtigungen bezeichnet) enthält.

Führen Sie zuerst die folgenden Schritte aus, um einen Beispielbereich namens „Employees.Read.All“ zu erstellen:

1. Melden Sie sich beim Microsoft Entra Admin Center an.

2. Wenn Sie Zugriff auf mehrere Mandanten haben, verwenden Sie im Menü am oberen Rand den Filter  **Verzeichnis und Abonnement** , um den Mandanten auszuwählen, der die Registrierung der Client-App enthält.

3. Wählen Sie  **Identität**, dann **Anwendung**  und schließlich  **App-Registrierungen** und danach die App-Registrierung Ihrer API aus.

4. Wählen Sie  **Eine API verfügbar machen** und dann  **+ Bereich hinzufügen** aus.

    ![Bereich „Eine API verfügbar machen“ der App-Registrierung im Azure-Portal](./media/portal-02-expose-api.png)

5. Sie werden aufgefordert, einen  **Anwendungs-ID-URI** festzulegen, falls Sie noch keinen konfiguriert haben. Der APP-ID-URI fungiert als Präfix für die Bereiche, auf die Sie in Ihrem API-Code verweisen, und muss global eindeutig sein. Sie können den bereitgestellten Standardwert im Format api://\<application-client-id\> verwenden oder einen besser lesbaren URI wie  `https://contoso.com/api` angeben.

6. Wählen Sie **Speichern und fortfahren** aus.

6. Geben Sie als Nächstes unter  **Bereich hinzufügen** die Attribute des Bereichs an. Für diese exemplarische Vorgehensweise können Sie die Beispielwerte verwenden oder eigene Werte angeben.

    | Feld| Beschreibung des Dataflows| Beispiel|
    | :--- | :--- | :--- |
    | Bereichsname| Name des Bereichs. Eine allgemeine Benennungskonvention für den Bereich ist „Ressource.Vorgang.Einschränkung“.| Employees.Read.All|
    | Zum Einwilligen berechtigte Personen| Gibt an, ob für diesen Bereich die Einwilligung von Benutzern ausreicht oder die Einwilligung eines Administrators erforderlich ist. Wählen Sie für umfassendere Berechtigungen die Option Nur Administratoren.| Administratoren und Benutzer|
    | Anzeigename der Administratoreinwilligung| Eine kurze Beschreibung des Zwecks für den Bereich, der nur Administratoren angezeigt wird.| Schreibgeschützter Zugriff auf Mitarbeiterdatensätze|
    | Beschreibung der Administratoreinwilligung| Eine ausführlichere Beschreibung der vom Bereich gewährten Berechtigung, die nur Administratoren angezeigt wird.| Ermöglicht der Anwendung einen schreibgeschützten Zugriff auf alle Mitarbeiterdaten.|
    | Anzeigename der Benutzereinwilligung| Eine kurze Beschreibung des Zwecks für den Bereich. Wird Benutzern nur angezeigt, wenn Sie unter Zum Einwilligen berechtigte Personen die Option Administratoren und Benutzer festgelegt haben.| Schreibgeschützter Zugriff auf Mitarbeiterdatensätze|
    | Beschreibung der Benutzereinwilligung| Eine ausführlichere Beschreibung der Berechtigung, die vom Bereich gewährt wird. Wird Benutzern nur angezeigt, wenn Sie unter Zum Einwilligen berechtigte Personen die Option Administratoren und Benutzer festgelegt haben.| Ermöglichen Sie der Anwendung einen schreibgeschützten Zugriff auf Ihre Mitarbeiterdaten.|

7. Legen Sie den  **Status**  auf  **Aktiviert** fest, und wählen Sie dann  **Bereich hinzufügen** aus.

8. (Optional) Soll Benutzer*innen Ihrer App keine Einwilligungsaufforderung für die von Ihnen festgelegten Bereiche angezeigt werden, können Sie die Clientanwendung für den Zugriff auf Ihre Web-API  *vorab autorisieren* . Sie sollten  *nur*  die Clientanwendungen vorab autorisieren, denen Sie vertrauen, da Ihre Benutzer*innen keine Möglichkeit haben, ihre Einwilligung zu verweigern.

   1. Wählen Sie unter  **Autorisierte Clientanwendungen** die Option  **Eine Clientanwendung hinzufügen** aus.

   2. Geben Sie den Wert für  **Anwendungs-ID (Client)**  der Clientanwendung ein, die Sie vorab autorisieren möchten, beispielsweise den einer zuvor registrierten Webanwendung.

   3. Wählen Sie unter  **Autorisierte Bereiche** die Bereiche aus, für die Sie die Einwilligungsaufforderung unterdrücken möchten, und wählen Sie dann  **Anwendung hinzufügen** aus.

   4. Wenn Sie diesen optionalen Schritt ausgeführt haben, ist die Client-App jetzt eine vorab autorisierte Client-App, und Benutzer werden bei der Anmeldung nicht zur Einwilligung aufgefordert.

#### Aufgabe 6: Hinzufügen eines Bereichs, der eine Administratoreinwilligung erfordert

Fügen Sie als Nächstes einen weiteren Beispielbereich namens „Employees.Write.All“, dem nur Administratoren die Einwilligung erteilen können. Bereiche, die die Einwilligung von Administratoren erfordern, werden in der Regel für den Zugriff auf Vorgänge mit erforderlichen höheren Berechtigungen verwendet. Außerdem werden sie häufig von Clientanwendungen verwendet, die als Back-End-Dienste oder Daemons ausgeführt werden und keine Benutzer interaktiv anmelden.

1. Um den Beispielbereich „Employees.Write.All“ hinzuzufügen, führen Sie die oben beschriebenen Schritte aus, und geben Sie unter  **Bereich hinzufügen**  die folgenden Werte an:

    | Feld| Beispielwert|
    | :--- | :--- |
    | Bereichsname| Employees.Write.All|
    | Zum Einwilligen berechtigte Personen| Nur Administratoren|
    | Anzeigename der Administratoreinwilligung| Schreibzugriff auf Mitarbeiterdatensätze|
    | Beschreibung der Administratoreinwilligung| Ermöglicht der Anwendung Schreibzugriff auf alle Mitarbeiterdaten.|
    | Anzeigename der Benutzereinwilligung| Keine (Feld leer lassen)|
    | Beschreibung der Benutzereinwilligung| Keine (Feld leer lassen)|

    >**Hinweis**: Wenn Sie die beiden in den vorherigen Abschnitten beschriebenen Beispielbereiche erfolgreich hinzugefügt haben, werden sie, ähnlich wie in der folgenden Abbildung gezeigt, im Bereich  **Eine API verfügbar machen**  der App-Registrierung Ihrer Web-API angezeigt:

    ![Screenshot des Bereiches „Eine API verfügbar machen“ mit zwei verfügbar gemachten Bereichen.](./media/portal-03-scopes-list.png)

    Wie aus der Abbildung hervorgeht, wird die vollständige Zeichenfolge eines Bereichs durch die Verkettung von  **Anwendungs-ID-URI**  der Web-API und  **Bereichsname** des Bereichs gebildet.

        **Note**: For example, if your web API's application ID URI is `https://contoso.com/api` and the scope name is Employees.Read.All, the full scope is: `https://contoso.com/api/Employees.Read.All`


        **Note**: Next, you will configure a client app's registration with access to your web API and the scopes you defined by following the steps above.
    Nachdem der Registrierung einer Client-App die Berechtigung für den Zugriff auf Ihre Web-API erteilt wurde, kann Microsoft Identity Platform für den Client ein OAuth 2.0-Zugriffstoken ausstellen. Wenn der Client die Web-API aufruft, präsentiert er ein Zugriffstoken, dessen Bereichsanspruch (scp) auf die Berechtigungen festgelegt ist, die Sie in der Client-App-Registrierung angegeben haben. Sie können später bei Bedarf zusätzliche Bereiche verfügbar machen. Beachten Sie, dass Ihre Web-API mehrere Bereiche verfügbar machen kann, die verschiedenen Vorgängen zugeordnet sind. Ihre Ressource kann zur Laufzeit durch Auswerten der Bereichsansprüche (scp) im erhaltenen OAuth 2.0-Zugriffstoken den Zugriff auf die Web-API steuern.


### Übung 2: Verwalten von App-Registrierungen mit einer benutzerdefinierten Rolle

#### Aufgabe 1: Erstellen einer neuen benutzerdefinierten Rolle zum Gewähren von Zugriff zum Verwalten von App-Registrierungen

Sie müssen eine neue benutzerdefinierte Rolle für die App-Verwaltung erstellen. Diese neue Rolle sollte nur die spezifischen Berechtigungen erhalten, die für die Verwaltung von Anmeldeinformationen erforderlich sind.

1. Melden Sie sich bei  [https://entra.microsoft.com](https://entra.microsoft.com)  mit einem globalen Administratorkonto an.

2. Öffnen Sie das Portalmenü, und wählen Sie dann  **Microsoft Entra ID** aus.

3. Wählen Sie im linken Menü unter **Identität** die Option **Rollen und Administratoren** aus.

4. Wählen Sie dann das Element **Rollen und Administratoren** und anschließend **+ Neue benutzerdefinierte Rolle** aus.

    ![Screenshot des Blatts „Rollen und Administratoren“ mit hervorgehobener Menüoption „Neue benutzerdefinierte Rolle“](./media/lp3-mod1-new-custom-role.png)

5. Geben Sie im Dialogfeld „Neue benutzerdefinierte Rolle“ auf der Registerkarte „Grundlagen“ im Namensfeld den Namen **My custom app role** ein.

6. Überprüfen Sie die übrigen Einstellungen, und wählen Sie dann **Weiter** aus.

7. Überprüfen Sie die verfügbaren Berechtigungen auf der Registerkarte Berechtigungen.

8. Geben Sie im Feld **Nach Rollennamen oder -beschreibung suchen** die **Anmeldeinformationen** ein.

9. Wählen Sie in den Ergebnissen die Berechtigungen zum **Verwalten** und dann **Weiter** aus.

    ```
       microsoft.directory/servicePrincipals/managePasswordSingleSignOnCredentials  -   Manage password single sign-on credentials or service principals.
       microsoft.directory/servicePrincipals/synchronizationCredentials/manage    -   Manage application provisioning secrets and credentials.
    ```

    ![Screenshot der Registerkarte „Berechtigungen“ für neue benutzerdefinierte Rollen mit hervorgehobener Suche, den Berechtigungen zum Verwalten und der Option „Weiter“](./media/lp3-mod1-custom-role-permissions.png)

    **Warum diese beiden Elemente ausgewählt werden**: Für die Anwendungsbereitstellung dieser beiden Elemente sind nur die Mindestberechtigungen erforderlich, um einmaliges Anmelden für die zu erstellende Anwendung oder den Dienstprinzipal zu aktivieren und zu erzwingen und um die Unternehmensanwendung einer Benutzergruppe oder Gruppen zuzuweisen.  Andere Berechtigungen können ebenfalls erteilt werden.  Sie finden eine vollständige Liste der verfügbaren Berechtigungen unter `https://docs.microsoft.com/azure/active-directory/roles/custom-enterprise-app-permissions`.

10. Überprüfen Sie die Änderungen, und wählen Sie dann **Erstellen** aus.
