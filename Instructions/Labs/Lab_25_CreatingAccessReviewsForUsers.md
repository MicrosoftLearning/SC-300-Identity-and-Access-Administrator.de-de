---
lab:
  title: '25: Erstellen von Zugriffsüberprüfungen für interne und externe Benutzer'
  learning path: '04'
  module: Module 04 - Plan and Implement and Identity Governance Strategy
---

# Lab 25: Erstellen von Zugriffsüberprüfungen für interne und externe Benutzer  

## Labszenario

Der privilegierte Benutzerzugriff sollte regelmäßig auf ähnliche Weise überprüft werden.  Da es sich um Zugriffszuweisungen mit erhöhten Rechten handelt, sollte die Überprüfung dieser Aufgaben auf einer einheitlichen, vom Unternehmen festgelegten Grundlage erfolgen.  Nicht verwendete und unnötige privilegierte Zuweisungen sollten entfernt werden.  Die automatisierte Entfernung sollte auch für Benutzer konfiguriert werden, die nicht mehr für das Unternehmen arbeiten oder Abteilungen im Unternehmen gewechselt haben.

#### Geschätzte Dauer: 5 Minuten

### Übung 1: Erstellen einer internen Zugriffsüberprüfung

#### Aufgabe: Erstellen einer neue Zugriffsüberprüfung

1. Melden Sie sich bei [https://portal.azure.com](https://portal.azure.com) als globaler Administrator an.

2. Zugriffsüberprüfungen können den Zugriffslebenszyklus verwalten.  Suchen Sie in **Azure Active Directory** den Eintrag **Identity Governance** unter dem Menü **Verwalten**.  Wählen Sie in **Identity Goverance** die Option **Zugriffsüberprüfungen** aus.

3. Wählen Sie **+ Neue Zugriffsüberprüfung** aus.

4. Wählen Sie im Feld **Wählen Sie aus, was zu überprüfen ist** die Option **Teams + Gruppen** in der Verwalten aus.

5. Wählen Sie **Teams + Gruppen auswählen** und dann in der Liste die Gruppe **Vertrieb und Marketing** aus, und wählen Sie **Auswählen** aus.

6. Legen Sie den **Bereich** auf **Alle Benutzer** fest.

7. Wählen Sie die Option **Überprüfungen** aus, um im Assistenten vorwärts zu wechseln.

8. Der nächste Schritt besteht darin, die Prüfer zu bestimmen.  Diese Prüfer können das Mitglied selbst sein, um eine Selbstüberprüfung auszuführen, oder können Vorgesetzten zugewiesen werden, wenn der Zugriff für eine gesamte Abteilung überprüft wird. Sie können auch die Aktion für den Fall festlegen, dass ein Prüfer nicht antwortet, um dem Mitglied automatisch den privilegierten Zugriff zu entziehen.

9. Wählen Sie eine Prüfer- und Überprüfungsserienoption aus.  Wählen Sie dann **Einstellungen** aus.

10. Mit den erweiterten Einstellungen können Sie eine Nachricht als Teil der Überprüfung angeben.

11. Wählen Sie **Überprüfen und Erstellen** aus, um die Zugriffsüberprüfung abzuschließen.

12. Nennen Sie die Zugriffsüberprüfung **SC300 Access Review Test**.

13. Wählen Sie **Erstellen** aus. Wenn die Zugriffsüberprüfung erstellt ist, wird die Zugriffsüberprüfungsliste mit den Rollen und Besitzern der Überprüfungen ausgefüllt.

14. Mitglieder, die überprüft werden, erhalten eine E-Mail, wenn die Überprüfung initiiert wird.

15. Wenn Sie eine Zugriffsüberprüfung einer der Rollen auswählen, wird der Status für diese Zugriffsüberprüfungen bereitgestellt.
