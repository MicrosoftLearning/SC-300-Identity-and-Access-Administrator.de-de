---
lab:
  title: '16: Verwenden von Azure Key Vault für verwaltete Identitäten'
  learning path: '02'
  module: Module 02 - Implement an Authentication and Access Management Solution
---

# Lab 16: Verwenden von Azure Key Vault für verwaltete Identitäten

### Anmeldetyp = Azure Resource-Anmeldung

## Labszenario

Mithilfe von verwalteten Identitäten für Azure-Ressourcen kann der Code Zugriffstoken zur Authentifizierung von Ressourcen abrufen, die die Microsoft Entra-Authentifizierung unterstützen.  Allerdings unterstützen nicht alle Azure-Dienste die Microsoft Entra-Authentifizierung. Um verwaltete Identitäten für Azure-Ressourcen mit diesen Diensten zu verwenden, speichern Sie die Dienstanmeldeinformationen in Azure Key Vault, und greifen Sie mit der verwalteten Identität auf Key Vault zu, um die Anmeldeinformationen abzurufen.

#### Geschätzte Dauer: 20 Minuten

### Übung 1: Verwenden von Azure Key Vault zum Verwalten von Identitäten virtueller Computer

#### Aufgabe 1: Erstellen eines Key Vault

1. Melden Sie sich mit einem globalen Administratorkonto bei [https://portal.azure.com]( https://portal.azure.com) an.

1. Wählen Sie oben in der linken Navigationsleiste **+ Ressource erstellen** aus.

1. Geben Sie im Feld „Marketplace durchsuchen“ den Suchbegriff **Key Vault** ein.  

1. Wählen Sie in den Ergebnissen **Key Vault** aus.

1. Klicken Sie auf **Erstellen**.

1. Füllen Sie alle erforderlichen Informationen wie unten gezeigt aus. Wählen Sie unbedingt das Abonnement und die Ressourcengruppe aus, die Sie für dieses Tutorial verwenden.
    **Hinweis**: Der Name der Key Vault-Ressource muss eindeutig sein. Suchen Sie rechts neben dem Feld nach einem grünen Häkchen.

 - **Ressourcengruppe**: rgSC300KeyVault
 - **Key Vault-Name** - *anyuniquevalue*
 - Wählen Sie auf der Seite **Access Configuration** das Optionsfeld **Vault Access Policy** aus.
1. Wählen Sie **Überprüfen + erstellen** aus.

1. Klicken Sie auf **Erstellen**.

#### Aufgabe 2: Erstellen eines virtuellen Windows-Computers

1. Wählen Sie **+ Ressource erstellen** aus.

1. Geben Sie **Windows 11** in der Marketplace-Suchleiste ein.

1. Wählen Sie **Windows 11** aus und wählen Sie aus der Dropdownliste **Windows 11 Enterprise, Version 22H2** aus. Wählen Sie dann **Erstellen** aus.

  | Feld | Werte |
  | :--   | :--    |
  | VM-Name | vmKeyVault |
  | Verfügbarkeitsoptionen | Keine Infrastrukturredundanz erforderlich |
  | Benutzername des Administrators | adminKeyVault |
  | Kennwort | Legen Sie ein sicheres Kennwort fest, das Sie sich merken können |
  | Lizenzierung | Bestätigen Sie, dass Sie über eine berechtigte Lizenz verfügen |

1. Vergessen Sie nicht, das Kontrollkästchen **Lizenzierung bestätigen** zu aktivieren.

1. Verwenden Sie die Schaltfläche **Weiter**, um zur Registerkarte **Verwaltung** zu gelangen.

1. Markieren Sie auf der Registerkarte **Verwaltung** das Kästchen neben **System zugewiesene verwaltete Identität aktivieren**.

1. Führen Sie die weiteren Schritte zum Erstellen eines virtuellen Computers aus. 

1. Wählen Sie **Überprüfen + Erstellen** und wählen Sie dann **Erstellen**.

#### Aufgabe 3: Erstellen eines Geheimnisses

1. Navigieren Sie zum neu erstellten Key Vault.

1. Öffnen Sie **Objekte** im linken Menü und wählen Sie dann **Geheimnisse**.

1. Wählen Sie die Option **+ Generieren/Importieren** aus.

1. Belassen Sie auf dem Bildschirm „Geheimnis erstellen“ unter „Uploadoptionen“ die Option **Manuell** ausgewählt.

1. Geben Sie einen Namen und einen Wert für das Geheimnis ein.  Dabei kann es sich um einen beliebigen Wert handeln. 

1. Belassen Sie das Aktivierungs- und das Ablaufdatum leer, und übernehmen Sie für „Aktiviert“ die ausgewählte Option „Ja“. 

1. Wählen Sie **Erstellen** aus, um das Geheimnis zu erstellen.

#### Aufgabe 4: Gewähren des Zugriffs auf Key Vault

1. Navigieren Sie zum neu erstellten Key Vault.

1. Wählen Sie im Menü auf der linken Seite die Option **Zugriffsrichtlinien** aus.

1. Wählen Sie **+ Erstellen** aus.

1. Wählen Sie im Abschnitt „Zugriffsrichtlinie hinzufügen“ unter „Aus Vorlage konfigurieren (optional)“ im Pulldownmenü die Option **Verwaltung von Geheimnissen** aus.

1. Verwenden Sie die Schaltfläche „Weiter“, um zur Registerkarte **Prinzipal** zu gelangen.

1. Geben Sie in das Suchfeld den Namen der VM ein, die Sie in Aufgabe 2 erstellt haben: **vmKeyVault**.  Wählen Sie in der Ergebnisliste den virtuellen Computer und dann Auswählen aus.

1. Klicken Sie auf „Weiter“, um zur Registerkarte **Überprüfen + erstellen** zu gelangen.

1. Klicken Sie auf **Erstellen**.

#### Aufgabe 5: Zugreifen auf Daten mit Key Vault-Geheimnis und PowerShell

1. Wechseln Sie zu **vmKeyVault** und verwenden Sie RDP, um eine Verbindung mit Ihrem virtuellen Computer als **adminKeyVault** herzustellen.

1. Öffnen Sie auf dem virtuellen Computer des Labs PowerShell.  

1. Rufen Sie in PowerShell die Webanforderung für den Mandanten auf, um das Token für den lokalen Host am spezifischen Port des virtuellen Computers abzurufen.  

    ```
    $Response = Invoke-RestMethod -Uri 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fvault.azure.net' -Method GET -Headers @{Metadata="true"}
    ```

1. Extrahieren Sie dann das Zugriffstoken aus der Antwort.  

    ```
    $KeyVaultToken = $Response.access_token
    ```

1. Verwenden Sie den PowerShell-Befehl „Invoke-WebRequest“, um das zuvor in Key Vault erstellte Geheimnis abzurufen. Übergeben Sie dabei das Zugriffstoken im Autorisierungsheader.  Sie benötigen die URL Ihrer Key Vaults. Diese befindet sich im Abschnitt Zusammenfassung der Seite Übersicht der Key Vault.  Erinnerung: Der URI für Key Vault befindet sich auf der Registerkarte „Übersicht“.

  - Key Vault-URI – Abrufen von der Key Vaults-Überblicksseite im Azure-Portal
  - Geheimnisname – Abrufen von der Seite „Objekte - Geheimnisse“ in der Key Vault

    ```
    Invoke-RestMethod -Uri https://<your-key-vault-URI>/secrets/<secret-name>?api-version=2016-10-01 -Method GET -Headers @{Authorization="Bearer $KeyVaultToken"}
    ```
1. Die Antwort sollte in etwa wie folgt aussehen: 
    ```
    'My Secret' https://mi-lab-vault.vault.azure.net/secrets/mi-test/50644e90b13249b584c44b9f712f2e51 @{enabled=True; created=16…
    ```
1. Dieses Geheimnis kann verwendet werden, um sich bei Diensten zu authentifizieren, für die ein Name und ein Kennwort erforderlich sind.
