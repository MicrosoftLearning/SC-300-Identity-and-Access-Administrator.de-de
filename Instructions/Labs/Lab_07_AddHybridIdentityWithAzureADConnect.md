---
lab:
  title: 07 - Optional --- Hinzufügen von hybriden Identitäten mit Microsoft Entra Connect
  learning path: '01'
  module: Module 01 - Implement an identity management solution
---

# Lab 07: OPTIONAL --- Hinzufügen von hybriden Identitäten mit Microsoft Entra Connect

# Dieses Lab funktioniert nur in einer Umgebung ohne Lab-Hoster. Wenn Sie es mit einem persönlichen Konto ausprobieren möchten, sollte es funktionieren. Sie können dies nicht innerhalb des Kurses ausführen.





**Hinweis**: Dieses Lab ist optional.  Die Bearbeitung dauert mindestens 1 Stunde, und Sie sollten die Arbeitsschritte so detailliert wie möglich befolgen.  Bitte nutzen Sie den Computer, wenn es Ihre Zeit erlaubt.  Wenn Ihr Unternehmen bereits eine Hybrid-Konfiguration eingerichtet hat oder Sie nicht vorhaben, Microsoft Entra Connect zu verwenden, überspringen Sie bitte dieses Lab.

## Labszenario

Ihr Unternehmen verfügt über lokale Azure Active Directory Domain Services (AD DS).  Sie möchten weiterhin ein lokales Active Directory als Lösung für das Identity & Access Management verwenden, aber auch die Möglichkeit bieten, dass Benutzer auf Cloudanwendungen mit demselben Benutzernamen und Kennwort zugreifen können.

#### Geschätzte Dauer: 60 Minuten

### Übung 1: Einrichten der lokalen Infrastruktur

#### Aufgabe 1: Erstellen der lokalen Active Directory-Infrastruktur

1. Auf die Bereitstellungsvorlage kann unter diesem Link zugegriffen werden: [Leitfaden zur lokalen Test-Labumgebung](https://github.com/maxskunkworks/TLG/tree/master/tlg-base-config_3-vm).

    **Hinweis für Lernende und MCTs**: Die Bereitstellung dieser Vorlage kann 30 bis 60 Minuten dauern. Sie sollten also bereit sein, bei diesem Schritt eine Pause einzulegen oder die Bereitstellung vor einem Vortragsteil des Kurses durchzuführen.

    **Hinweis für Labanbieter**: Wenn möglich, wäre es für Lernende hilfreich, wenn sie die Labumgebung im Rahmen ihrer Einrichtung durchführen und bereitstellen könnten.

2. Wählen Sie auf der Seite **TLG (Test Lab Guide) - 3 VM Base Configuration (v1.0)** die Option **Deploy to Azure** aus.

   **Hinweis**: Die 3 VM Base Configuration stellt einen Domänencontroller für Windows Server 2016 Active Directory mit dem Namen DC1 bereit, der den Domänennamen, den Sie angeben, und einen Domänenmitgliedsserver mit dem Namen APP1 verwendet, auf dem Windows Server 2016 ausgeführt wird. Sie bietet auch eine Option zum Bereitstellen einer Client-VM unter Windows 10. Diese verwenden wird jedoch nicht in unserem Lab (in erster Linie aufgrund von Lizenzierungsanforderungen, die bei der Ausführung von Windows 10-VMs in Azure gelten). Auf dem Domänenmitgliedsserver (APP1) ist .NET 4.5 und IIS automatisch installiert.  
   
   **Hinweis**: Die VM, die für dieses Lab erforderlich ist, ist **DC1**.

3. Legen Sie auf der Seite **Benutzerdefinierte Bereitstellung** die folgenden Einstellungen fest, und wählen Sie dann **Überprüfen + erstellen** und danach **Erstellen** aus.

   -   Abonnement: Der Name des Azure-Zielabonnements, in dem Sie die Azure-VMs der Labumgebung bereitstellen möchten.
   -   Ressourcengruppe: (Neu erstellen) **hybrididentity-RG**
   -   Speicherort: Der Name der Azure-Region, die die Azure-VMs der Labumgebung hosten soll.
   -   Konfigurationsname: **TlgBaseConfig-01**
   -   Domänenname: **corp.contoso.com**
   -   Serverbetriebssystem: **2016-Datacenter**
   -   Administratorbenutzername: **demouser**
   -   Administratorkennwort: **Geben Sie ein sicheres Kennwort ein, das Sie sich merken können**
   -   Client-VM bereitstellen: **Nein**
   -   Client-VHD-URI: **Leer lassen**
   -   VM-Größe: **Standard_D2s_v3**
   
   **Hinweis**: Verwenden Sie eine ähnliche VM-Größe, wenn Ihr Abonnement die aufgeführte Größe nicht unterstützt. Die Dokumentation ist hier verknüpft: <https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sizes>.

   -   DNS-Bezeichnungspräfix: **Jeder gültige, global eindeutige DNS-Name (eine eindeutige Zeichenfolge bestehend aus Buchstaben, Ziffern und Bindestrichen, beginnend mit einem Buchstaben und bis zu 47 Zeichen).**

   -   _artifacts-Speicherort: **Übernehmen Sie die Standardeinstellung**
   -   _artifacts-Speicherort-Sas-Token: **Leer lassen**

4. Wählen Sie **Überprüfen + erstellen** aus.

5. Wählen Sie nach erfolgreicher Überprüfung **Erstellen** aus.
    
6. Warten Sie, bis die Bereitstellung abgeschlossen ist. Dies kann etwa 60 Minuten dauern.


### Aufgabe 2: Konfigurieren der Labumgebung für Azure-VMs

1. Navigieren Sie im Browserfenster, in dem das Azure-Portal angezeigt wird, zur Azure-VM **DC1**, und stellen Sie eine Verbindung über Remotedesktop her. Wenn Sie dazu aufgefordert werden, melden Sie sich mit den folgenden Anmeldeinformationen an:

   -   Benutzername: **demouser**
   -   Kennwort: **Verwenden das sichere Kennwort, das Sie in Aufgabe 1 erstellt haben**

2.  Starten Sie in der Remotedesktopsitzung zu **DC1** **Windows PowerShell ISE** und öffnen Sie dann den Skriptbereich.  Fügen Sie als Nächstes das folgende Skript zum Skriptbereich hinzu und führen Sie es aus, um die erweiterte Sicherheitskonfiguration von Internet Explorer und die Benutzerzugriffssteuerung auf den Azure-VMs **DC1** und **APP1** zu deaktivieren:

    ```pwsh

    $vmNames = @('dc1','app1')
    Invoke-Command -ComputerName $vmNames {Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Active Setup\Installed Components\{A509B1A7-37EF-4b3f-8CFC-4F3A74704073}" -Name "IsInstalled" -Value 0}
    Invoke-Command -ComputerName $vmNames {Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Active Setup\Installed Components\{A509B1A8-37EF-4b3f-8CFC-4F3A74704073}" -Name "IsInstalled" -Value 0}
    Invoke-Command -ComputerName $vmNames {Set-ItemProperty "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" -Name "ConsentPromptBehaviorAdmin" -Value 00000000}
    ```

    **Hinweis:** Wenn Sie mehrere PowerShell-Skripts in derselben Datei ausführen möchten, können Sie ein bestimmtes Skript markieren und neben der grünen Wiedergabeschaltfläche **Auswahl ausführen** auswählen. 

3.  Fügen Sie im Fenster **Windows PowerShell ISE** das folgende Skript zum Skriptbereich hinzu, und führen Sie es aus, um Remoteserver-Verwaltungstools auf den beiden Azure-VMs *DC1* und **APP1** zu installieren:

    ```pwsh

    $vmNames = @('dc1','app1')
    Invoke-Command -ComputerName $vmNames {Install-WindowsFeature RSAT -IncludeAllSubFeature} 
    ```

4.  Fügen Sie im Fenster **Windows PowerShell ISE** das folgende Skript zum Skriptbereich hinzu, und führen Sie es aus, um TLS 1.2 auf den beiden Azure-VMs *DC1* und **APP1** zu aktivieren:

    ```pwsh

    $vmNames = @('dc1','app1')
    Invoke-Command -ComputerName $vmNames {New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -Force}
    Invoke-Command -ComputerName $vmNames {New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -Force}
    Invoke-Command -ComputerName $vmNames {New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -name 'Enabled' -value 1 –PropertyType DWORD}
    Invoke-Command -ComputerName $vmNames {New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -name 'DisabledByDefault' -value 0 –PropertyType DWORD}
    Invoke-Command -ComputerName $vmNames {New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -name 'Enabled' -value 1 –PropertyType DWORD}
    Invoke-Command -ComputerName $vmNames {New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -name 'DisabledByDefault' -value 0 –PropertyType DWORD}
    Invoke-Command -ComputerName $vmNames {New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\.NETFramework\v4.0.30319' -name 'SchUseStrongCrypto' -value 1 –PropertyType DWORD}
    ```

5.  Fügen Sie im Fenster **Windows PowerShell ISE** das folgende Skript zum Skriptbereich hinzu, und führen Sie es aus, um die integrierte Windows-Authentifizierung auf der Standardwebsite zu konfigurieren, die auf der Azure-VM **APP1** gehostet wird:

    ```pwsh

    $vmNames = @('app1')
    Invoke-Command -ComputerName $vmNames {Enable-WindowsOptionalFeature -Online -FeatureName IIS-WindowsAuthentication}
    Invoke-Command -ComputerName $vmNames {Set-WebConfigurationProperty -Filter "/system.webServer/security/authentication/anonymousAuthentication" -Name Enabled -Value False -PSPath IIS:\ -Location "Default Web Site"}
    Invoke-Command -ComputerName $vmNames {Set-WebConfigurationProperty -Filter "/system.webServer/security/authentication/windowsAuthentication" -Name Enabled -Value True -PSPath IIS:\ -Location "Default Web Site"}
    ```

### Aufgabe 3: Neustarten der Azure-VMs

1. Führen Sie im Fenster **Windows PowerShell ISE** im Konsolenbereich Folgendes aus, um **APP1** neu zu starten:

    ```pwsh

    Restart-Computer -ComputerName 'APP1'
    ```

2. Führen Sie im Fenster **Windows PowerShell ISE** im Konsolenbereich Folgendes aus, um **DC1** neu zu starten:

    ```pwsh
    Restart-Computer -ComputerName 'DC1'
    ```

### Aufgabe 5: Konfigurieren von Active Directory für contoso.local

1. Stellen Sie erneut eine Verbindung zur Azure VM **DC1** über Remotedesktop her. Wenn Sie dazu aufgefordert werden, melden Sie sich mit den folgenden Anmeldeinformationen an:

    -   Benutzername: **demouser**

    -   Kennwort: **demo\@pass123**
       - **Es wird dringend empfohlen, ein sicheres Kennwort einzugeben, das Sie sich merken können.**

2.  Starten Sie Internet Explorer in der Remotedesktopsitzung auf **DC1**, und navigieren Sie zu dem nachstehenden Link.

    ```
    https://github.com/microsoft/MCW-Hybrid-identity/tree/main/Archive/Hands-on%20lab/studentfiles
    ```

3. Wählen Sie auf der Seite **Create Users/Group for Active Directory Demo/Test Environment** den Link **CreateDemoUsers.ps1** aus, akzeptieren Sie die Lizenzbedingungen, und speichern Sie das entsprechende Skript im lokalen Dateisystem.

4. Wählen Sie auf der Seite **Create Users/Group for Active Directory Demo/Test Environment** den Link **CreateDemoUsers.csv** (direkt über dem PowerShell-Codeabschnitt) aus, und speichern Sie die entsprechende CSV-Datei an demselben Speicherort wie die Datei **CreateDemoUsers.ps1**.

5. Starten Sie in der Remotedesktopsitzung auf **DC1** Datei-Explorer, navigieren Sie zu dem Ordner, in dem Sie beide Dateien heruntergeladen haben. Wählen Sie mit der rechten Maustaste die Datei **CreateDemoUsers.ps1** aus, wählen Sie **Eigenschaften** aus, aktivieren Sie im Dialogfeld **Eigenschaften von CreateDemoUsers.ps1** das Kontrollkästchen **Entsperren**, und wählen Sie **OK** aus.

6. Wählen Sie im Fenster „Datei-Explorer“ erneut mit der rechten Maustaste die Datei **CreateDemoUsers.ps1** aus, und wählen Sie **Bearbeiten** aus. 

7. Ändern Sie im Fenster **Administrator: Windows PowerShell ISE** die Zeile **148** von:

    ```pwsh
    $UserCount = 1000 #Up to 2500 can be created
    ```

   in
    ```pwsh
    $UserCount = 2500 #Up to 2500 can be created
    ```

8. Speichern Sie im Fenster **Windows PowerShell ISE** die Änderung, und führen Sie das Skript **CreateDemoUsers.ps1** aus, um eine Organisationseinheitshierarchie der Labumgebung zu erstellen und mit Testbenutzerkonten zu füllen. 

9.  Fügen Sie im Fenster **Windows PowerShell ISE** das folgende Skript zum Skriptbereich hinzu, und führen Sie es aus, um die Einstellungen der AD-Benutzerkonten zu ändern, die Sie in dieser Übung verwenden werden:

    ```pwsh

    $adUser1 = Get-ADUser -Filter {samAccountName -eq "AGAyers"}
    $adUser1groups = $adUser1 | Get-ADPrincipalGroupMembership 
    $adUser1groups | foreach { if ($_.name -ne 'Domain Users') {Remove-ADPrincipalGroupMembership -MemberOf $_.name -Identity $adUser1.DistinguishedName} }
    Add-ADPrincipalGroupMembership -MemberOf 'Engineering' -Identity $adUser1.DistinguishedName
    Move-ADObject -Identity $adUser1.DistinguishedName -TargetPath 'OU=NJ,OU=US,OU=Users,OU=Demo Accounts,DC=corp,DC=contoso,DC=com'

    Set-ADAccountPassword -Identity 'CN=Ayers\, Ann,OU=NJ,OU=US,OU=Users,OU=Demo Accounts,DC=corp,DC=contoso,DC=com' -Reset -NewPassword (ConvertTo-SecureString -AsPlainText "demo@pass123" -Force)

    $adUser2 = Get-ADUser -Filter {samAccountName -eq "TFBell"}
    $adUser2groups = $adUser2 | Get-ADPrincipalGroupMembership 
    $adUser2groups | foreach { if ($_.name -ne 'Domain Users') {Remove-ADPrincipalGroupMembership -MemberOf $_.name -Identity $adUser2.DistinguishedName} }
    Add-ADPrincipalGroupMembership -MemberOf 'Engineering' -Identity $adUser2.DistinguishedName
    Move-ADObject -Identity $adUser2.DistinguishedName -TargetPath 'OU=VT,OU=US,OU=Users,OU=Demo Accounts,DC=corp,DC=contoso,DC=com'

    Set-ADAccountPassword -Identity 'CN=Bell\, Teresa,OU=VT,OU=US,OU=Users,OU=Demo Accounts,DC=corp,DC=contoso,DC=com' -Reset -NewPassword (ConvertTo-SecureString -AsPlainText "demo@pass123" -Force)
    Get-ADGroup -Identity 'Domain Admins' | Add-ADGroupMember -Members 'CN=Ayers\, Ann,OU=NJ,OU=US,OU=Users,OU=Demo Accounts,DC=corp,DC=contoso,DC=com'
    Get-ADGroup -Identity 'Enterprise Admins' | Add-ADGroupMember -Members 'CN=Ayers\, Ann,OU=NJ,OU=US,OU=Users,OU=Demo Accounts,DC=corp,DC=contoso,DC=com'
    ```

10. Fügen Sie im Fenster **Windows PowerShell ISE** das folgende Skript zum Skriptbereich hinzu, und führen Sie es aus, um zusätzliche Organisationseinheiten mit dem Namen **Server** und **Clients** zu erstellen und das Computerkonto **APP1** auf den ersten davon zu verschieben:

    ```pwsh

    New-ADOrganizationalUnit -Name 'Servers' -Path 'OU=Demo Accounts,DC=corp,DC=contoso,DC=com'
    New-ADOrganizationalUnit -Name 'Clients' -Path 'OU=Demo Accounts,DC=corp,DC=contoso,DC=com'

    Move-ADObject -Identity 'CN=APP1,CN=Computers,DC=corp,DC=contoso,DC=com' -TargetPath 'OU=Servers,OU=Demo Accounts,DC=corp,DC=contoso,DC=com'
    ```

11. Melden Sie sich von **DC1** ab.

## Übung 2: Integrieren einer Active Directory-Gesamtstruktur in einem Azure Active Directory-Mandanten

### Aufgabe 1: Erstellen eines Azure Active Directory-Mandanten und Aktivieren einer EMS E5-Testversion

In dieser Aufgabe erstellen Sie einen Azure Active Directory-Mandanten mit den folgenden Einstellungen: 

-   Organisationsname: **Contoso**

-   Anfänglicher Domänenname: Jeder gültige, eindeutige Domänenname.

-   Land oder Region: **USA**

1. Starten Sie auf dem Lab-Computer ein neues Webbrowserfenster, und navigieren Sie zum Azure-Portal unter <https://portal.azure.com>, sofern noch nicht geschehen.

2. Wenn Sie dazu aufgefordert werden, melden Sie sich bei dem Azure-Abonnement an, in dem Sie in den Übungen „Vor dem Praxislab“ Ressourcen bereitgestellt haben.

3. Wählen Sie auf dem Lab-Computer im Azure-Portal **+ Ressource erstellen** aus.

4. Geben Sie auf der Seite **Neu** im Textfeld **Marketplace durchsuchen** **Azure Active Directory** ein, und wählen Sie in der Ergebnisliste **Azure Active Directory** aus.

5. Wählen Sie auf der Seite **Azure Active Directory** die Option **Erstellen** aus.

6. Legen Sie auf der Seite **Verzeichnis erstellen** die folgenden Einstellungen fest, und wählen Sie **Erstellen** aus:

Registerkarte „Grundeinstellungen“:
    -   Mandantentyp auswählen: Wählen Sie **Azure Active Directory** aus.

Registerkarte „Konfiguration“
    -   Organisationsname: **Contoso**

    -   Anfänglicher Domänenname: Jeder gültige, eindeutige Domänenname.

    -   Land oder Region: **USA**

7. Öffnen Sie nach der Erstellung **Azure Active Directory**.

8. Wählen Sie auf der Seite „Übersicht“ die Option **Mandanten verwalten** aus.

9. Setzen Sie ein Häkchen vor Ihr neu erstelltes Verzeichnis.

10. Wählen Sie obenauf der Seite **Wechseln** aus.

    >**Hinweis**: Es einige Minuten dauern kann, bis alles korrekt angezeigt wird.

11. Wählen Sie auf der Seite **Contoso – Übersicht** die Option **Benutzer** aus.

12. Beachten Sie, dass Sie nur über einen einzelnen ExternalAzureAD-Benutzer in diesem neuen Mandanten verfügen.

### Aufgabe 2: Erstellen und Konfigurieren des Azure AD-Benutzers zum Verwalten dieses Verzeichnisses

1. Navigieren Sie auf dem Lab-Computer im Azure-Portal zurück zur Seite **Contoso – Übersicht**.

2. Wählen Sie auf der Seite **Contoso – Übersicht** die Option **Benutzer** unter **Verwalten** im linken Navigationsbereich aus.

3. Wählen Sie auf der Seite **Benutzer – Alle Benutzer** den Eintrag aus, der Ihr Benutzerkonto darstellt.

4. Wählen Sie auf der Seite **Profil** die Option **Bearbeiten** aus.

5. Wählen Sie im Abschnitt **Einstellungen** in der Dropdownliste **Nutzungsspeicherort** den Eintrag **USA** aus, und wählen Sie **Speichern** aus.

#### Erstellen des neuen Administrators

6. Vergewissern Sie sich, dass auf der Seite **Neuer Benutzer** die Option **Benutzer erstellen** aktiviert ist, geben Sie die folgenden Einstellungen an, und wählen Sie **Erstellen** aus:

    - Benutzername: **john.doe *@your Domänenname des Azure AD-Mandanten* ** wobei ***der Domänenname Ihres Azure AD-Mandanten*** der Domänenname ist, den Sie beim Erstellen des Azure AD-Mandanten „Contoso“ angegeben haben.

    - Name: **john.doe**

    - Vorname: **John**

    - Nachname: **Doe**
    
    - Kennwort: **Kennwort automatisch generieren**
    
    - Kennwort anzeigen: **Aktiviert**, kopieren Sie dann das Kennwort.

    - Gruppen: **0 Gruppen ausgewählt**
    
    - Rollen: **Globaler Administrator**
    
    - Anmeldung blockieren: **Nein**
    
    - Nutzungsspeicherort: **USA**
    
    - Position: **Leer lassen**
    
    - Abteilung: **Leer lassen**

    > **Hinweis**: Kopieren Sie die Werte für **Benutzername** und **Kennwort** in den Editor. Sie werden sie später in diesem Lab benötigen.


### Aufgabe 5: Konfigurieren des DNS-Suffix in der Active Directory-Gesamtstruktur für Contoso

In dieser Aufgabe konfigurieren Sie das DNS-Suffix der Active Directory-Gesamtstruktur für Contoso so, dass sie mit dem neu überprüften benutzerdefinierten Azure AD-Domänennamen übereinstimmt.

1. Bestätigen Sie auf dem Lab-Computer im Azure-Portal, dass Sie beim Azure AD-Mandanten angemeldet sind, der dem Azure-Abonnement zugeordnet ist, in dem Sie in den Übungen „Vor dem Praxislab“ Ressourcen (im **Standardverzeichnis**) bereitgestellt haben. Wählen Sie andernfalls das Symbol **Verzeichnis + Abonnement** in der Symbolleiste des Azure-Portal (rechts neben dem Symbol **Cloud Shell**) aus, um zu diesem Azure AD-Mandanten zu wechseln. 

2. Navigieren Sie im Azure-Portal zur Seite der VM **DC1**.

3. Stellen Sie auf der Seite der VM **DC1** über Remotedesktop eine Verbindung mit **DC1** her. Wenn Sie aufgefordert werden, sich anzumelden, verwenden Sie den Namen **demouser** und das Kennwort **demo\@pass123**. 

4. Starten Sie in der Remotedesktopsitzung auf **DC1** im Fenster **Server-Manager** die Konsole **Active Directory-Domänen und -Vertrauensstellungen** unter **Tools**. 

5. Wählen Sie in der Konsole **Active Directory-Domänen und -Vertrauensstellungen** mit der rechten Maustaste **Active Directory-Domänen und -Vertrauensstellungen [DC1.corp.contoso.com]** aus, und wählen Sie **Eigenschaften** aus.

6. Geben Sie auf der Registerkarte **UPN-Suffixe** des Fensters **Active Directory-Domänen und -Vertrauensstellungen [DC1.corp.contoso.com]** in das Textfeld **Alternative UPN-Suffixe** den Namen der benutzerdefinierten Domäne ein, den Sie in der vorherigen Aufgabe überprüft haben, wählen Sie **Hinzufügen** und dann **OK** aus.

7. Starten Sie in der Remotedesktopsitzung auf **DC1** im Fenster **Server-Manager** die Konsole **Active Directory-Benutzer und -Computer** unter **Tools**. 

8. Erweitern Sie in der Konsole **Active Directory-Benutzer und -Computer** links den Eintrag **corp.contoso.com**, und überprüfen Sie die Organisationseinheitshierarchie der Domäne und die Gruppenmitgliedschaft der Domänengruppen. 

9.  Starten Sie in der Remotedesktopsitzung auf **DC1** Windows PowerShell ISE, und führen Sie im Skriptbereich Folgendes aus, um das UPN-Suffix aller Benutzer, die Mitglieder der Gruppe **Engineering** sind, durch diejenigen zu ersetzen, die mit dem benutzerdefinierten überprüften Domänennamen des Azure AD-Mandanten „Contoso“ übereinstimmen (ersetzen Sie den Platzhalter `<custom_domain_name>` durch den tatsächlichen Namen des benutzerdefinierten überprüften Domänennamens, den Sie dem Azure AD-Mandanten „Contoso“ zugewiesen haben). 

    ```pwsh
    $domainName = '<custom_domain_name>'
    $users = Get-ADGroupMember -Identity 'Engineering' -Recursive | Where-Object {$_.objectClass -eq 'user'}

    foreach ($user in $users) {
        $user = Get-ADUser -Identity $User.SamAccountName
        $userName = $user.UserPrincipalName.Split('@')[0] 
        $upn = $userName + "@" + $domainName 
        $user | Set-ADUser -UserPrincipalName $upn
    }
    ```

### Aufgabe 6: Microsoft Entra Connect installieren

In dieser Aufgabe werden Sie Microsoft Entra Connect installieren.

1. Wählen Sie in der Remotedesktopsitzung auf **DC1** im Server-Manager **Lokaler Server** aus, und vergewissern Sie sich, dass das **Verstärkte Sicherheitskonfiguration für IE** aktiviert ist. Andernfalls wählen Sie den Link **Ein** neben **Verstärkte Sicherheitskonfiguration für IE** aus, legen die **Administratoreinstellungen** auf **Aus** fest, und wählen **OK** aus.

2. Öffnen Sie in der Remotedesktopsitzung auf **DC1** das Fenster **Windows PowerShell ISE**, und führen Sie diesen Befehl aus, um den Chrome-Browser zu installieren.

    ```pwsh
    $LocalTempDir = $env:TEMP; $ChromeInstaller = "ChromeInstaller.exe"; (new-object System.Net.WebClient).DownloadFile('http://dl.google.com/chrome/install/375.126/chrome_installer.exe', "$LocalTempDir\$ChromeInstaller"); & "$LocalTempDir\$ChromeInstaller" /silent /install; $Process2Monitor = "ChromeInstaller"; Do { $ProcessesFound = Get-Process | ?{$Process2Monitor -contains $_.Name} | Select-Object -ExpandProperty Name; If ($ProcessesFound) { "Still running: $($ProcessesFound -join ', ')" | Write-Host; Start-Sleep -Seconds 2 } else { rm "$LocalTempDir\$ChromeInstaller" -ErrorAction SilentlyContinue -Verbose } } Until (!$ProcessesFound)
    ```

2. Starten Sie in der Remotedesktopsitzung auf **DC1** den Chrome-Browser, und navigieren Sie zum Azure-Portal unter <https://portal.azure.com>.

3. Wenn Sie aufgefordert werden, sich anzumelden, geben Sie die Anmeldedaten des Microsoft Entra-Benutzerkontos **john.doe** ein, das Sie zuvor in Notepad kopiert haben.

4. Geben Sie bei entsprechender Aufforderung das Kennwort für das Benutzerkonto **john.doe** ein. 
  
    > **Hinweis**: Wenn Sie die Nachricht erhalten: **„Dieses Kennwort wird zu häufig verwendet. Wählen Sie ein Kennwort, das weniger leicht zu erraten ist.**“ müssen Sie das Kennwort so lange ändern, bis es eindeutig genug ist, um akzeptiert zu werden.

5. Wählen Sie bei der Frage **Angemeldet bleiben?** **Nein** aus. Sie werden zur Azure-Portal-Schnittstelle weitergeleitet. 

6. Wenn das Dialogfeld **Willkommen bei Microsoft Azure** angezeigt wird, wählen Sie **Vielleicht später** aus. 

7. Suchen Sie im Azure-Portal nach **Microsoft Entra Connect**.

8. Wählen Sie auf der Seite mit den Suchergebnissen **Microsoft Entra Connect**.

9.  Wählen Sie auf der Seite **Microsoft Entra Connect** den Link **Microsoft Entra Connect herunterladen**.  Wählen Sie dann im Menü **Connect-Synchronisierung** aus.

10. Wählen Sie auf der Webseite **Microsoft Azure Active Directory Connect v2** der Website „Microsoft Downloads“ die Option **Herunterladen** aus.

11. Wenn Sie gefragt werden, ob **AzureADConnect.msi** ausgeführt oder gespeichert werden soll, wählen Sie **Ausführen** aus. Dadurch wird die Datei heruntergeladen und der Assistent **Microsoft Azure Active Directory Connect** automatisch gestartet. 

12. Aktivieren Sie auf der Seite **Willkommen bei Azure AD Connect** das Kontrollkästchen **Ich akzeptiere die Lizenzbedingungen und den Datenschutzhinweis**, und wählen Sie anschließend **Weiter** aus.

13. Wählen Sie auf der Seite **Express-Einstellungen** die Schaltfläche **Anpassen** aus.

14. Belassen Sie auf der Seite **Erforderliche Komponenten installieren** alle optionalen Konfigurationsoptionen deaktiviert, und wählen Sie **Installieren** aus.

15. Wählen Sie auf der Seite **Benutzeranmeldung** die Option **Passthrough-Authentifizierung** aus, aktivieren Sie die Kontrollkästchen **Einmaliges Anmelden aktivieren**, und wählen Sie **Weiter** aus.

16. Melden Sie sich auf der Seite **Mit Azure AD verbinden** mit den Anmeldeinformationen des Kontos **john.doe** an, und wählen Sie **Weiter** aus.

17. Stellen Sie auf der Seite **Verzeichnisse verbinden** sicher, dass der Eintrag **corp.contoso.com** in der Dropdownliste **GESAMTSTRUKTUR** angezeigt wird, und wählen Sie **Verzeichnis hinzufügen** aus. Vergewissern Sie sich, dass im **AD-Gesamtstrukturkonto** die Option **AD-Gesamtstrukturkonto** ausgewählt ist, geben Sie in das Textfeld **BENUTZERNAME DES UNTERNEHMENSADMINISTRATORS** den Namen **CORP.CONTOSO.COM\\demouser**, in das Textfeld **KENNWORT** den Wert **demo\@pass123**, und wählen Sie **OK** aus.


18. Zurück auf der Seite **Verzeichnisse verbinden** wählen Sie die Option **Weiter** aus.

19. Stellen Sie auf der Seite **Azure AD-Anmeldungskonfiguration** sicher, dass Ihr benutzerdefinierter Domänenname als überprüftes **Active Directory-UPN-Suffix** aufgeführt ist und dass der Eintrag **userPrincipalName** in der Dropdownliste **BENUTZERPRINZIPALNAME** angezeigt wird. Beachten Sie die Warnung: **Users will not be able to sign into Azure AD with on-premises credentials if the UPN suffix does not match a verified domain name**. Aktivieren Sie das Kontrollkästchen **Ohne Abgleich aller UPN-Suffixe mit überprüften Domänen fortfahren**, und wählen Sie **Weiter** aus. 

    >**Hinweis**: Dies wird erwartet, da einige Benutzer weiterhin mit dem UPN-Suffix **contoso.local** konfiguriert sind. Das nicht routingfähig und kann nicht als verifizierter benutzerdefinierter Domänenname eines Azure AD-Mandanten konfiguriert werden.

20. Wählen Sie auf der Seite **Filtern von Domänen und Organisationseinheiten** die Option **Ausgewählte Domänen und Organisationseinheiten synchronisieren** aus, und stellen Sie dann sicher, dass nur die Organisationseinheiten **DemoAccounts** und alle untergeordneten Organisationseinheiten ausgewählt sind, und wählen Sie **Weiter** aus. 


21. Übernehmen Sie auf der Seite **Eindeutige Identifizierung Ihrer Benutzer** die Standardeinstellungen, und wählen Sie **Weiter** aus. 


22. Übernehmen Sie auf der Seite **Benutzer und Geräte filtern** die Standardeinstellungen, und wählen Sie **Weiter** aus. 

23. Übernehmen Sie auf der Seite **Optionale Features** die Standardeinstellungen, und wählen Sie **Weiter** aus.

24. Wählen Sie auf der Seite **Einmaliges Anmelden aktivieren** die Option **** im Dialogfeld **Anmeldeinformationen für die Gesamtstruktur** ein, melden Sie sich mit dem Benutzernamen **CORP\\demouser** und dem Kennwort **demo\@pass123** an, und wählen Sie **Weiter** aus.


25. Vergewissern Sie sich auf der Seite **Bereit zur Konfiguration**, dass das Kontrollkästchen **Starten Sie den Synchronisierungsvorgang, nachdem die Konfiguration abgeschlossen wurde** **NICHT** aktiviert ist, und wählen Sie **Installieren** aus.


   > **Hinweis**: Sie konfigurieren die Filterung auf Attributebene, bevor Sie den Synchronisierungsprozess aktivieren.

   > **Hinweis**: Die Installation sollte ungefähr 2 Minuten dauern.

26. Wählen Sie auf der Seite **Konfiguration abgeschlossen** die Option **Beenden** aus.


### Aufgabe 7: Aktivieren des Active Directory-Papierkorbs

In dieser Aufgabe aktivieren Sie den Papierkorb in der Active Directory-Domäne „Contoso“. 

1. Starten Sie in der Remotedesktopsitzung auf **DC1** im Menü „Tools“ in der Server-Manager-Konsole **Active Directory-Verwaltungscenter**.


2. Wählen Sie in der Konsole **Active Directory-Verwaltungscenter** mit der rechten Maustaste **corp (local)** auf der linken Seite aus, und wählen Sie **Enable Recycle Bin** aus. Wenn eine Bestätigung angefordert wird, wählen Sie **OK** aus.


3. Wenn Sie aufgefordert werden, „Active Directory-Verwaltungscenter“ zu aktualisieren, wählen Sie **OK** aus.

   > **Hinweis**: Informationen zu den Vorteilen des Papierkorbs in Hybridszenarien finden Sie unter <https://docs.microsoft.com/en-us/azure/active-directory/hybrid/how-to-connect-sync-recycle-bin>

### Aufgabe 8: Konfigurieren der Filterung auf Attributebene in Azure AD Connect

In dieser Aufgabe konfigurieren Sie die Filterung auf Attributsebene von Azure AD Connect, die die Synchronisierung von Benutzerkonten auf diejenigen beschränkt, deren UPN-Suffix mit dem benutzerdefinierten Domänennamen des Azure AD-Zielmandanten übereinstimmt.

   > **Hinweis**: Für die positive Filterung sind mindestens zwei Synchronisierungsregeln erforderlich. Eine davon bestimmt den richtigen Bereich der zu synchronisierenden Objekte. Die zweite Catchall-Synchronisierungsregel filtert alle Objekte heraus, die noch nicht als ein zu synchronisierendes Objekt identifiziert wurden.

1. Starten Sie in der Remotedesktopsitzung auf **DC1** den **Editor für Synchronisierungsregeln** unter **Azure AD Connect** im Menü „Start“.


2. Stellen Sie im Fenster „Editor für Synchronisierungsregeln“ auf der Seite **View and manage your synchronization rules** sicher, dass **Eingehend** in der Dropdownliste **Richtung** angezeigt wird, und wählen Sie **Neue Regel hinzufügen** aus. Dadurch wird der Assistent **Create inbound synchronization rule** gestartet.


3. Geben Sie auf der Seite **Create inbound synchronization rule – Beschreibung** die folgenden Einstellungen an, und wählen Sie **Weiter** aus:

    - Name: **Benutzerdefiniert eingehend aus AD – UPN-Filter**

    - Beschreibung: **Benutzerdefinierte eingehende Regel – enthält Benutzer mit UPN, die mit der benutzerdefinierten Azure AD-Domäne übereinstimmen**

    - Verbundenes System: **corp.contoso.com**

    - Objekttyp des verbundenen Systems: **Benutzer**

    - Metaverse-Objekttyp: **Person**

    - Verknüpfungstyp: **Join**

    - Rangfolge: **50**

    - Tag: **Leer lassen**

    - Kennwortsynchronisierung aktivieren: **Leer lassen**

    - Deaktiviert: **Leer lassen**


4. Wählen Sie auf der Seite **Create inbound scoping filter** die Option **Gruppe hinzufügen** aus, wählen Sie **Klausel hinzufügen** aus, geben Sie Folgendes an, und wählen Sie **Weiter** aus:

    - Attribut: **userPrincipalName**

    - Operator: **ENDSWITH**

    - Wert: **\@\<your custom domain name>**

5. Wählen Sie auf der Seite **Verknüpfungsregeln** die Option **Weiter** aus.

6. Wählen Sie auf der Seite **Transformationen** die Option **Transformation hinzufügen** aus, geben Sie Folgendes an, und wählen Sie **Hinzufügen** aus:

    - FlowType: **Constant**

    - Zielattribut: **cloudFiltered**

    - Quelle: **False**

7. Wenn ein **Warnungsdialogfeld** mit der Meldung **A full import and full synchronization will be run on 'corp.contoso.com' during your next synchronization cycle** angezeigt wird, wählen Sie **OK** aus.

   > **Hinweis**: Dadurch sollten Sie zurück zur Schnittstelle zum Anzeigen und Verwalten Ihrer Synchronisierungsregeln gelangen, wobei die neue Regel oben in der Regelliste aufgeführt ist. 

8. Zurück im Fenster **Editor für Synchronisierungsregeln** stellen Sie auf der Seite **View and manage your synchronization rules** sicher, dass **Eingehend** in der Dropdownliste **Richtung** angezeigt wird, und wählen Sie erneut **Neue Regel hinzufügen** aus. Dadurch wird der Assistent **Create inbound synchronization rule** gestartet.

9. Geben Sie auf der Seite **Beschreibung** die folgenden Einstellungen an, und wählen Sie **Weiter** aus:

    - Name: **Benutzerdefiniert eingehend aus AD – Catchall-Filter**

    - Beschreibung: **Benutzerdefinierte eingehende Regel – schließt alle Benutzer mit UPN aus, die nicht mit der benutzerdefinierten Azure AD-Domäne übereinstimmen**

    - Verbundenes System: **corp.contoso.com**

    - Objekttyp des verbundenen Systems: **Benutzer**

    - Metaverse-Objekttyp: **Person**

    - Verknüpfungstyp: **Join**

    - Rangfolge: **51**

    - Tag: **Leer lassen**

    - Kennwortsynchronisierung aktivieren: **Leer lassen**

    - Deaktiviert: **Leer lassen**


10. Wählen Sie auf der Seite **Bereichsfilter** die Option **Weiter** aus.

11. Wählen Sie auf der Seite **Verknüpfungsregeln** die Option **Weiter** aus.

12. Wählen Sie auf der Seite **Transformationen** die Option **Transformation hinzufügen** aus, geben Sie Folgendes an, und wählen Sie **Hinzufügen** aus:

    - FlowType: **Constant**

    - Zielattribut: **cloudFiltered**

    - Quelle: **True**

13. Wenn ein **Warnungsdialogfeld** mit der Meldung **A full import and full synchronization will be run on 'corp.contoso.com' during your next synchronization cycle** angezeigt wird, wählen Sie **OK** aus.

    >**Hinweis**: Dadurch sollten Sie zurück zur Schnittstellen **View and manage your synchronization rules** gelangen, wobei die neue Regel oben in der Regelliste aufgeführt ist. 

### Aufgabe 9: Initiieren und Überprüfen der Verzeichnissynchronisierung

1. Doppelklicken Sie in der Remotedesktopsitzung auf **DC1** auf die Desktopverknüpfung **Azure AD Connect**.

2. Wählen Sie auf der Seite **Willkommen bei Azure AD Connect** die Option **Weiter** aus. 

3. Wählen Sie auf der Seite **Weitere Aufgaben** die Option **Synchronisierungsoptionen anpassen** aus, und wählen Sie **Weiter** aus.

4. Melden Sie sich auf der Seite **Mit Azure AD verbinden** mit den Anmeldeinformationen des Kontos **john.doe** an, und wählen Sie **Weiter** aus.

5. Wählen Sie auf der Seite **Verzeichnisse verbinden** die Option **Weiter**.

6. Wählen Sie auf der Seite **Filtern von Domänen und Organisationseinheiten** die Option **Weiter**. 

7. Übernehmen Sie auf der Seite **Optionale Features** die Standardeinstellungen, und wählen Sie **Weiter** aus.

8. Wählen Sie auf der Seite **Einmaliges Anmelden aktivieren** die Option **Weiter** aus.

9. Aktivieren Sie auf der Seite **Bereit zur Konfiguration** das Kontrollkästchen **Starten Sie den Synchronisierungsvorgang, nachdem die Konfiguration abgeschlossen wurde**, und wählen Sie **Konfigurieren** aus.

10. Wählen Sie auf der Seite **Konfiguration abgeschlossen** die Option **Beenden** aus.

11. Navigieren Sie in der Remotedesktop-Sitzung auf **DC1** im Edge-Browserfenster mit dem Azure-Portal, zur Seite **Benutzer – Alle Benutzer** des Azure AD-Mandanten „Contoso“.

12. Beachten Sie auf der Seite **Benutzer – Alle Benutzer**, dass die Liste der Benutzerobjekte alle Benutzerkonten mit dem UPN-Suffix enthält, das dem benutzerdefinierten Domänennamen des Azure AD-Mandanten entspricht. Möglicherweise müssen Sie die Seite aktualisieren oder einige Minuten warten, bis die Änderung angezeigt wird.

13. Navigieren Sie im Azure-Portal zur Seite **Gruppen – Alle Gruppen** des Azure AD-Mandanten „Contoso“, und beachten Sie, dass alle corp.contoso.com-Domänengruppen ebenfalls synchronisiert wurden. 

14. Navigieren Sie im Azure-Portal zur Seite **Contoso – Azure AD Connect**, und wählen Sie auf der linken Seite **Azure AD Connect** aus. Vergewissern Sie sich, dass die folgenden Einstellungen festgelegt sind: 

    - Azure AD Connect Sync Status: **Aktiviert** 
  
    - Letzte Synchronisierung: **Dies sollte ein Zeitstempel**. 
  
    - Kennworthashsynchronisierung: **Deaktiviert** 
  
    - Partnerverbund: **Deaktiviert**
   
    - Nahtloses einmaliges Anmelden: **Für 1 Domäne aktiviert** 
  
    - Passthrough-Authentifizierung: **Mit 1 Agent aktiviert**

   > **Hinweis**: In einer Produktionsumgebung würden Sie aus Redundanzgründen zusätzliche Agents installieren. Weitere Informationen finden Sie unter <https://docs.microsoft.com/en-us/azure/active-directory/hybrid/how-to-connect-pta-quick-start>.

### Aufgabe 10: Konfigurieren Hybrid-Azure AD-Einbindung

In dieser Aufgabe konfigurieren Sie Synchronisierungsoptionen für Azure AD Connect-Geräte.

1. Doppelklicken Sie in der Remotedesktopsitzung auf **DC1** auf die Desktopverknüpfung **Azure AD Connect**.

2. Wählen Sie auf der Seite **Willkommen bei Azure AD Connect** die Option **Weiter** aus. 

3. Wählen Sie auf der Seite **Zusätzliche Aufgaben** die Option **Geräteoptionen konfigurieren** und dann **Weiter** aus.

4. Überprüfen Sie auf der Seite **Übersicht** die Information zu **Hybrid-Azure AD-Einbindung** und **Geräterückschreiben**, und wählen Sie **Weiter** aus.

5. Melden Sie sich auf der Seite **Mit Azure AD verbinden** mit den Anmeldeinformationen des Kontos **john.doe** an, und wählen Sie **Weiter** aus.

6. Vergewissern Sie sich, dass auf der Seite **Geräteoptionen** die Option **Hybrid-Azure AD-Einbindung konfigurieren** aktiviert ist, und wählen Sie **Weiter** aus. 

7. Aktivieren Sie auf der Seite **Gerätebetriebssysteme** die Kontrollkästchen **In die Domäne eingebundene Geräte mit Windows 10 oder höher** und **Supported Windows down-level domain-joined devices**, und wählen Sie **Weiter** aus. 

   > **Hinweis**: Kompatible Windows-Geräte werden nur unterstützt, wenn Sie nahtloses SSO für verwaltete Domänen oder einen Partnerverbunddienst wie AD FS für Verbunddomänen Verbund verwenden.

8. Aktivieren Sie auf der Seite **SCP-Konfiguration** das Active Directory-Gesamtstruktur-Kontrollkästchen **corp.contoso.com**, wählen Sie den Eintrag **Azure Active Directory** in der Dropdownliste **Authentifizierungsdienst** aus, und wählen Sie **Hinzufügen** aus.

9. Wenn Sie im Dialogfeld **Windows-Sicherheit** zur Eingabe von Anmeldeinformationen für den Unternehmensadministrator für corp.contoso.com aufgefordert werden, melden Sie mit dem Benutzernamen **CORP\\demouser** und dem Kennwort **demo\@pass123** an.

10. Zurück auf der Seite **SCP-Konfiguration** wählen Sie die Option **Weiter** aus.

11. Wählen Sie auf der Seite **Bereit für Konfiguration** die Option **Konfigurieren**.

12. Überprüfen Sie auf der Seite **Konfiguration abgeschlossen**, ob die Aufgabe erfolgreich abgeschlossen wurde, und wählen Sie **Beenden** aus.


### Aufgabe 11: Durchführen der Hybrid-Azure AD-Einbindung

1. Bestätigen Sie auf dem Lab-Computer im Azure-Portal, dass Sie beim Azure AD-Mandanten angemeldet sind, der dem Azure-Abonnement zugeordnet ist, in dem Sie in den Übungen „Vor dem Praxislab“ Ressourcen (im **Standardverzeichnis**) bereitgestellt haben. Wählen Sie andernfalls das Symbol **Verzeichnis + Abonnement** in der Symbolleiste des Azure-Portal (rechts neben dem Symbol **Cloud Shell**) aus, um zu diesem Azure AD-Mandanten zu wechseln. 

2. Navigieren Sie im Azure-Portal zur Seite der VM **APP1**.

3. Stellen Sie auf der Seite der VM **APP1** über Remotedesktop eine Verbindung mit **APP1** her. Wenn Sie aufgefordert werden, sich anzumelden, verwenden Sie den Benutzernamen **AGAyers\@<benutzerdefinierter_Domänenname>** mit dem Kennwort **demo@pass123** (wobei der Platzhalter **<benutzerdefinierter_Domänenname>** den benutzerdefinierten DNS-Domänennamen darstellt, den Sie früher in dieser Übung dem Azure AD-Mandanten „Contoso“ zugewiesen haben.

4. Starten Sie in der Remotedesktopsitzung auf **APP1** im **Server-Manager-Fenster** die **Aufgabenplanung** unter **Tools**. 


5. Navigieren Sie in der Konsole **Aufgabenplanung** zu **Aufgabenplanungsbibliothek** > **Microsoft** > **Windows** > **Workplace Join**. Aktivieren Sie dann die Ausführung der Aufgabe **Automatic-Device-Join**. 


6. Wechseln Sie zur Remotedesktopsitzung auf **DC1**, und starten Sie im Konsolenbereich des Fensters „Windows PowerShell ISE“ die Deltasynchronisierung für Azure AD Connect, indem Sie Folgendes ausführen:

   ```pwsh
   Import-Module -Name 'C:\Program Files\Microsoft Azure AD Sync\Bin\ADSync\ADSync.psd1'
   
   Start-ADSyncSyncCycle -PolicyType Delta
   ```

7. Wechseln Sie zurück zur Remotedesktopsitzung auf **APP1**, und starten Sie eine **Eingabeaufforderung**.

8. Überprüfen Sie im Eingabeaufforderungsfenster den Azure AD-Registrierungsstatus von APP1, indem Sie Folgendes ausführen: 

   ```
   dsregcmd /status
   ```

9. Die Ausgabe des Befehls sieht in etwa wie im folgenden Beispiel aus:

   ```
   +----------------------------------------------------------------------+
   | Device State                                                         |
   +----------------------------------------------------------------------+

        AzureAdJoined : YES
     EnterpriseJoined : NO
             DeviceId : 61eea2b8-efbe-43d9-b267-126433c8ee34
           Thumbprint : BBAAA0FB4A55E880388851BED955A2669A961A96
       KeyContainerId : 2eb75eb8-0a1d-437b-99d9-9dd161ca0d90
          KeyProvider : Microsoft Software Key Storage Provider
         TpmProtected : NO
         KeySignTest: : PASSED
                  Idp : login.windows.net
             TenantId : xxxxxxx-xxxx-xxx-xxxx-xxxxxxxxxx
           TenantName : xxxxxxx-xxxx-xxx-xxxx-xxxxxxxxxx
          AuthCodeUrl : https://login.microsoftonline.com/xxxxxxx-xxxx-xxx-xxxx-xxxxxxxxxx/oauth2/authorize
       AccessTokenUrl : https://login.microsoftonline.com/xxxxxxx-xxxx-xxx-xxxx-xxxxxxxxxx/oauth2/token
               MdmUrl :
            MdmTouUrl :
     MdmComplianceUrl :
          SettingsUrl :
       JoinSrvVersion : 1.0
           JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/
            JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net
        KeySrvVersion : 1.0
            KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/
             KeySrvId : urn:ms-drs:enterpriseregistration.windows.net
         DomainJoined : YES
           DomainName : CORP

   +----------------------------------------------------------------------+
   | User State                                                           |
   +----------------------------------------------------------------------+

               NgcSet : NO
      WorkplaceJoined : NO
        WamDefaultSet : NO
           AzureAdPrt : NO

   +----------------------------------------------------------------------+
   | Ngc Prerequisite Check                                               |
   +----------------------------------------------------------------------+

        IsUserAzureAD : NO
        PolicyEnabled : NO
       DeviceEligible : YES
   SessionIsNotRemote : NO
     X509CertRequired : NO
         PreReqResult : WillNotProvision

   ```
11. Wechseln Sie zurück zur Remotedesktopsitzung auf **DC1**, navigieren Sie im Edge-Browserfenster mit dem Azure-Portal zur Seite **Geräte – Alle Geräte** des Azure AD-Mandanten „Contoso“, und bestätigen Sie, dass ein Eintrag vorhanden ist, der den APP1-Server darstellt, wobei der **Verknüpfungstyp** auf **In Hybrid-Azure AD eingebunden** festgelegt ist.

   > **Hinweis**: Möglicherweise müssen Sie warten, bis der Azure AD-Registrierungsstatus richtig gemeldet wird und das Azure AD-Objekt im Azure-Portal angezeigt wird.


