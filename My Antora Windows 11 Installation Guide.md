# DRAFT - My Antora Windows 11 Installation Guide

## Assumption(s)

* [x] A GitHub repository is ready to start working from.
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

```sh
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

```sh
volta install node
```

For more detail, see Volta's [Getting Started](https://docs.volta.sh/guide/getting-started) guide.

#### Option 2: Manually Install a Specific Version of Node.js

1. Find the latest LTS release version number at [Node.js Releases](https://nodejs.org/en/about/previous-releases).
1. Open **PowerShell**.
1. Run the following command:

```sh
volta install node@<version_number>
```

For more detail, see Volta's [Getting Started](https://docs.volta.sh/guide/getting-started) guide.

## Per-Project Installation

### Install Antora Locally to Each Project

1. Open **VS Code**.
1. Select **CTRL+`** to open **Terminal**.
1. Run the following command:

```sh
cd <project_directory_name>
```

4. Install **Antora CLI** by running the following command:

```sh
node -e "fs.writeFileSync('package.json', '{}')"; if ($?) {npm i -D -E @antora/cli@<version number>}
```

5. Install **Antora Site Generator** by running the following command:

```sh
npm i -D -E @antora/site-generator@<version_number>
```

6. Confirm the **Antora CLI** and **Site Generator** installations by running the following command:

```sh
npx antora -v
```

For more detail, see [Install Antora](https://docs.antora.org/antora/latest/install/install-antora/).

### Configure GitHub Linguist

**Note:** These Linguist configuration steps affect how language stats are displayed *only on public* repositories. Skip them for private repositories.

#### Exclude Generated HTML from GitHub Repo Stats

1. Add the following code to **.gitattributes**:

```gitattributes
# Exclude generated HTML from repo language stats
*.html linguist-generated
```

#### Exclude Vendored Code from GitHub Repo Stats

1. Add the following code to **.gitattributes**:

```gitattributes
# Exclude vendored code from repo language stats
<directory_name>/node_modules/** linguist-vendored
<directory_name>/package-lock.json linguist-vendored
<directory_name>/package.json linguist-vendored
```

#### Include README.md in GitHub Repo Stats

1. Add the following code to **.gitattributes**:

```gitattributes
# Include README.md in repo language stats
README.md -linguist-documentation
```

### Configure GitHub Pages or Another Static Site Host

...

### Configure the Antora Playbook

This is a basic playbook, written in YAML:

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

For more detail, see:

* [Antora Playbook Introduction](https://docs.antora.org/antora/latest/playbook/)
* [Set Up a Playbook](https://docs.antora.org/antora/latest/playbook/set-up-playbook/)

#### Configure Content Sources in the Playbook

##### URL Key

If the content source is the same repository that contains the playbook, configure the URL as follows:

```yml
content:
  sources:
  - url: .   
```

For more detail, see [URLs for Content Sources](https://docs.antora.org/antora/latest/playbook/content-source-url/) 

##### Branches Key

The **branches:** key can take the following values:

* ...




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

```sh
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