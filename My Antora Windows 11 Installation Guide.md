# DRAFT - My Antora Windows 11 Installation Guide

## Assumption(s)

* [x] A GitHub repository is ready to work from.
* [x] That GitHub repository contains these files in its root:
  * [x] **.gitattributes**
  * [x] **README.md** 

## Contents

* [First-Time Installation](#first-time-installation)
  * [Install Volta](#install-volta)
  * [Install Node.js with Volta](#install-nodejs-with-volta)
* [Per-Project Installation](#per-project-installation)
  * [Install Antora Locally to Each Project](#install-antora-locally-to-each-project)
  * [Configure GitHub Linguist](#configure-github-linguist)
  * [Configure GitHub Pages or Another Static Site Host](#configure-github-pages-or-another-static-site-host)
  * [Configure the Antora Playbook](#configure-the-antora-playbook)
  * [Organize Antora Content Files](#organize-antora-content-files)
  * [Configure antora.yml](#configure-antorayml)
  * [Configure Supplemental UI Directories](#configure-supplemental-ui-directories)
  * [Install the Lunr Search Extension Locally to Each Project](#install-the-lunr-search-extension-locally-to-each-project)
  * [Generate Sites Locally](#generate-sites-locally)
  * [Deploy Sites Online](#deploy-sites-online)


## First-Time Installation

### Install Volta

1. Open **PowerShell**.
1. Run the following command:

```
winget install Volta.Volta
```

For more detail, see Volta's [Getting Started](https://docs.volta.sh/guide/getting-started) guide.

### Install Node.js with Volta

#### Node.js Terminology

<dl>
  <dt>LTS</dt>
  <dd>Long-Term Support
</dl>

#### Option 1: Automatically Install the Latest LTS Release of Node.js

1. Open **PowerShell**.
1. Run the following command:

```
volta install node
```

For more detail, see Volta's [Getting Started](https://docs.volta.sh/guide/getting-started) guide.

#### Option 2: Manually Install a Specific Version of Node.js

1. Find the latest LTS release version number at [Node.js Releases](https://nodejs.org/en/about/previous-releases).
1. Open **PowerShell**.
1. Run the following command:

```
volta install node@<version_number>
```

For more detail, see Volta's [Getting Started](https://docs.volta.sh/guide/getting-started) guide.

## Per-Project Installation

### Install Antora Locally to Each Project

1. Open **VS Code**.
1. Select **CTRL+`** to open **Terminal**.
1. Run the following command:

```
cd <project_directory_name>
```

4. Install **Antora CLI** by running the following command:

```
node -e "fs.writeFileSync('package.json', '{}')"; if ($?) {npm i -D -E @antora/cli@<version number>}
```

5. Install **Antora Site Generator** by running the following command:

```
npm i -D -E @antora/site-generator@<version_number>
```

6. Confirm the **Antora CLI** and **Site Generator** installations by running the following command:

```
npx antora -v
```

For more detail, see [Install Antora](https://docs.antora.org/antora/latest/install/install-antora/).

### Configure GitHub Linguist

> [!TIP] 
> These Linguist configuration steps affect how language stats are displayed *only on public* repositories. 
>
> Skip these steps for private repositories.

#### Exclude Generated HTML from GitHub Repo Stats

1. Add the following code to **.gitattributes**:

```gitattributes
# Exclude generated HTML from repo language stats
*.html linguist-generated
```
For more detail, see GitHub Linguist [Overrides](https://github.com/github-linguist/linguist/blob/main/docs/overrides.md#generated-code).

#### Exclude Vendored Code from GitHub Repo Stats

1. Add the following code to **.gitattributes**:

```gitattributes
# Exclude vendored code from repo language stats
<directory_name>/node_modules/** linguist-vendored
<directory_name>/package-lock.json linguist-vendored
<directory_name>/package.json linguist-vendored
```
For more detail, see GitHub Linguist [Overrides](https://github.com/github-linguist/linguist/blob/main/docs/overrides.md#vendored-code).

#### Include README.md in GitHub Repo Stats

1. Add the following code to **.gitattributes**:

```gitattributes
# Include README.md in repo language stats
README.md -linguist-documentation
```

For more detail, see GitHub Linguist [Overrides](https://github.com/github-linguist/linguist/blob/main/docs/overrides.md#documentation).

### Configure GitHub Pages or Another Static Site Host

...

### Configure the Antora Playbook

1. Write a basic playbook in YAML:

```yml
site:
  title: <site_name>
  url: <url>
  start_page: <component_name>::index.adoc
content:
  sources:
  - url: <repo_url>.git
    branches: <branch_name(s)>
    start_path: <content_root_directory>
ui:
  bundle:
    url: <url>
    snapshot: true
```

> [!IMPORTANT]
> The playbook file extension must be **.yml**.   

For more detail, see:

* [Antora Playbook Introduction](https://docs.antora.org/antora/latest/playbook/)
* [Set Up a Playbook](https://docs.antora.org/antora/latest/playbook/set-up-playbook/)

#### Configure Content Sources in the Playbook

##### URL Key

1. If the content source is the same repository that contains the playbook, configure the URL as follows:

```yml
content:
  sources:
  - url: .
    branches: <branch_name(s)>
    start_path: <content_root_directory>     
```
2. If the content source is from an external repository, configure the URL as follows:

```yml
content:
  sources:
  - url: <repo_url>.git
    branches: <branch_name(s)>
    start_path: <content_root_directory>
```

3. If the content is spread across more than one repository, configure as many URLs as required:

```yml
content:
  sources:
  - url: <repo_url>.git
    branches: <branch_name(s)>
    start_path: <content_root_directory>
  - url: <repo_url>.git
    branches: <branch_name(s)>
    start_path: <content_root_directory>
  - url: <repo_url>.git
    branches: <branch_name(s)>
    start_path: <content_root_directory>
# ...        
```

For more detail, see [URLs for Content Sources](https://docs.antora.org/antora/latest/playbook/content-source-url/). 

##### Branches Key

The `branches` key can take the following values.

| Value | Description |
| --- | --- |
| `HEAD` | Reserved value for the current branch of a local repository |
| Branch name | Examples include `branches: v9.1` or `branches: '9.2'` |
| Pattern | See [Specify Branches by Pattern](https://docs.antora.org/antora/latest/playbook/content-branches/#glob-pattern) |
| Exclusion | See [Exclude Branches by Pattern](https://docs.antora.org/antora/latest/playbook/content-branches/#exclude-branches-by-pattern) |
Filter | See [Default Branches Filter](https://docs.antora.org/antora/latest/playbook/content-branches/#default) |
List | Any combination of the above value types, comma separated, and enclosed by square brackets, such as `branches: [HEAD, v1.*, '2.0']`

> [!IMPORTANT]
> If a value begins with a number or symbol, enclose it with single quotation marks.

#### Configure the UI in the Playbook

...

### Organize Antora Content Files

This is the standard file and directory set:

```text
<content_root_name>
  antora.yml
  modules
    ROOT
      attachments
      examples
      images
      pages
      partials
      nav.adoc
    <named_module>
      pages
      nav.adoc
```
The **modules** directory must contain **either** *or* **both** of the following:

* a **ROOT** module directory
* at least one named module directory

Module directories must contain at lease one child directory. Including **nav.adoc** is optional.

For more detail, see:

* [How to Organize Your Content Files](https://docs.antora.org/antora/latest/organize-content-files/)
* [Repositories and Content Source Roots](https://docs.antora.org/antora/latest/content-source-repositories/)
* [Content Source Versioning Methods](https://docs.antora.org/antora/latest/content-source-versioning-methods/)
* [Standard File and Directory Set](https://docs.antora.org/antora/latest/standard-directories/)

### Configure antora.yml

> [!IMPORTANT]
> The **antora.yml** file extension must be **.yml**.  

For more detail, see:

* [What’s antora.yml?](https://docs.antora.org/antora/latest/component-version-descriptor/)

### Configure Supplemental UI Directories

...

#### Register Supplmental UI in the Antora Playbook

...

### Install the Lunr Search Extension Locally to Each Project

1. Open **VS Code**.
1. Select **CTRL+`** to open **Terminal**.
1. Run the following command:

```
npm i @antora/lunr-extension
```

For more detail, see the Antora Lunr Extension [README](https://gitlab.com/antora/antora-lunr-extension/-/blob/main/README.adoc?ref_type=heads).


#### Register Lunr Search in the Antora Playbook

Add this code to the Antora playbook:

```yml
antora:
  extensions:
  - require: '@antora/lunr-extension'
```
For more detail and options, see the Antora Lunr Extension [README](https://gitlab.com/antora/antora-lunr-extension/-/blob/main/README.adoc?ref_type=heads).

### Generate Sites Locally

For more detail, see [Run Antora to Generate Your Site](https://docs.antora.org/antora/latest/run-antora/).

### Deploy Sites Online

...