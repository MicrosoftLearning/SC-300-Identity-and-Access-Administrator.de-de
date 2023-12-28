---
lab:
  title: 17 - Defender for Cloud Apps Anwendungserkennung und Erzwingung von Einschränkungen
  learning path: '03'
  module: Module 03 - Implement Access Management for Apps
---

# Übung 17 - Defender for Cloud Apps Anwendungserkennung und Erzwingen von Einschränkungen

## Labszenario

Microsoft Defender for Cloud Apps nutzt die Protokolle des Netzwerkverkehrs, um die Anwendungen zu identifizieren, die auf die Benutzer zugreifen.Datenverkehrsprotokolle von lokalen Firewalls bieten einen Momentaufnahmebericht über die am häufigsten verwendeten Anwendungen und die Benutzer, die auf diese Apps zugreifen.Der Datenverkehr von verwalteten Geräten wird in das Übersichts-Dashboard von Microsoft Defender for Cloud Apps eingespeist

#### Geschätzte Dauer: 10 Minuten

### Übung 1 - Entdecken Sie Microsoft Defender for Cloud Apps

#### Aufgabe 1 - Entdeckung von Apps in Defender for Cloud Apps

1. Melden Sie sich bei [https://security.microsoft.com](https://security.microsoft.com) mit einem globalen Administrator-Konto an.

1. Blättern Sie im linken Menü zur Überschrift **Cloud Apps** und wählen Sie **Cloud App Catalog**.

1. Wählen Sie im Bereich **Durchsuchen nach Kategorie** die Option **Cloud-Speicher**.

1. Achten Sie in der Liste der Apps auf die **Risikobewertung** neben dem Namen der App.  

1. Öffnen Sie eine weitere Browser-Registerkarte und navigieren Sie zu **www.dropbox.com**.

1. Sie können dann auf diese Website zugreifen.


#### Aufgabe 2 - Apps in Defender für Cloud-Apps einschränken

1. Kehren Sie zur Kachel **Entdeckte Apps** zurück und wählen Sie die **Kennzeichnung als unbestätigt** für Dropbox.  **Hinweis**: Diese befindet sich neben dem eingekreisten Häkchen.

1. Klicken Sie unten auf der Seite auf **Speichern**.

1. Mit diesem Verfahren können Sie Anwendungen blockieren, die nicht im Rahmen Ihrer Unternehmensrichtlinien zugelassen sind, und so die Schatten-IT in Ihrem Unternehmen einschränken.

**Hinweis**: Es gibt eine Verzögerung zwischen der Entsperrung einer Anwendung und der Sperrung dieser Anwendung.

Sobald die Anwendung als nicht genehmigt blockiert wurde, ist der Zugriff auf die Anwendung über einen Browser, einen privaten Browser oder einen Speicherdownload auf einem Client, der in MDE (Microsoft Defender for Endpoint) mit Microsoft Defender for Cloud Apps integriert ist, nicht mehr möglich.



