# Teil 3 – Reflexion

## 1. Unterschiede im Umgang mit Variablen zwischen GitHub Actions und Jenkins

### GitHub Actions:
- Umgebungsvariablen werden über `env:` im YAML-Workflow gesetzt.
- Globale Variablen gelten für alle Jobs; lokale Variablen innerhalb eines Jobs oder Steps.
- Zugriff über `$ENV_NAME` in Shell oder `${{ env.ENV_NAME }}` in Ausdrücken.
- YAML ist deklarativ, weniger flexibel bei komplexer Logik.

### Jenkins:
- Variablen über `environment {}` in Groovy-basierter Pipeline.
- Können global, pro Stage oder dynamisch im `script`-Block gesetzt werden.
- Zugriff über `${env.VARIABLE}`.
- Groovy erlaubt mehr Logik und Flexibilität.

**Fazit:** Jenkins ist flexibler, GitHub Actions einfacher und enger integriert.

---

## 2. Vor- und Nachteile von Secrets in beiden Tools

| Aspekt              | GitHub Actions                              | Jenkins                                         |
|---------------------|---------------------------------------------|------------------------------------------------|
| **Verwaltung**       | Im GitHub-UI pro Repo/Organisation          | Über „Credentials“-System                      |
| **Zugriff**          | `${{ secrets.NAME }}`                       | `credentials('ID')`                            |
| **Sichtbarkeit**     | Automatisch maskiert                        | Muss manuell verarbeitet werden                |
| **Flexibilität**     | Nur Secret Text                             | Viele Typen: Text, SSH, Files etc.             |
| **Nachteile**        | Eingeschränkte Steuerung                    | Adminrechte häufig notwendig                   |

**Fazit:** GitHub Actions ist einfacher, Jenkins ist vielseitiger.

---

## 3. Wo würde ich `set-output` oder `credentials()` im Projektalltag verwenden?

### `set-output` (bzw. `$GITHUB_OUTPUT`)
- Wenn ein Step Daten erzeugt, die ein anderer Step braucht.
- Beispiel: Versionsermittlung im Build, Übergabe an Deployment.

### `credentials()` in Jenkins
- Für API-Zugriffe, Deployments, Docker-Logins etc.
- Beispiel: Sicherer Zugriff auf eine Deployment-Umgebung oder Cloud-API.

---

## Gesamtfazit
Beide Tools ermöglichen gute CI/CD-Automatisierung mit sicherem Variablen- und Secret-Handling.

- GitHub Actions: Schnell, einfach, gut für GitHub-zentrierte Projekte.
- Jenkins: Sehr flexibel, besonders bei komplexen Infrastrukturen oder Legacy-Systemen.
