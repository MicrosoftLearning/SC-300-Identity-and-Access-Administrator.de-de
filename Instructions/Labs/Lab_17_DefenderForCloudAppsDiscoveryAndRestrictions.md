---
lab:
  title: '17: Defender for Cloud Apps: Anwendungs-Discovery und Erzwingen von Einschränkungen'
  learning path: '03'
  module: Module 03 - Implement Access Management for Apps
---

# Lab 17: Defender for Cloud Apps: Anwendungs-Discovery und Erzwingen von Einschränkungen

### Anmeldetyp = Microsoft 365 Admin

## Labszenario

Microsoft Defender for Cloud Apps verwendet Protokolle vom Netzwerkdatenverkehr, um die Anwendungen zu identifizieren, auf die Benutzer zugreifen.  Datenverkehrsprotokolle von lokalen Firewalls bieten einen Momentaufnahmebericht über die am häufigsten verwendeten Anwendungen und die Benutzer, die auf diese Apps zugreifen.  Der Datenverkehr von verwalteten Geräten wird in das Übersichtsdashboard „Microsoft Defender für Cloud Apps Discovery“ aufgenommen.

#### Geschätzte Dauer: 10 Minuten

### Übung 1: Discovery von Microsoft Defender for Cloud Apps

#### Aufgabe 1: Discovery-Apps in Defender für Cloud Apps

1. Melden Sie sich mit einem globalen Administratorkonto bei [https://security.microsoft.com](https://security.microsoft.com)  an.

1. Scrollen Sie im linken Menü zur Überschrift **Cloud-Apps**, und wählen Sie **Cloud-App-Katalog** aus.

1. Wählen Sie im Bereich **Nach Kategorien durchsuchen** die Option **Cloudspeicher** aus.

1. Achten Sie in der Liste der Apps auf die **Risikobewertung** neben dem Namen der App.  

1. Öffnen Sie eine weitere Browser-Registerkarte und navigieren Sie zu **www.dropbox.com**.

1. Sie können dann auf diese Website zugreifen.

1. Schließen Sie die Registerkarte für Dropbox.

1. Kehren Sie zum Bildschirm „Defender for Cloud Apps“ zurück und wählen Sie die drei Punkte rechts neben Dropbox aus.

1. Wählen Sie **Sanktioniert** und dann die Schaltfläche **Weiter**. 

#### Aufgabe 2: Einschränken von Apps in Defender for Cloud Apps

1. Kehren Sie zur Kachel **Ermittelte Apps** zurück, und wählen Sie **Als "Nicht sanktioniert" markieren** für Dropbox aus.  **Hinweis**: Dies befindet sich neben dem eingekreisten Häkchen.

1. Wählen Sie **Speichern** aus.

1. Mit diesem Prozess können Sie Anwendungen blockieren, die nicht innerhalb Ihrer Unternehmensrichtlinie genehmigt sind, wodurch die Schatten-IT in Ihrer Organisation eingeschränkt wird.

**Hinweis:** Bei der Genehmigung und Aufhebung der Genehmigung von dieser Anwendung und anderer Anwendungen kommt es zu einer Verzögerung. Möglicherweise müssen Sie bis zu 5 Minuten warten.

Sobald die Anwendung als nicht genehmigt blockiert wurde, kann auf die Anwendung nicht über einen Browser, einen InPrivate-Browser oder einen Speicherdownload auf einem Client zugegriffen werden, der in MDE (Microsoft Defender for Endpunkt) integriert ist, das in Microsoft Defender for Cloud Apps integriert ist.
