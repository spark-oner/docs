---
title: Configuring secret scanning for your repositories
intro: 'You can configure how {% data variables.product.prodname_dotcom %} scans your repositories for secrets.'
permissions: 'People with admin permissions to a repository can enable {% data variables.product.prodname_secret_scanning %} for the repository.'
redirect_from:
  - /github/administering-a-repository/configuring-secret-scanning-for-private-repositories
  - /github/administering-a-repository/configuring-secret-scanning-for-your-repositories
  - /code-security/secret-security/configuring-secret-scanning-for-your-repositories
product: '{% data reusables.gated-features.secret-scanning %}'
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
  ghec: '*'
type: how_to
topics:
  - Secret scanning
  - Advanced Security
  - Repositories
shortTitle: Configure secret scans
---

{% data reusables.secret-scanning.beta %}
{% data reusables.secret-scanning.enterprise-enable-secret-scanning %}

{% ifversion fpt or ghec %}
{% note %}

**Note:** {% data variables.product.prodname_secret_scanning_caps %} is enabled by default on public repositories and cannot be turned off. You can configure {% data variables.product.prodname_secret_scanning %} for your private repositories only.

{% endnote %}
{% endif %}

## Enabling {% data variables.product.prodname_secret_scanning %} for {% ifversion fpt or ghec %}private {% endif %}repositories

{% ifversion ghes or ghae-next %}
You can enable {% data variables.product.prodname_secret_scanning %} for any repository that is owned by an organization.
{% endif %} Once enabled, {% data reusables.secret-scanning.secret-scanning-process %}

{% data reusables.repositories.navigate-to-repo %}
{% data reusables.repositories.sidebar-settings %}
{% data reusables.repositories.navigate-to-security-and-analysis %}
{% ifversion fpt or ghes > 3.0 or ghae-next or ghec %}
4. If {% data variables.product.prodname_advanced_security %} is not already enabled for the repository, to the right of "{% data variables.product.prodname_GH_advanced_security %}", click **Enable**.
   {% ifversion fpt or ghec %}![Enable {% data variables.product.prodname_GH_advanced_security %} for your repository](/assets/images/help/repository/enable-ghas-dotcom.png)
   {% elsif ghes > 3.0 or ghae-next %}![Enable {% data variables.product.prodname_GH_advanced_security %} for your repository](/assets/images/enterprise/3.1/help/repository/enable-ghas.png){% endif %}
5. Review the impact of enabling {% data variables.product.prodname_advanced_security %}, then click **Enable {% data variables.product.prodname_GH_advanced_security %} for this repository**.
6. When you enable {% data variables.product.prodname_advanced_security %}, {% data variables.product.prodname_secret_scanning %} may automatically be enabled for the repository due to the organization's settings. If "{% data variables.product.prodname_secret_scanning_caps %}" is shown with an **Enable** button, you still need to enable {% data variables.product.prodname_secret_scanning %} by clicking **Enable**. If you see a **Disable** button, {% data variables.product.prodname_secret_scanning %} is already enabled. ![Enable {% data variables.product.prodname_secret_scanning %} for your repository](/assets/images/help/repository/enable-secret-scanning-dotcom.png)
   {% elsif ghes = 3.0 %}
7. To the right of "{% data variables.product.prodname_secret_scanning_caps %}", click **Enable**. ![Enable {% data variables.product.prodname_secret_scanning %} for your repository](/assets/images/help/repository/enable-secret-scanning-ghe.png)
   {% endif %}
{% ifversion ghae %}
1. Before you can enable {% data variables.product.prodname_secret_scanning %}, you need to enable {% data variables.product.prodname_GH_advanced_security %} first. To the right of "{% data variables.product.prodname_GH_advanced_security %}", click **Enable**. ![Enable {% data variables.product.prodname_GH_advanced_security %} for your repository](/assets/images/enterprise/github-ae/repository/enable-ghas-ghae.png)
2. Click **Enable {% data variables.product.prodname_GH_advanced_security %} for this repository** to confirm the action. ![Confirm enabling {% data variables.product.prodname_GH_advanced_security %} for your repository](/assets/images/enterprise/github-ae/repository/enable-ghas-confirmation-ghae.png)
3. To the right of "{% data variables.product.prodname_secret_scanning_caps %}", click **Enable**. ![Enable {% data variables.product.prodname_secret_scanning %} for your repository](/assets/images/enterprise/github-ae/repository/enable-secret-scanning-ghae.png)
{% endif %}

## Excluding alerts from {% data variables.product.prodname_secret_scanning %} in {% ifversion fpt or ghec %}private {% endif %}repositories

Du kannst eine *secret_scanning.yml*-Datei verwenden, um Verzeichnisse von {% data variables.product.prodname_secret_scanning %} auszuschließen. Beispielsweise kannst Du Verzeichnisse ausschließen, welche Tests oder zufällig generierte Inhalte enthalten.

{% data reusables.repositories.navigate-to-repo %}
{% data reusables.files.add-file %}
3. Gib im Feld „Dateiname" *.github/secret_scanning.yml* ein.
4. Gib unter **Edit new file** (Neue Datei bearbeiten) `paths-ignore:` ein, gefolgt von den Pfaden, die Du von {% data variables.product.prodname_secret_scanning %} ausschließen willst.
    ``` yaml
    paths-ignore:
      - "foo/bar/*.js"
    ```

    Du kannst Sonderzeichen wie `*` verwenden, um Pfade zu filtern. Weitere Informationen zu Filtermustern findest Du unter „[Workflow-Syntax für GitHub-Aktionen](/actions/reference/workflow-syntax-for-github-actions#filter-pattern-cheat-sheet)."

    {% note %}

    **Hinweise:**
    - Wenn es mehr als 1.000 Einträge in `paths-ignore` gibt, wird {% data variables.product.prodname_secret_scanning %} nur die ersten 1.000 Verzeichnisse von Scans ausschließen.
    - Wenn *secret_scanning.yml* größer als 1 MB ist, wird {% data variables.product.prodname_secret_scanning %} die ganze Datei ignorieren.

    {% endnote %}

Du kannst auch einzelne Warnungen von {% data variables.product.prodname_secret_scanning %} ignorieren. Weitere Informationen findest Du unter „[Warnungen von {% data variables.product.prodname_secret_scanning %} verwalten](/github/administering-a-repository/managing-alerts-from-secret-scanning#managing-secret-scanning-alerts)."

## Weiterführende Informationen

- "[Managing security and analysis settings for your organization](/organizations/keeping-your-organization-secure/managing-security-and-analysis-settings-for-your-organization)"
{% ifversion fpt or ghes > 3.1 or ghae-next or ghec %}- "[Defining custom patterns for {% data variables.product.prodname_secret_scanning %}](/code-security/secret-security/defining-custom-patterns-for-secret-scanning)"{% endif %}
