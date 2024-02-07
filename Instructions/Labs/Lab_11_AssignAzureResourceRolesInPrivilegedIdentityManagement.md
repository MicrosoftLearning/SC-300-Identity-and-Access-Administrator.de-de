---
lab:
  title: '11: Zuweisen von Azure-Ressourcenrollen in Privileged Identity Management'
  learning path: '02'
  module: Module 02 - Implement an authentication and access management solution
---

# Lab 11: Zuweisen von Azure-Ressourcenrollen in Privileged Identity Management

**Hinweis**: Für dieses Lab ist ein Azure Pass erforderlich. Anweisungen dazu finden Sie in Lab 00.

## Labszenario

Azure Active Directory Privileged Identity Management (Azure AD PIM) kann sowohl die integrierten Azure-Ressourcenrollen als auch benutzerdefinierte Rollen verwalten. Beispiele:

- Besitzer
- Benutzerzugriffsadministrator
- Mitwirkender
- Sicherheitsadministrator
- Sicherheits-Manager

Sie müssen einen Benutzer für eine Azure-Ressourcenrolle als „berechtigt“ festzulegen.


#### Geschätzte Dauer: 10 Minuten

### Übung 1: PIM mit Azure-Ressourcen

#### Aufgabe 1: Zuweisen von Azure-Ressourcenrollen

1. Melden Sie sich mit einem globalen Administratorkonto bei [https://portal.azure.com](https://portal.azure.com) an.

2. Suchen Sie nach **Azure AD Privileged Identity Management**, und wählen Sie es aus.

3. Wählen Sie auf der Seite „Privileged Identity Management“ im linken Navigationsbereich **Azure-Ressourcen** aus.

4. Wählen Sie im oberen Menü **Ressourcen ermitteln** aus.

5. Wählen Sie auf der Seite „Azure-Ressourcen – Ermittlung“ Ihr Abonnement aus, und wählen Sie anschließend im oberen Menü **Ressource verwalten** aus.

   ![Screenshot der Seite „Azure-Ressourcen – Ermittlung“ mit hervorgehobenem Abonnement und Option „Ressource verwalten“](./media/lp4-mod3-pim-azure-resource-management.png)

6. Überprüfen Sie im Dialogfeld **Für die ausgewählte Ressource Onboarding zur Verwaltung durchführen** die Informationen, und wählen Sie dann **OK** aus.

7. Schließen Sie nach Abschluss des Onboardingvorgangs die Seite „Azure-Ressourcen – Ermittlung“.

8. Wählen Sie auf der Seite „Azure-Azure-Ressourcen“ das Abonnement aus.

   ![Screenshot der neu hinzugefügten Azure-Ressource](./media/lp4-mod3-pim-az-resource-overview.png)

9. Wählen Sie im linken Navigationsmenü unter **Verwalten** die Option **Rollen** aus, um die Liste der Rollen für Azure-Ressourcen anzuzeigen.

10. Wählen Sie im oberen Menü **+ Zuweisungen hinzufügen** aus.

11. Wählen Sie auf der Seite „Zuweisungen hinzufügen“ das Menü **Rolle auswählen** aus, und wählen Sie dann **API-Verwaltungsdienstmitwirkender** aus.

12. Wählen Sie unter **Mitglied(er) auswählen** die Option **Keine Mitglieder ausgewählt** aus.

13. Wählen Sie **Miriam Graham** aus Ihrer Organisation aus, der die Rolle zugewiesen wird.  Wählen Sie anschließend **Auswählen** aus.

14. Wählen Sie **Weiter** aus.

15. Wählen Sie auf der Registerkarte **Einstellungen** unter **Zuweisungstyp** die Option **Berechtigt** aus.

   - Für **berechtigte** Zuweisungen muss das Mitglied der Rolle eine Aktion durchführen, um die Rolle verwenden zu können. Beispiele für Aktionen sind eine erfolgreiche Überprüfung der Multi-Faktor-Authentifizierung (MFA), die Angabe einer geschäftlichen Begründung oder das Anfordern einer Genehmigung von den angegebenen genehmigenden Personen.

   - Für **aktive** Zuweisungen ist es nicht erforderlich, dass das Mitglied eine Aktion durchführt, um die Rolle nutzen zu können. Bei als aktiv zugewiesenen Mitgliedern sind die Berechtigungen immer der Rolle zugewiesen.

16. Geben Sie die Zuweisungsdauer an, indem Sie den Start- und Endzeitpunkt für Datum und Uhrzeit ändern.

17. Wählen Sie abschließend **Zuweisen** aus.

18. Nachdem die neue Rollenzuweisung erstellt wurde, wird eine Statusbenachrichtigung angezeigt.

#### Aufgabe 2: Aktualisieren oder Entfernen der Zuweisung einer vorhandenen Ressourcenrolle

Befolgen Sie diese Anweisungen zum Aktualisieren oder Entfernen einer vorhandenen Rollenzuweisung.

1. Öffnen Sie **Azure AD Privileged Identity Management**.

2. Wählen Sie **Azure-Ressourcen** aus.

3. Wählen Sie das zu verwaltende Abonnement aus, um die Übersichtsseite zu öffnen.

4. Wählen Sie unter **Verwalten** die Option **Zuweisungen** aus.

5. Überprüfen Sie auf der Registerkarte **Berechtigte Rollen** in der Spalte „Aktion“ die verfügbaren Optionen.

6. Wählen Sie **Entfernen**.

7. Überprüfen Sie im Dialogfeld **Entfernen** die Informationen, und wählen Sie **Ja** aus.
