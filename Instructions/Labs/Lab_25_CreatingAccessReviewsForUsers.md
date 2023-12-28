---
lab:
  title: 'Übung: Erstellen von Zugriffsüberprüfungen für interne und externe Benutzer*innen'
  learning path: '04'
  module: Module 04 - Plan and Implement and Identity Governance Strategy
---

# Übung: Erstellen von Zugriffsüberprüfungen für interne und externe Benutzer*innen  

## Labszenario

Der privilegierte Benutzerzugriff sollte regelmäßig auf ähnliche Weise überprüft werden.Da es sich um erhöhte Zugriffszuweisungen handelt, sollte die Überprüfung dieser Aufgaben konsistent erfolgen, wie sie vom Unternehmen identifiziert werden.Nicht verwendete und unnötige privilegierte Zuordnungen sollten entfernt werden.Die automatisierte Entfernung sollte auch für Benutzer konfiguriert werden, die nicht mehr mit dem Unternehmen zusammenarbeiten oder Abteilungen innerhalb des Unternehmens geändert haben.

#### Geschätzte Dauer: 5 Minuten

### Übung 1 – Erstellen einer internen Zugriffsüberprüfung

#### Erstellen Sie eine neue Zugriffsüberprüfung.

1. Melden Sie sich als globaler Administrator an.

2. Zugriffsüberprüfungen können den Zugriffslebenszyklus verwalten.Suchen Sie innerhalb **der Microsoft Entra-ID** die Identitätsgovernance****, und wählen Sie **dann Access-Rezensionen** aus.

3. Wählen Sie **+ Neue Zugriffsüberprüfung** aus.

4. Wählen Sie im Feld **Zu überprüfende Elemente auswählen** die Option **Teams + Gruppen** aus.

5. Wählen Sie "Teams + Gruppen" aus, und wählen Sie **in der Liste die **Gruppe "Vertrieb und Marketing**" aus, und drücken Sie "**Auswählen"**.**

6. Legen Sie den **Bereich** auf **alle Benutzer** fest.

7. Wählen Sie " **Weiter" aus: Rezensionen** , die im Assistenten vorwärts verschoben werden sollen.

8. Der nächste Schritt besteht darin, die Prüfer zu bestimmen.Diese Prüfer können das Mitglied selbst sein, um eine Selbstüberprüfung zu erledigen, oder den Vorgesetzten zugewiesen werden, wenn der Zugriff für eine gesamte Abteilung überprüft wird. Sie können die Aktion auch festlegen, wenn ein Bearbeiter nicht automatisch reagiert, um diesen privilegierten Zugriff vom Mitglied zu entfernen.

9. Wählen Sie eine Prüfer- und Überprüfungsserienoption aus.  Wählen Sie dann **Einstellungen** aus.

10. Mit den erweiterten Einstellungen können Sie eine Nachricht als Teil der Überprüfung ablegen.

11. Wechseln Sie zur **Registerkarte "Überprüfen + Erstellen** ", um die Zugriffsüberprüfung abzuschließen.

12. Benennen Sie den Zugriffsüberprüfungstest **** SC300.

13. Wählen Sie am unteren Rand der Seite die Option **Erstellen**.

    **Hinweis** : Wenn die Zugriffsüberprüfung erstellt wird, wird die Zugriffsüberprüfungsliste mit den Rollen und Besitzern der Rezensionen aufgefüllt.

14. Mitglieder, die überprüft werden, erhalten eine E-Mail, wenn die Überprüfung initiiert wird.

15. Wenn Sie eine Zugriffsüberprüfung einer der Rollen auswählen, wird der Status für diese Zugriffsüberprüfungen bereitgestellt.
