---
lab:
  title: "Lab\_3.9: Verwenden von Azure Key Vault für verwaltete Identitäten"
  learning path: '02'
  module: Module 02 - Implement an Authentication and Access Management Solution
---

# Lab 3.9: Verwenden von Azure Key Vault für verwaltete Identitäten

**Hinweis** : Für dieses Lab ist ein Azure Pass erforderlich. Anweisungen finden Sie in Lab 00.

## Labszenario

Mithilfe von verwalteten Identitäten für Azure-Ressourcen kann der Code Zugriffstoken zur Authentifizierung von Ressourcen abrufen, die die Microsoft Entra-Authentifizierung unterstützen.Jedoch nicht alle Azure-Dienste unterstützen die Microsoft Entra-Authentifizierung. Um verwaltete Identitäten für Azure-Ressourcen mit diesen Diensten zu verwenden, speichern Sie die Dienstanmeldeinformationen in Azure Key Vault, und greifen Sie mit der verwalteten Identität des virtuellen Computers auf Key Vault zu, um die Anmeldeinformationen abzurufen.

#### Geschätzte Dauer: 20 Minuten

### Übung 1 – Verwenden von Azure Key Vault zum Verwalten von Identitäten virtueller Computer

#### Aufgabe 1: Erstellen einer VM

1. Navigieren Sie zur folgenden URL: [https://portal.azure.com](https://portal.azure.com)

1. Wählen Sie **+ Ressource erstellen**.

1. Geben Sie **Windows Server** auf der Suchleiste „Marketplace durchsuchen“ ein.

1. Wählen Sie Windows 11** aus, und wählen Sie **in der Dropdownliste "Plan" die Option **"Windows 11 Enterprise, Version 21H2**" aus. Wählen Sie dann **Erstellen** aus.

1. Sie müssen einen Administratorbenutzernamen und ein Kennwort für den virtuellen Computer erstellen.

1. Aktivieren Sie auf der **Registerkarte "Verwaltung** " das Kontrollkästchen " **Vom System zugewiesene verwaltete Identität** aktivieren".

1. Führen Sie die weiteren Schritte zum Erstellen eines virtuellen Computers aus. 

1. Klicken Sie auf Erstellen.

#### Aufgabe 2: Erstellen eines Schlüsseltresors

1. Melden Sie sich mit dem globalen Administratorkonto beim Azure-Portal an.

1. Wählen Sie oben auf der linken Navigationsleiste Ressource erstellen aus.

1. Geben Sie im Feld Marketplace durchsuchen den Suchbegriff Key Vault ein, und drücken Sie die EINGABETASTE.  

1. Wählen Sie in den Ergebnissen **Key Vault** aus.

1. Klicken Sie auf **Erstellen**.

1. Füllen Sie alle erforderlichen Informationen aus. Wählen Sie unbedingt das Abonnement und die Ressourcengruppe aus, die Sie für dieses Tutorial verwenden.
    Der Name der Key Vault-Ressource muss eindeutig sein. Suchen Sie rechts neben dem Feld nach einem grünen Häkchen.

 - **Ressourcengruppe** - sc300KeyVaultrg
 - **Schlüsseltresorname** - *anyuniquevalue*
 - Wählen Sie auf der Seite " **Access-Konfiguration** " das **Optionsfeld "Tresorzugriffsrichtlinie** " aus.
1. Klicken Sie auf **Überprüfen + erstellen**.

1. Klicken Sie auf **Erstellen**.


#### Aufgabe 3 – Erstellen eines geheimen Schlüssels

1. Navigieren Sie zur neu erstellten Key Vault-Instanz.

1. Wählen Sie **Secrets** (Geheimnisse) aus.

1. Wählen Sie die Option **+ Generieren/Importieren** aus.

1. Lassen Sie auf dem Bildschirm Geheimnis erstellen unter Uploadoptionen die Option Manuell ausgewählt.

1. Geben Sie einen Namen und einen Wert für das Geheimnis ein.  Dabei kann es sich um einen beliebigen Wert handeln. 

1. Lassen Sie das Aktivierungs- und das Ablaufdatum leer, und übernehmen Sie für Aktiviert die ausgewählte Option Ja. 

1. Wählen Sie **Erstellen**, um das Geheimnis zu erstellen.

#### Gewähren des Zugriffs auf Key Vault

1. Navigieren Sie zur neu erstellten Key Vault-Instanz.

1. Wählen Sie im Menü auf der linken Seite die Option **Zugriffsrichtlinie** aus.

1. Wählen Sie **+ Erstellen** aus.

1. Wählen Sie im Abschnitt Zugriffsrichtlinie hinzufügen unter Anhand einer Vorlage konfigurieren (optional) im Pulldownmenü die Option Verwaltung von Geheimnissen aus.

1. Wählen Sie für **"Prinzipal** auswählen" die Option **"Keine" aus** , um die Liste der zu markierenden Prinzipale zu öffnen. Geben Sie im Suchfeld den Namen der VM ein, die Sie in Aufgabe 2 erstellt haben.  Wählen Sie in der Ergebnisliste den virtuellen Computer und dann Auswählen aus.

1. Wählen Sie **Hinzufügen**.

1. Wählen Sie **Speichern** aus.

#### Aufgabe 5 – Zugreifen auf Daten mit Schlüsseltresorschlüssel mit PowerShell

1. Öffnen Sie PowerShell auf dem virtuellen Computer.  

1. Rufen Sie in PowerShell die Webanforderung für den Mandanten auf, um das Token für den lokalen Host am spezifischen Port des virtuellen Computers abzurufen.  

    ```
    $Response = Invoke-RestMethod -Uri 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fvault.azure.net' -Method GET -Headers @{Metadata="true"}
    ```

1. Extrahieren Sie dann das Zugriffstoken aus der Antwort.  

    ```
    $KeyVaultToken = $Response.access_token
    ```

1. Verwenden Sie abschließend den PowerShell-Befehl „Invoke-WebRequest“, um das zuvor in der Key Vault erstellte Geheimnis abzurufen. Übergeben Sie dabei das Zugriffstoken im Autorisierungsheader.  Sie benötigen die URL Ihrer Key Vaults. Diese befindet sich im Abschnitt Zusammenfassung der Seite Übersicht der Key Vault.  Erinnerung – URI für Key Vault befindet sich auf der Registerkarte "Übersicht".

    ```
    Invoke-RestMethod -Uri https://<your-key-vault-URI>/secrets/<secret-name>?api-version=2016-10-01 -Method GET -Headers @{Authorization="Bearer $KeyVaultToken"}
    ```
1. Die Antwort sollte in etwa wie folgt aussehen: 
    ```
    'My Secret' https://mi-lab-vault.vault.azure.net/secrets/mi-test/50644e90b13249b584c44b9f712f2e51 @{enabled=True; created=16…
    ```
1. Dieser Geheimschlüssel kann verwendet werden, um sich bei Diensten zu authentifizieren, die einen Namen und ein Kennwort erfordern.
