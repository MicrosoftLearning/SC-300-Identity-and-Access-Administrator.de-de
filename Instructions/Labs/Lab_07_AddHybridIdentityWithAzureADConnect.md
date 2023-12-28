---
lab:
  title: 07 – Optionaler --- Hinzufügen von Hybrididentität mit Microsoft Entra Verbinden
  learning path: '01'
  module: Module 01 - Implement an identity management solution
---

# Übung 07: OPTIONALer --- Hinzufügen von Hybrididentität mit Microsoft Entra Verbinden



# Diese Funktion ist derzeit nicht verfügbar.  Aufgrund einer Lizenzierungsänderung in der Microsoft Entra-ID ist das Lab fehlgeschlagen.  Wir behandeln derzeit problembehebung und aktualisieren das Labor und sollten es innerhalb einer Woche wieder online haben.  Wechseln Sie zur nächsten Übung.




**Hinweis** : Für dieses Lab ist ein Azure Pass erforderlich. Anweisungen finden Sie in Lab 00.

**Hinweis 2** : Diese Übung ist optional.  Es dauert mindestens 1 Stunde, bis sie abgeschlossen ist und erfordert, dass Sie in Den Laborschritten detailliert beschrieben sind.  Bitte zögern Sie nicht, es zu computern, wenn die Zeit dies zulässt.  Wenn Ihr Unternehmen seine Hybridkonfiguration bereits eingerichtet hat oder Sie nicht beabsichtigen, Microsoft Entra Verbinden zu verwenden, springen Sie bitte über dieses Labor.

## Labszenario

Ihr Unternehmen verfügt über eine lokale AD DS-Domäne (Active Directory Domain Services).  Sie möchten weiterhin lokales Active Directory als Identitäts- und Zugriffsverwaltungslösung verwenden, aber auch die Möglichkeit erfordern, dass Benutzer auf Cloudanwendungen mit demselben Benutzernamen und Kennwort zugreifen können.

#### Geschätzte Zeit: 60 Minuten.

### Übung 1 – Einrichten der lokalen Infrastruktur

#### Aufgabe 1 – Erstellen der lokales Active Directory-Infrastruktur

1. Auf die Bereitstellungsvorlage kann unter diesem Link zugegriffen werden: [Leitfaden zur](https://github.com/maxskunkworks/TLG/tree/master/tlg-base-config_3-vm) lokalen Testumgebung.

    **Hinweis zu Lernenden und MCTs** – Die Bereitstellung dieser Vorlage kann 30-60 Minuten dauern. Seien Sie also bereit, bei diesem Schritt eine Pause zu unternehmen oder die Bereitstellung vor einem Vorlesungsabschnitt des Kurses auszuführen.

    **Hinweis zu Lab-Anbietern** – Wenn möglich, ist es hilfreich, dass Schüler/Studenten das Setup der Lab-Umgebung abschließen und bereitstellen können.

2. Wählen Sie auf der **Seite "TLG (Test Lab Guide) – 3 VM Base Configuration (v1.0)"** die Option **"In Azure** bereitstellen" aus.

   **Hinweis**: Die 3 VM-Basiskonfiguration stellt einen Windows Server 2016 Active Directory-Do Standard Controller mit dem Namen DC1 bereit Standard den Sie angeben, und einen do Standard Memberserver mit dem Namen APP1 unter Windows Server 2016. Es bietet auch eine Option zum Bereitstellen einer Client-VM unter Windows 10, wir verwenden sie jedoch nicht in unserem Labor (in erster Linie aufgrund von Lizenzierungsanforderungen, die bei der Ausführung von Windows 10-VMs in Azure gelten). Der Do Standard Memberserver (APP1) hat .NET 4.5 und IIS automatisch installiert.  
   
   **Hinweis** : Der virtuelle Computer, der für dieses Lab erforderlich ist, ist **DC1**.  Wenn Sie einen Azure Pass verwenden, gibt es eine Einschränkung von 2 VMs, sodass der virtuelle Clientcomputer fehlschlägt.  Dies ist für diesen Artikel nicht erforderlich.

3. Geben Sie auf der Seite "**Benutzerdefinierte Bereitstellung**" die folgenden Einstellungen an, und wählen Sie **dann "Überprüfen" und dann "**Erstellen**"** aus.

   -   Abonnement: Der Name des Azure-Zielabonnements, in dem Sie die Azure-VMs der Lab-Umgebung bereitstellen möchten.
   -   Ressourcengruppe: (Neue) **Hybrididentity-RG erstellen**
   -   Speicherort: Der Name der Azure-Region, die die Azure-VMs der Lab-Umgebung hosten soll.
   -   Konfigurationsname: **TlgBaseConfig-01**
   -   Rootdomänenname = corp.contoso.com
   -   Serverbetriebssystem: **2016-Datacenter**
   -   Administratorbenutzername: **Demouser**
   -   Administratorkennwort: **Geben Sie ein sicheres Kennwort ein, das Sie sich merken werden.**
   -   Bereitstellen eines virtuellen Clientcomputers: **Nein**
   -   Client-VHD-URI: **Leer lassen**
   -   VM-Größe: **Standard_D2s_v3**
   
   **Hinweis** : Verwenden Sie eine ähnliche VM-Größe, wenn Ihr Abonnement die aufgeführte Größe nicht unterstützt. Die Dokumentation ist hier verknüpft: <https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sizes>.

   -   DNS-Bezeichnungspräfix: **Jeder gültige, global eindeutige DNS-Name (eine eindeutige Zeichenfolge bestehend aus Buchstaben, Ziffern und Bindestrichen, beginnend mit einem Buchstaben und bis zu 47 Zeichen lang).**

   -   _artifacts Speicherort: **Übernehmen Sie die Standardeinstellung**
   -   _artifacts Location Sas Token: Lassen Sie diese Angabe leer.

4. Klicken Sie auf **Überprüfen + erstellen**.

5. Wählen Sie nach erfolgreicher Überprüfung **Erstellen** aus.
    
6. Warten Sie, bis die Bereitstellung abgeschlossen ist. Dies kann etwa zehn Minuten dauern.


### Aufgabe 2 : Konfigurieren der Lab-Umgebung für Azure-VMs

1. Navigieren Sie im Browserfenster, in dem die Azure-Portal angezeigt wird, zur **Azure-VM DC1**, und stellen Sie eine Verbindung über Remotedesktop her. Wenn Sie dazu aufgefordert werden, melden Sie sich mit den folgenden Anmeldeinformationen an:

   -   Benutzername: **Demouser**
   -   Kennwort: **Verwenden Des sicheren Kennworts, das Sie in Aufgabe 1 erstellt haben**

2.  Starten Sie **in der Remotedesktopsitzung auf **DC1** Windows PowerShell ISE**, und öffnen Sie dann den Skriptbereich.  Fügen Sie als Nächstes das folgende Skript zum Skriptbereich hinzu, und führen Sie es aus, um die erweiterte Sicherheitskonfiguration von Internet Explorer und die Benutzerzugriffskontrolle sowohl auf DC1- als **auch **AUF APP1-Azure-VMs**** zu deaktivieren:

    ```pwsh

    $vmNames = @('dc1','app1')
    Invoke-Command -ComputerName $vmNames {Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Active Setup\Installed Components\{A509B1A7-37EF-4b3f-8CFC-4F3A74704073}" -Name "IsInstalled" -Value 0}
    Invoke-Command -ComputerName $vmNames {Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Active Setup\Installed Components\{A509B1A8-37EF-4b3f-8CFC-4F3A74704073}" -Name "IsInstalled" -Value 0}
    Invoke-Command -ComputerName $vmNames {Set-ItemProperty "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" -Name "ConsentPromptBehaviorAdmin" -Value 00000000}
    ```

    **Hinweis:** Wenn Sie mehrere PowerShell-Skripts in derselben Datei ausführen möchten, können Sie ein bestimmtes Skript hervorheben und neben der grünen Wiedergabeschaltfläche "Auswahl** ausführen" auswählen**. 

3.  Fügen Sie im **Windows PowerShell ISE-Fenster** das folgende Skript zum Skriptbereich hinzu, und führen Sie es aus, um Remoteserver-Verwaltungstools sowohl auf **DC1 als **auch AUF APP1*** Azure-VMs zu installieren:

    ```pwsh

    $vmNames = @('dc1','app1')
    Invoke-Command -ComputerName $vmNames {Install-WindowsFeature RSAT -IncludeAllSubFeature} 
    ```

4.  Fügen Sie im **Windows PowerShell ISE-Fenster** das folgende Skript zum Skriptbereich hinzu, und führen Sie es aus, um TLS 1.2 sowohl auf **DC1- als **auch AUF APP1-Azure-VMs*** zu aktivieren:

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

5.  Fügen Sie im **Windows PowerShell ISE-Fenster** das folgende Skript zum Skriptbereich hinzu, und führen Sie es aus, um die integrierte Windows-Authentifizierung auf der Standardwebsite zu konfigurieren, die auf der **Azure-VM APP1** gehostet wird:

    ```pwsh

    $vmNames = @('app1')
    Invoke-Command -ComputerName $vmNames {Enable-WindowsOptionalFeature -Online -FeatureName IIS-WindowsAuthentication}
    Invoke-Command -ComputerName $vmNames {Set-WebConfigurationProperty -Filter "/system.webServer/security/authentication/anonymousAuthentication" -Name Enabled -Value False -PSPath IIS:\ -Location "Default Web Site"}
    Invoke-Command -ComputerName $vmNames {Set-WebConfigurationProperty -Filter "/system.webServer/security/authentication/windowsAuthentication" -Name Enabled -Value True -PSPath IIS:\ -Location "Default Web Site"}
    ```

### Aufgabe 3 – Starten Sie die Azure-VMs neu

1. **Führen Sie im Windows PowerShell ISE-Fenster** im Konsolenbereich Folgendes aus, um APP1** neu zu starten**:

    ```pwsh

    Restart-Computer -ComputerName 'APP1'
    ```

2. **Führen Sie im Windows PowerShell ISE-Fenster** im Konsolenbereich folgendes aus, um DC1** neu zu starten**:

    ```pwsh
    Restart-Computer -ComputerName 'DC1'
    ```

### Aufgabe 5 – Konfigurieren von contoso.local Active Directory

1. Verbinden erneut zum **DC1** Azure VM über Remotedesktop. Wenn Sie dazu aufgefordert werden, melden Sie sich mit den folgenden Anmeldeinformationen an:

    -   Benutzername: **Demouser**

    -   Kennwort: **Demo\@pass123**
       - **Es wird dringend empfohlen, ein sicheres Kennwort einzugeben, das Sie sich merken können.**

2.  Starten Sie Internet Explorer in der Remotedesktopsitzung auf **DC1**, und navigieren Sie zu dem nachstehenden Link.

    ```
    https://github.com/microsoft/MCW-Hybrid-identity/tree/main/Archive/Hands-on%20lab/studentfiles
    ```

3. Wählen Sie auf der **Seite "Benutzer/Gruppe für Active Directory Demo/TestUmgebung** erstellen" den **Link "CreateDemoUsers.ps1** " aus, akzeptieren Sie die Lizenzbedingungen, und speichern Sie das entsprechende Skript im lokalen Dateisystem.

4. Wählen Sie auf der **Seite "Benutzer/Gruppe für Active Directory Demo/TestUmgebung** erstellen" den **Link "CreateDemoUsers.csv** " (direkt über dem PowerShell-Codeabschnitt) aus, und speichern Sie die entsprechende CSV-Datei an demselben Speicherort wie die **Datei "CreateDemoUsers.ps1** ".

5. Starten Sie in der Remotedesktopsitzung auf **DC1** Explorer, navigieren Sie zu dem Ordner, in dem Sie beide Dateien heruntergeladen haben. Wählen Sie in der Datei **"CreateDemoUsers.ps1**" die Option "Eigenschaften" aus, aktivieren **Sie im **Dialogfeld "** Eigenschaften erstellenDemoUsers.ps1**" das **Kontrollkästchen "Blockierung** aufheben", und aktivieren Sie **"OK**".

6. Wählen Sie im fenster Explorer die Datei **"CreateDemoUsers.ps1**" erneut aus, und wählen Sie "Bearbeiten" aus****. 

7. Ändern Sie im Fenster "Administrator: Windows PowerShell ISE **" die **Zeile **148** von:

    ```pwsh
    $UserCount = 1000 #Up to 2500 can be created
    ```

   Bis
    ```pwsh
    $UserCount = 2500 #Up to 2500 can be created
    ```

8. Speichern Sie im **Windows PowerShell ISE-Fenster** die Änderung, und führen Sie das **Skript CreateDemoUsers.ps1** aus, um eine Organisationseinheitshierarchie der Laborumgebung zu erstellen und mit Testbenutzerkonten aufzufüllen. 

9.  Fügen Sie im **Windows PowerShell ISE-Fenster** das folgende Skript zum Skriptbereich hinzu, und führen Sie es aus, um die Einstellungen der AD-Benutzerkonten zu ändern, die Sie in dieser Übung verwenden werden:

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

10. Fügen Sie im **Windows PowerShell ISE-Fenster** das folgende Skript zum Skriptbereich hinzu, und führen Sie es aus, um zusätzliche Organisationseinheiten mit dem Namen **"Server** und **Clients** " zu erstellen und das **APP1-Computerkonto** auf den ersten davon zu verschieben:

    ```pwsh

    New-ADOrganizationalUnit -Name 'Servers' -Path 'OU=Demo Accounts,DC=corp,DC=contoso,DC=com'
    New-ADOrganizationalUnit -Name 'Clients' -Path 'OU=Demo Accounts,DC=corp,DC=contoso,DC=com'

    Move-ADObject -Identity 'CN=APP1,CN=Computers,DC=corp,DC=contoso,DC=com' -TargetPath 'OU=Servers,OU=Demo Accounts,DC=corp,DC=contoso,DC=com'
    ```

11. Sign-out From AAD (Von AAD abmelden)

## Übung 3: Synchronisieren einer Active Directory-Gesamtstruktur mit einem Azure Active Directory-Mandanten

### Aufgabe 1: Erstellen eines Azure Active Directory-Mandanten und Aktivieren einer EMS E5-Testversion

In dieser Aufgabe erstellen Sie einen Azure Active Directory-Mandanten mit den folgenden Einstellungen: 

-   Organisation: Contoso

-   Initial do Standard name: Any valid, unique do Standard name.

-   Land oder Region: USA

1. Starten Sie auf dem Lab-Computer ein neues Webbrowserfenster, und navigieren Sie zu der Azure-Portal, <https://portal.azure.com> sofern sie noch nicht geschehen ist.

2. Melden Sie sich bei dem Azure-Abonnement an, in dem Sie Ressourcen in den Übungen "Before Hands-On Lab" bereitgestellt haben.

3. Wählen Sie im Menü des Azure-Portals auf der Startseite die Option + Ressource erstellen aus.

4. Geben Sie auf der **Seite "Neu**" im **Textfeld "Marketplace** durchsuchen" Azure Active Directory** ein, und wählen Sie in der Ergebnisliste Azure Active Directory** aus**.**

5. Wählen Sie auf der Seite **Anmelden** die Option **Azure Active Directory B2C** aus.

6. Geben Sie auf der Seite **Autorisierung erstellen** die folgenden Einstellungen ein, und wählen Sie **Erstellen** aus:

Registerkarte "Einfach":
    -   Wählen Sie unter „Mandantentyp“ die Option **Azure Active Directory** aus.

Registerkarte „Konfiguration“
    -   Organisation: Contoso

    -   Initial do Standard name: Any valid, unique do Standard name.

    -   Land oder Region: USA

7. Öffnen Sie **Nach der Erstellung Azure Active Directory**.

8. Wählen Sie auf der Seite Übersicht die Option Mandanten verwalten aus.

9. Setzen Sie ein Einchecken Ihres neu erstellten Verzeichnisses ein.

10. Wählen Sie im oberen Seitenbereich die Option **Hinzufügen** aus.

    >Beachten Sie, dass es einige Minuten dauern kann, bis alles angezeigt wird.

11. Wählen Sie auf der Seite **Übersicht** die Option **Benutzer** aus.

12. Beachten Sie, dass Sie nur über einen einzelnen ExternalAzureAD-Benutzer in diesem neuen Mandanten verfügen.

### Aufgabe 2: Erstellen und Konfigurieren des Azure AD-Benutzers zum Verwalten dieses Verzeichnisses

1. Navigieren Sie vom Laborcomputer in der Azure-Portal zurück zur **Seite "Contoso – Übersicht"**.

2. Wählen Sie auf der **Seite "Contoso – Übersicht**" unter "**Benutzer** verwalten**" in der linken Navigationsleiste **aus.

3. Klicken Sie auf dem Blatt Benutzer  Alle Benutzer auf den Eintrag, der Ihr Benutzerkonto darstellt.

4. Wählen Sie auf der Seite **Profil bearbeiten** die Option **Konto löschen** aus.

5. Wählen Sie im **Abschnitt Einstellungen** in der **Dropdownliste "Verwendungsort**" den **Eintrag USA** aus, und wählen Sie "Speichern"** aus**.

#### Erstellen des neuen Administrators

6. Stellen Sie auf dem Blatt Neuer Benutzer sicher, dass die Option Benutzer erstellen ausgewählt ist, und geben Sie die folgenden Einstellungen an:

    - Benutzername: **john.doe *@your Azure AD-Mandant Standard Name* ** wobei ***Ihr Azure AD-Mandant die Standard Do Standard Name*** ist, den Sie beim Erstellen des Azure AD-Mandanten von Contoso angegeben haben.

    - Name: **john.doe**

    - Vorname: Jane

    - De Nachname.
    
    - Kennwort: **Kennwort automatisch generieren**
    
    - Kennwort anzeigen: **Aktiviert** , stellen Sie sicher, dass Sie das Kennwort kopieren.

    - Gruppen: **0 Gruppe ausgewählt**
    
    - Rolle: Globaler Administrator
    
    - Anmeldung blockieren: **Nein**
    
    - Verwendungsort: **USA**
    
    - Position: **Leer lassen**
    
    - Abteilung: **Leer lassen**

    > **Hinweis**: Kopieren Sie die Werte für **Benutzername** und **Kennwort** in Editor. Sie werden sie später in diesem Lab benötigen.


### Aufgabe 5: Konfigurieren des DNS-Suffix in der Contoso Active Directory-Gesamtstruktur

In dieser Aufgabe konfigurieren Sie das DNS-Suffix der Contoso Active Directory-Gesamtstruktur so, dass sie mit dem neu überprüften benutzerdefinierten Azure AD-Vorgang übereinstimmt Standard Name.

1. Überprüfen Sie auf dem Laborcomputer im Azure-Portal, dass Sie beim Azure AD-Mandanten angemeldet sind, der dem Azure-Abonnement zugeordnet ist, in dem Sie Ressourcen in den Übungen "Before Hands-On Lab" (Standardverzeichnis****) bereitgestellt haben. Wählen Sie andernfalls das **Symbol "Verzeichnis + Abonnement**" in der Symbolleiste des Azure-Portal (rechts neben dem **Cloud Shell-Symbol**) aus, um zu diesem Azure AD-Mandanten zu wechseln. 

2. Navigieren Sie im Azure-Portal zur Übersichtsseite Ihrer VM.

3. Stellen Sie auf der Seite " **VIRTUELLER COMPUTER DC1** " über Remotedesktop eine Verbindung mit **DC1** her. Wenn Sie zur Anmeldung aufgefordert werden, verwenden Sie den **Demousernamen** und das **Demo\@pass123-Kennwort** . 

4. Starten Sie in der Remotedesktopsitzung auf DC1 im fenster Server-Manager** die **Konsole "Active Directory-Domäne s and Trusts**" unter **"Tools**".****** 

5. Wählen Sie **in der Konsole Active Directory-Domäne s und Vertrauensstellungen** auf der **linken Seite Active Directory-Domäne s und Vertrauensstellungen [DC1.corp.contoso.com]** aus, und wählen Sie "Eigenschaften"** aus**.

6. Geben Sie auf der **Registerkarte "UPN-Suffixe**" des **Fensters "Active Directory-Domäne" und "Trusts[DC1.corp.contoso.com]"** im Textfeld "**Alternative UPN-Suffixe**" den Namen des benutzerdefinierten Vorgangs ein Standard sie in der vorherigen Aufgabe überprüft haben, wählen Sie **"Hinzufügen"** und dann "OK **" aus**.

7. Starten Sie in der Remotedesktopsitzung auf **DC1** im **fenster Server-Manager** die **Active Directory-Benutzer und -Computer** Konsole unter **"Extras**". 

8. Erweitern Sie **in der **Active Directory-Benutzer und -Computer** Konsole corp.contoso.com** auf der linken Seite, und überprüfen Sie die Organisationseinheitshierarchie der Do Standard und die Gruppenmitgliedschaft der Do Standard gruppen. 

9.  Starten Sie in der Remotedesktopsitzung auf **DC1** Windows PowerShell ISE, und führen Sie im Skriptbereich Folgendes aus, um das UPN-Suffix aller Benutzer zu ersetzen, die Mitglieder der **Engineering-Gruppe** sind, durch den Namen der benutzerdefinierten überprüften Aufgabe Standard Name des Contoso Azure AD-Mandanten (ersetzen Sie den Platzhalter `<custom_domain_name>` durch den tatsächlichen Namen des benutzerdefinierten überprüften Do Standard Namens, den Sie dem Contoso Azure AD-Mandanten zugewiesen haben. 

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

### Installieren Sie Microsoft Entra Connect.

In dieser Aufgabe installieren Sie Microsoft Entra Verbinden.

1. Wählen Sie **in der Remotedesktopsitzung auf **DC1** in Server-Manager den lokalen Server** aus, und stellen Sie sicher, dass **die erweiterte IE-Sicherheitskonfiguration** deaktiviert ist. Andernfalls wählen Sie den **Link "Ein**" neben **der erweiterten Sicherheitskonfiguration** von IE aus, legen Sie die **Administratoreinstellungen** auf **"Aus"** fest, und wählen Sie "OK **" aus**.

2. Öffnen Sie innerhalb der Remotedesktopsitzung auf **DC1** das **Windows PowerShell ISE-Fenster** , und führen Sie diesen Befehl aus, um den Chrome-Browser zu installieren.

    ```pwsh
    $LocalTempDir = $env:TEMP; $ChromeInstaller = "ChromeInstaller.exe"; (new-object System.Net.WebClient).DownloadFile('http://dl.google.com/chrome/install/375.126/chrome_installer.exe', "$LocalTempDir\$ChromeInstaller"); & "$LocalTempDir\$ChromeInstaller" /silent /install; $Process2Monitor = "ChromeInstaller"; Do { $ProcessesFound = Get-Process | ?{$Process2Monitor -contains $_.Name} | Select-Object -ExpandProperty Name; If ($ProcessesFound) { "Still running: $($ProcessesFound -join ', ')" | Write-Host; Start-Sleep -Seconds 2 } else { rm "$LocalTempDir\$ChromeInstaller" -ErrorAction SilentlyContinue -Verbose } } Until (!$ProcessesFound)
    ```

2. Starten Sie in der Remotedesktopsitzung auf **DC1** den Chrome-Browser, und navigieren Sie zu der Azure-Portal unter <https://portal.azure.com>.

3. Wenn Sie aufgefordert werden, sich anzumelden, geben Sie die Anmeldeinformationen des **Benutzerkontos "john.doe** Microsoft Entra" ein, das Sie weiter oben in dieser Übung in Editor kopiert haben.

4. Geben Sie bei entsprechender Aufforderung das Kennwort für das Benutzerkonto ein. 
  
    > **Hinweis**: Wenn Sie die Nachricht **erhalten, wurde dieses Kennwort zu oft angezeigt. Wählen Sie etwas schwieriger zu erraten**, müssen Sie das Kennwort ändern, bis es eindeutig genug ist, um akzeptiert zu werden.

5. Wenn Sie gefragt werden, ob Sie angemeldet bleiben möchten, wählen Sie **Nein** aus. Sie werden zum Azure-Portal umgeleitet. 

6. Wenn das **Dialogfeld "Willkommen bei Microsoft Azure** " angezeigt wird, wählen Sie **"Vielleicht später" aus**. 

7. Suchen Sie im Azure-Portal nach **Microsoft Entra-ID**.

8. Wählen Sie in den Suchergebnissen **Microsoft Entra ID** aus.

9.  Wählen Sie auf der **Seite "Microsoft Entra Verbinden**" den **Link "Microsoft Entra Verbinden** herunterladen" aus.  Wählen Sie **dann im Menü Verbinden Synchronisieren** aus.

10. Wählen Sie auf der Downloadseite **Microsoft Azure Active Directory Connect** die Option **Herunterladen** aus.

11. Wenn Sie gefragt werden, ob das Installationsprogramm **AzureADConnect.msi** ausgeführt oder gespeichert werden soll, wählen Sie **Ausführen** aus. Dadurch wird die Datei heruntergeladen und der **Microsoft Azure Active Directory-Verbinden-Assistent** automatisch gestartet. 

12. Aktivieren Sie auf der Seite Willkommen bei Azure AD Connect des Assistenten für Microsoft Azure Active Directory Connect das Kontrollkästchen Ich akzeptiere die Lizenzbedingungen und den Datenschutzhinweis., und wählen Sie anschließend Weiter aus.

13. Wählen Sie auf der **Seite "Express Einstellungen**" die **Schaltfläche "Anpassen**" aus.

14. Lassen Sie auf der Seite **Erforderliche Komponenten installieren** alle optionalen Konfigurationsoptionen deaktiviert, und wählen Sie **Installieren** aus.

15. Wählen Sie auf der Seite **Benutzeranmeldung** die Schaltfläche **Passthrough-Authentifizierung** und dann **Einmaliges Anmelden aktivieren** und **Weiter**.

16. Melden Sie sich auf der Verbinden auf der **Azure AD-Seite** mit den Anmeldeinformationen des **John.doe-Kontos** an, und wählen Sie "Weiter"** aus**.

17. Stellen Sie auf der **Seite Verbinden Ihrer Verzeichnisse** sicher, dass der **eintrag corp.contoso.com** in der **Dropdownliste "GESAMTSTRUKTUR**" angezeigt wird, und wählen Sie "Verzeichnis** hinzufügen" aus**. **Stellen Sie im AD-Gesamtstrukturkonto** sicher, dass die **Option "Neues AD-Konto** erstellen" ausgewählt ist, geben **Sie im **Textfeld "ENTERPRISE ADMIN USERNAME"** CORP.CONTOSO.COM\\Demouser** ein, geben Sie im **Textfeld "KENNWORT**" den Befehl **"Demo\@pass123**" ein, und wählen Sie "OK **" aus**.


18. Wählen Sie auf der Seite **Verzeichnisse verbinden** die Option **Weiter**.

19. Stellen Sie auf der **Azure AD-Anmeldekonfigurationsseite** sicher, dass Ihr benutzerdefinierter Vorgang Standard Name als überprüftes **Active Directory-UPN-Suffix** aufgeführt ist und dass der **Eintrag "userPrincipalName**" in der **Dropdownliste "USER PRINCIPAL NAME**" angezeigt wird. Beachten Sie die Warnung, dass **Benutzer sich nicht mit lokalen Anmeldeinformationen bei Azure AD anmelden können, wenn das UPN-Suffix nicht mit einem überprüften Do Standard Namen** übereinstimmt. Aktivieren Sie das **Kontrollkästchen "Weiter", ohne alle UPN-Suffixe zu überprüfen Standard** und wählen Sie "Weiter"** aus**. 

    >**Hinweis**: Dies wird erwartet, da einige Benutzer weiterhin mit dem **UPN-Suffix "contoso.local**" konfiguriert sind, das nicht routingfähig ist und nicht als bestätigter benutzerdefinierter Vorgang konfiguriert werden kann Standard Name eines Azure AD-Mandanten.

20. Wählen Sie auf der **Seite "Do Standard" und "OU-Filterung**" die Option **"Synchronisierung" aus Standard und "OUs**" aus, und stellen Sie dann sicher, dass nur die **OeOs "DemoAccounts**" und alle untergeordneten OUs ausgewählt sind, und wählen Sie "Weiter"** aus**. 


21. Übernehmen Sie auf der Seite **Eindeutige Identifizierung Ihrer Benutzer** die Standardeinstellungen, und wählen Sie **Weiter** aus. 


22. Übernehmen Sie auf der Seite **Benutzer und Geräte filtern** die Standardeinstellungen, und wählen Sie **Weiter** aus. 

23. Übernehmen Sie auf der Seite **Optionale Features** die Standardeinstellungen, und wählen Sie **Weiter** aus.

24. Wählen Sie auf der **Seite "Einmaliges Anmelden** aktivieren" im Dialogfeld "Anmeldeinformationen der **Gesamtstruktur" die Option **"Anmeldeinformationen**** für Gesamtstruktur" aus, melden Sie sich mit dem **benutzernamen** "CORP\\" und **dem Demo\@pass123-Kennwort** an, und wählen Sie "Weiter"** aus**.


25. Vergewissern Sie sich auf der Seite Bereit zur Konfiguration, dass das Kontrollkästchen Starten Sie den Synchronisierungsvorgang, nachdem die Konfiguration abgeschlossen wurde. aktiviert ist, und wählen Sie anschließend Installieren aus.


   > **Hinweis**: Sie konfigurieren die Filterung auf Attributebene, bevor Sie den Synchronisierungsprozess aktivieren.

   > **Hinweis**: Die Installation sollte ungefähr 2 Minuten dauern.

26. Wählen Sie auf der Seite **Konfiguration abgeschlossen** die Option **Beenden**.


### Aktivieren des Active Directory-Papierkorbs

In dieser Aufgabe aktivieren Sie den Papierkorb in Contoso Active Directory Standard. 

1. Starten **Sie in der Remotedesktopsitzung auf **DC1** im Menü "Extras" in der Server-Manager Konsole das Active Directory-Verwaltungscenter**.


2. Wählen Sie **in der Konsole des **Active Directory-Verwaltungscenters** rechts -Corp (lokal)** auf der linken Seite aus, und wählen Sie "**Papierkorb** aktivieren" aus. Wenn eine Bestätigung angefordert wird, klicken Sie auf **OK**.


3. Wenn Sie aufgefordert werden, das AD Administrative Center zu aktualisieren, wählen Sie "OK **" aus**.

   > **Hinweis**: Informationen zu den Vorteilen des Papierkorbs in Hybridszenarien finden Sie unter <https://docs.microsoft.com/en-us/azure/active-directory/hybrid/how-to-connect-sync-recycle-bin>

### Aufgabe 8: Konfigurieren der Azure AD-Verbinden Filterung auf Attributebene

In dieser Aufgabe konfigurieren Sie die Filterung auf Azure AD-Verbinden Attributebene, die die Synchronisierung von Benutzerkonten mit denen mit dem UPN-Suffix mit dem benutzerdefinierten Do Standard Namen des Azure AD-Zielmandanten begrenzt.

   > Die positive Filterung erfordert zwei Synchronisierungsregeln. Einer davon bestimmt den richtigen Bereich der zu synchronisierenden Objekte. Darüber hinaus benötigen Sie eine zweite Catchall-Synchronisierungsregel, die alle Objekte herausfiltert, die noch nicht als ein zu synchronisierendes Objekt identifiziert wurden.

1. Starten Sie innerhalb der Remotedesktopsitzung auf **DC1** den Synchronisierungsregeln-Editor** unter **Azure AD Verbinden** im Menü .**


2. Stellen Sie im Fenster "Synchronisierungsregeln-Editor" auf der **Seite "Synchronisierungsregeln** anzeigen und verwalten" sicher, dass **"Eingehend**" in der **Dropdownliste "Richtung**" angezeigt wird, und wählen Sie "Neue Regel** hinzufügen" aus**. Dadurch wird der **Assistent zum Erstellen eingehender Synchronisierungsregel** gestartet.


3. Geben Sie auf der **Seite "Synchronisierungsregel für eingehende Synchronisierung erstellen – Beschreibung**" die folgenden Einstellungen an, und wählen Sie "Weiter"** aus**:

    - Name: **Benutzerdefiniert aus AD – UPN-Filter**

    - Beschreibung: Benutzerdefinierte eingehende Regel – **enthält Benutzer mit UPN, die auf die benutzerdefinierte Azure AD-Aufgabe festgelegt sind Standard**

    - Verbinden ed System: **corp.contoso.com**

    - Objekttyp des verbundenen Systems: Benutzer

    - Metaverse-Objekttyp: Person

    - Verknüpfungstyp: Join

    - Rangfolge: **50**

    - Tag: Lassen Sie dieses Feld leer.

    - Kennwortsynchronisierung aktivieren: **Leer lassen**

    - Deaktiviert: **Leer lassen**


4. Wählen Sie auf der **Seite "Eingehende Bereichsdefinitionsfilter** erstellen" die Option **"Gruppe** hinzufügen" aus, wählen Sie "Klausel** hinzufügen" aus, geben **Sie Folgendes an, und wählen Sie "Weiter"** aus**:

    - Zielattribut: userPrincipalName

    - Operator: EndsWith

    - Wert: **\@\<your custom domain name>**

5. Wählen Sie auf der Seite **Verknüpfungsregeln** die Option **Weiter** aus.

6. Wählen Sie auf der **Seite "Transformationen**" die Option **"Transformation** hinzufügen" folgendes aus, und wählen Sie "Hinzufügen"** aus**:

    - FlowType: Konstant

    - Target-Attribut: **cloudFiltered**

    - Quelle: **False**

7. **Wenn ein Dialogfeld "Warnung**" angezeigt wird, in dem die Meldung angezeigt wird, dass **während des nächsten Synchronisierungszyklus** ein vollständiger Import und eine vollständige Synchronisierung auf "corp.contoso.com" ausgeführt werden, wählen Sie **"OK**" aus.

   > **Hinweis**: Dies sollte Sie zurück zur Ansicht bringen und Ihre Synchronisierungsregelnschnittstelle verwalten, wobei die neue Regel oben in der Regelliste aufgeführt ist. 

8. Stellen Sie wieder im **Fenster "Synchronisierungsregeln-Editor**" auf der **Seite "Synchronisierungsregeln** anzeigen und verwalten" sicher, dass **"Eingehend**" in der **Dropdownliste "Richtung**" angezeigt wird, und wählen Sie erneut "Neue Regel** hinzufügen" aus**. Dadurch wird der **Assistent zum Erstellen eingehender Synchronisierungsregel** gestartet.

9. Geben Sie auf der Seite **Beschreibung** Folgendes ein, und wählen Sie anschließend **Weiter** aus:

    - Name: **Benutzerdefiniert aus AD – Catch-all-Filter**

    - Beschreibung: Benutzerdefinierte eingehende Regel – **schließt alle Benutzer mit UPN aus, die nicht auf die benutzerdefinierte Azure AD-Aufgabe festgelegt sind Standard**

    - Verbinden ed System: **corp.contoso.com**

    - Objekttyp des verbundenen Systems: Benutzer

    - Metaverse-Objekttyp: Person

    - Verknüpfungstyp: Join

    - Rangfolge: **51**

    - Tag: Lassen Sie dieses Feld leer.

    - Kennwortsynchronisierung aktivieren: **Leer lassen**

    - Deaktiviert: **Leer lassen**


10. Wählen Sie auf dem Bildschirm für den **Bereichsfilter** die Option **Weiter** aus.

11. Wählen Sie auf der Seite **Verknüpfungsregeln** die Option **Weiter** aus.

12. Wählen Sie auf der **Seite "Transformationen**" die Option **"Transformation** hinzufügen" folgendes aus, und wählen Sie "Hinzufügen"** aus**:

    - FlowType: Konstant

    - Target-Attribut: **cloudFiltered**

    - Quelle: **True**

13. Wenn ein **Dialogfeld "Warnung** " angezeigt wird, in dem eine Meldung angezeigt wird, dass **während des nächsten Synchronisierungszyklus** eine vollständige Import- und vollständige Synchronisierung auf "corp.contoso.com" ausgeführt wird, wählen Sie **"OK**" aus.

    >**Hinweis**: Dies sollte Sie zurück zur **Ansicht bringen und Ihre Synchronisierungsregelnschnittstelle** verwalten, wobei die neuen Regeln oben in der Regelliste aufgeführt sind. 

### Aufgabe 3: Überprüfen der Verzeichnissynchronisierung

1. Doppeltippen Sie in der Remotedesktopsitzung auf **DC1** die **Azure AD Verbinden** Desktopverknüpfung aus.

2. 2 – Klicken Sie auf der Seite **Willkommen bei Azure AD Connect** auf **Weiter**. 

3. Wählen Sie auf der Seite **Weitere Aufgaben** die Option **Synchronisierungsoptionen anpassen** aus, und wählen Sie dann **Weiter** aus.

4. Melden Sie sich auf der Verbinden auf der **Azure AD-Seite** mit den Anmeldeinformationen des **John.doe-Kontos** an, und wählen Sie "Weiter"** aus**.

5. Wählen Sie auf der Seite **Verzeichnisse verbinden** die Option **Weiter**.

6. Wählen Sie auf der Seite **Filtern von Domänen und Organisationseinheiten** die Option **Weiter**. 

7. Übernehmen Sie auf der Seite **Optionale Features** die Standardeinstellungen, und wählen Sie **Weiter** aus.

8. Wählen Sie auf der **Seite "Einmaliges** Anmelden aktivieren" die Option "Weiter"** aus**.

9. Vergewissern Sie sich auf der Seite **Bereit zur Konfiguration**, dass das Kontrollkästchen **Starten Sie den Synchronisierungsvorgang, nachdem die Konfiguration abgeschlossen wurde.** aktiviert ist, und wählen Sie anschließend **Installieren** aus.

10. Wählen Sie auf der Seite **Konfiguration abgeschlossen** die Option **Beenden**.

11. Navigieren Sie in der Remotedesktop-Sitzung für **adVM** im Fenster „Microsoft Edge“, in dem das Azure-Portal angezeigt wird, zum Blatt **Benutzer – Alle Benutzer** des Azure AD-Mandanten „Adatum-Lab“.

12. Beachten Sie auf der **Seite "Benutzer – Alle Benutzer**", dass die Liste der Benutzerobjekte alle Benutzerkonten mit dem UPN-Suffix enthält, das dem benutzerdefinierten Do entspricht Standard Name des Azure AD-Mandanten. Möglicherweise müssen Sie die Seite aktualisieren oder einige Minuten warten, um die Änderung anzuzeigen.

13. Navigieren Sie im Azure-Portal zur **Seite "Gruppen – Alle Gruppen**" des Azure AD-Mandanten von Contoso, und beachten Sie, dass alle corp.contoso.com Standard Gruppen ebenfalls synchronisiert wurden. 

14. Navigieren Sie im Azure-Portal zur **Seite "Contoso - Azure AD Verbinden**", und wählen Sie **auf der linken Seite azure AD Verbinden** aus. Vergewissern Sie sich, dass die folgenden Einstellungen aktiv sind: 

    - Azure AD Verbinden Synchronisierungsstatus: **Aktiviert** 
  
    - Letzte Synchronisierung: **Dies sollte ein Zeitstempel einer Art sein**. 
  
    - Kennworthashsynchronisierung: **Deaktiviert** 
  
    - Partnerverbund: **Deaktiviert**
   
    - Nahtloses Einmaliges Anmelden: **Für 1 aktiviert Standard** 
  
    - Agent für Pass-Through-Authentifizierung

   > **Hinweis**: In einer Produktionsumgebung würden Sie zusätzliche Agents für Redundanz installieren. Weitere Informationen finden Sie unter <https://docs.microsoft.com/en-us/azure/active-directory/hybrid/how-to-connect-pta-quick-start>.

### Konfigurieren der Hybrid-Azure AD-Einbindung

In dieser Aufgabe konfigurieren Sie Azure AD Verbinden Gerätesynchronisierungsoptionen.

1. Doppeltippen Sie in der Remotedesktopsitzung auf **DC1** die **Azure AD Verbinden** Desktopverknüpfung aus.

2. 2 – Klicken Sie auf der Seite **Willkommen bei Azure AD Connect** auf **Weiter**. 

3. Wählen Sie auf der Seite **Zusätzliche Aufgaben** die Option **Geräteoptionen konfigurieren** und dann **Weiter** aus.

4. Überprüfen Sie auf der Seite Übersicht im Fenster Microsoft Azure Active Directory Connect die Information zu Hybrid-Azure AD-Einbindung und Geräterückschreiben, und wählen Sie Weiter aus.

5. Melden Sie sich auf der Verbinden auf der **Azure AD-Seite** mit den Anmeldeinformationen des **John.doe-Kontos** an, und wählen Sie "Weiter"** aus**.

6. Wählen Sie auf der Seite **Geräteoptionen** die Option **Hybrid-Azure AD-Einbindung konfigurieren** und dann **Weiter** aus. 

7. Wählen Sie auf der **Seite "Gerätebetriebssystem**" die **Kontrollkästchen "Windows 10" oder "Höher" aus Standard-verbundenen Geräten** und **aktivierte Windows-Abwärtsstufen Standard Kontrollkästchen für verbundene Geräte**, und wählen Sie "Weiter"** aus**. 

   > **Hinweis**: Windows-Geräte werden nur unterstützt, wenn Sie nahtlosen SSO für verwaltete Aufgaben verwenden Standard oder einen Verbunddienst wie AD FS für Verbund do Standard s.

8. Aktivieren Sie auf der SCP-Konfigurationsseite** das **Feld corp.contoso.com** Active Directory-Gesamtstruktur, aktivieren Sie den **Azure Active Directory-Eintrag** in der Dropdownliste des **Authentifizierungsdiensts**, und wählen Sie "Hinzufügen"** aus**.**

9. Wenn Sie zur Eingabe von Unternehmensadministratoranmeldeinformationen für corp.contoso.com aufgefordert werden, melden Sie sich im Dialogfeld Windows-Sicherheit** mit dem\\** Unternamen corp demouser** und **dem Demo\@pass123-Kennwort** **an.

10. Klicken Sie auf der Seite **Konfigurationstyp auswählen** auf **Weiter**.

11. Wählen Sie auf der Seite **Bereit für Konfiguration** die Option **Konfigurieren**.

12. Überprüfen Sie auf der **Seite "Konfiguration abgeschlossen**", ob die Aufgabe erfolgreich abgeschlossen wurde, und wählen Sie "Beenden" aus****.


### Aufgabe 11: Durchführen der Hybrid-Azure AD-Verknüpfung

1. Überprüfen Sie auf dem Laborcomputer im Azure-Portal, dass Sie beim Azure AD-Mandanten angemeldet sind, der dem Azure-Abonnement zugeordnet ist, in dem Sie Ressourcen in den Übungen "Before Hands-On Lab" (Standardverzeichnis****) bereitgestellt haben. Wählen Sie andernfalls das **Symbol "Verzeichnis + Abonnement**" in der Symbolleiste des Azure-Portal (rechts neben dem **Cloud Shell-Symbol**) aus, um zu diesem Azure AD-Mandanten zu wechseln. 

2. Navigieren Sie im Azure-Portal zur Übersichtsseite Ihrer VM.

3. Stellen Sie auf der **Seite "APP1** virtual machine" eine Verbindung mit APP1** über Remotedesktop her**. Wenn Sie zur Anmeldung aufgefordert werden, verwenden Sie den **Benutzernamen AGAyers\@<custom_doStandard_name>** mit dem ****demo@pass123Kennwort (wobei **<custom_doStandard_name>** Platzhalter den benutzerdefinierten DNS-Vorgang darstellt Standard Name, den Sie dem Azure AD-Mandanten von Contoso zuvor in dieser Übung zugewiesen haben.

4. Starten Sie in der Remotedesktopsitzung auf **APP1** im **Server-Manager-Fenster** den Taskplaner** unter **"Extras"**.** 


5. Erweitern Sie in der Konsolenstruktur der Aufgabenplanung AufgabenplanungsbibliothekMicrosoftWindows. Aktivieren Sie dann die **Aufgabe "Automatic-Device-Join** ". 


6. Wechseln Sie zur Remotedesktopsitzung zu **DC1**, und starten Sie im Konsolenbereich des Windows PowerShell ISE-Fensters Azure AD Verbinden Deltasynchronisierung, indem Sie Folgendes ausführen:

   ```pwsh
   Import-Module -Name 'C:\Program Files\Microsoft Azure AD Sync\Bin\ADSync\ADSync.psd1'
   
   Start-ADSyncSyncCycle -PolicyType Delta
   ```

7. Wechseln Sie zurück zur Remotedesktopsitzung zu **APP1** , und starten Sie eine **Eingabeaufforderung**.

8. Überprüfen Sie im Eingabeaufforderungsfenster den Azure AD-Registrierungsstatus von APP1, indem Sie Folgendes ausführen: 

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
11. Wechseln Sie zurück zur Remotedesktopsitzung zu **DC1**, im Edge-Browserfenster, in dem die Azure-Portal angezeigt wird, navigieren Sie zur **Seite "Geräte – Alle Geräte**" des Azure AD-Mandanten von Contoso, und stellen Sie sicher, dass ein Eintrag vorhanden ist, der den APP1-Server darstellt, wobei der **Verknüpfungstyp** auf "**Hybrid azure AD"** festgelegt ist.

   > **Hinweis**: Möglicherweise müssen Sie warten, bis der Azure AD-Registrierungsstatus richtig gemeldet wird und das Azure AD-Objekt im Azure-Portal angezeigt wird.


