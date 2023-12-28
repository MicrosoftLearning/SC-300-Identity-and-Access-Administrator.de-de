---
lab:
  title: "Verwalten Sie den Lebenszyklus externer Benutzer in Microsoft\_Entra Identity\_Governance-Einstellungen."
  learning path: '04'
  module: Module 04 - Plan and Implement and Identity Governance Strategy
---

# Verwalten Sie den Lebenszyklus externer Benutzer in Microsoft Entra Identity Governance-Einstellungen.  

## Labszenario

Sie können auswählen, was passiert, wenn ein externer Benutzer, der per Genehmigung der Anforderung eines Zugriffspakets eingeladen wurde, nicht mehr über Zuweisungen von Zugriffspaketen verfügt. Dies kann passieren, wenn der Benutzer alle Zuweisungen von Zugriffspaketen aufgibt oder seine letzte Zuweisung eines Zugriffspakets abläuft. Wenn ein externer Benutzer nicht mehr über Zuweisungen von Zugriffspaketen verfügt, wird für ihn die Anmeldung bei Ihrem Verzeichnis standardmäßig blockiert. Nach 30 Tagen wird das Gastbenutzerkonto aus Ihrem Verzeichnis entfernt.

#### Geschätzte Dauer: 5 Minuten

### Identitätsgovernance – Microsoft Entra

#### Verwalten Sie den Lebenszyklus externer Benutzer in Microsoft Entra Identity Governance-Einstellungen.

1. Melden Sie sich als globaler Administrator an.

2. Öffnen Sie Microsoft Entra ID und wählen Sie  **Identity Governance** aus.

3. Wählen Sie im linken Navigationsmenü unter **Berechtigungsverwaltung** die Option **Einstellungen** aus.

4. Wählen Sie im oberen Menü die Option **Bearbeiten** aus.

    ![Screenshot der Seite „Einstellungen“ in Identity Governance mit hervorgehobener Option „Lebenszyklus von externen Benutzern verwalten“](./media/lp4-mod1-manage-lifcycle-of-ext-users.png)

5. Überprüfen Sie im Abschnitt **Lebenszyklus von externen Benutzern verwalten** die unterschiedlichen Einstellungen für externe Benutzer.

6. Wenn ein externer Benutzer seine letzte Zuweisung zu Zugriffspaketen verliert und Sie die Anmeldung bei diesem Verzeichnis blockieren möchten, legen Sie die Option **Anmelden von externen Benutzern bei diesem Verzeichnis blockieren** auf **Ja** fest.

7. Wenn die Anmeldung eines Benutzers bei diesem Verzeichnis blockiert ist, kann der Benutzer das Zugriffspaket nicht erneut anfordern und auch keinen zusätzlichen Zugriff in diesem Verzeichnis beantragen. Konfigurieren Sie keine Blockierung der Anmeldung, wenn die Benutzer später den Zugriff auf weitere Zugriffspakete anfordern müssen.

8. Wenn ein externer Benutzer seine letzte Zuweisung zu Zugriffspaketen verliert und Sie sein Gastbenutzerkonto aus diesem Verzeichnis entfernen möchten, müssen Sie **Externen Benutzer entfernen** auf **Ja** festlegen.

    Im Rahmen der Berechtigungsverwaltung werden nur Konten entfernt, für die eine Einladung per Berechtigungsverwaltung erfolgt ist. Beachten Sie außerdem Folgendes: Für einen Benutzer wird auch dann die Anmeldung blockiert und die Entfernung aus dem Verzeichnis durchgeführt, wenn dieser Benutzer zu Ressourcen im Verzeichnis hinzugefügt wurde, die nicht den Zuweisungen von Zugriffspaketen unterliegen. Wenn der Gastbenutzer bereits in diesem Verzeichnis vorhanden war, bevor die Zuweisungen von Zugriffspaketen durchgeführt wurden, wird er nicht entfernt. Falls der Gast aber per Zuweisung eines Zugriffspakets eingeladen und anschließend auch einer OneDrive for Business- oder SharePoint Online-Website zugewiesen wurde, wird er trotzdem entfernt.

9. Wenn Sie das Gastbenutzerkonto in diesem Verzeichnis entfernen möchten, können Sie die Anzahl von Tagen festlegen, die ablaufen sollen, bevor die Entfernung durchgeführt wird. Falls Sie das Gastbenutzerkonto entfernen möchten, sobald die letzte Zuweisung von Zugriffspaketen abgelaufen ist, legen Sie **Anzahl von Tagen, bevor ein externer Benutzer aus diesem Verzeichnis entfernt wird** auf **0** fest.

10. Wenn Sie Änderungen vorgenommen haben, wählen Sie **Speichern** aus.
