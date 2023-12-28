---
lab:
  title: 11 - Zuweisen von Azure-Ressourcenrollen in PIM
  learning path: '02'
  module: Module 02 - Implement an authentication and access management solution
---

# Übung 11 - Zuweisen von Azure-Ressourcenrollen in PIM

**Hinweis**: Für dieses Lab ist ein Azure Pass erforderlich. Anweisungen finden Sie in Lab 00.

## Labszenario

Microsoft Entra Privileged Identity Management (Azure AD PIM) kann sowohl die integrierten Azure-Ressourcenrollen als auch benutzerdefinierte Rollen verwalten. Beispiele:

- Besitzer
- Benutzerzugriffsadministrator
- Mitwirkender
- Sicherheitsadministrator
- Sicherheits-Manager

Sie müssen einem Benutzer*in die Berechtigung für eine Azure-Ressourcenrolle erteilen.


#### Geschätzte Dauer: 10 Minuten

### Übung 1 - PIM mit Azure-Ressourcen

#### Aufgabe 1 - Zuweisen von Azure-Ressourcenrollen

1. Melden Sie sich bei [https://entra.microsoft.com](https://entra.microsoft.com) mit einem globalen Administratorkonto an.

2. Suchen und wählen Sie dann **Privileged Identity Management.**

3. Wählen Sie auf der Seite "Privileged Identity Management" in der linken Navigation **Azure-Ressourcen.**

4. Klicken Sie im oberen Menü auf **Ressourcen ermitteln**.

5. Wählen Sie auf der Seite "Azure-Ressourcen - Ermittlung" Ihr Abonnement aus.

   ![Screenshot der Seite „Azure-Ressourcen - Ermittlung“ mit hervorgehobenem Abonnement und Option „Ressource verwalten“](./media/lp4-mod3-pim-azure-resource-management.png)

6. Überprüfen Sie die Informationen auf der Seite **Übersicht**.

   ![Screenshot der neu hinzugefügten Azure-Ressource](./media/lp4-mod3-pim-az-resource-overview.png)

7. Klicken Sie im linken Navigationsmenü unter **Verwalten** auf **Rollen**, um die Liste der Rollen für Azure-Ressourcen anzuzeigen.

8. Klicken Sie im oberen Menü auf **Zuweisungen hinzufügen**.

9. Wählen Sie auf der Seite "Zuweisungen hinzufügen" das Menü **Rolle auswählen** und wählen Sie dann **API Management Service Contributor.**

10. Wählen Sie unter **Mitglied(er) auswählen** die Option **Keine Mitglieder ausgewählt** aus.

11. Wählen Sie **Miriam Graham** aus Ihrer Organisation aus, der die Rolle zugewiesen werden soll.  Wählen Sie anschließend **Auswählen** .

12. Wählen Sie **Weiter** aus.

13. Klicken Sie auf der Registerkarte **Einstellungen** unter **Zuweisungstyp** auf die Option **Berechtigt**.

   - Für **berechtigte** Zuweisungen muss das Mitglied der Rolle eine Aktion durchführen, um die Rolle verwenden zu können. Beispiele für Aktionen sind eine erfolgreiche Multi-Factor Authentication-Überprüfung (MFA), die Angabe einer geschäftlichen Begründung oder das Anfordern einer Genehmigung von den angegebenen genehmigenden Personen.

   - Für **aktive** Zuweisungen ist es nicht erforderlich, dass das Mitglied eine Aktion durchführt, um die Rolle nutzen zu können. Bei als aktiv zugewiesenen Mitgliedern sind die Berechtigungen immer der Rolle zugewiesen.

14. Geben Sie die Zuweisungsdauer an, indem Sie den Start- und Endzeitpunkt für Datum und Uhrzeit ändern.

15. Klicken Sie abschließend auf **Zuweisen**.

16. Nachdem die neue Rollenzuweisung erstellt wurde, wird eine Statusbenachrichtigung angezeigt.

#### Aufgabe 2 - Aktualisieren oder Entfernen der Zuweisung einer vorhandenen Ressourcenrolle

Befolgen Sie diese Anweisungen zum Aktualisieren oder Entfernen einer vorhandenen Rollenzuweisung.

1. Öffnen Sie **Microsoft Entra Privileged Identity Management**.

2. Wählen Sie **Azure-Ressourcen** aus.

3. Wählen Sie das Abonnement, das Sie verwalten möchten, um die Übersichtsseite zu öffnen.

4. Wählen Sie unter **Verwalten** die Option **Zuweisungen** aus.

5. Überprüfen Sie auf der Registerkarte **Zuschussfähige Zuweisungen** in der Spalte "Aktion" die verfügbaren Optionen.

6. Wählen Sie **Entfernen**.

7. Überprüfen Sie im Dialogfeld **Entfernen** die Informationen, und klicken Sie auf **Ja**.
