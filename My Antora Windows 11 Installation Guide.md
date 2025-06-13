# DRAFT - My Antora Windows 11 Installation Guide

## Assumption(s)

* [x] Asciidoctor and its dependencies have been installed.
  * See [My Asciidoctor Windows 11 Installation Guide](https://github.com/paulcarrtech/asciidoc-test-repo/blob/main/My%20Asciidoctor%20Windows%2011%20Installation%20Guide.md).
* [x] A GitHub repository is ready to work from.
* [x] That GitHub repository contains these files in its root:
  * [x] **.gitattributes**
  * [x] **README.md** 

## Contents

* [First-Time Installation](#first-time-installation)
  * [Install Volta](#install-volta)
  * [Install Node.js with Volta](#install-nodejs-with-volta)
* [Per-Project Installation and Configuratio](#per-project-installation-and-configuration)
  * [Install Antora Locally to Each Project](#install-antora-locally-to-each-project)
  * [Configure GitHub Linguist](#configure-github-linguist)
  * [Configure GitHub Pages or Another Static Site Host](#configure-github-pages-or-another-static-site-host)
  * [Configure the Antora Playbook](#configure-the-antora-playbook)
  * [Organize Antora Content Files](#organize-antora-content-files)
  * [Configure antora.yml](#configure-antorayml)
  * [Configure Each Module's nav.adoc](#configure-each-modules-navadoc)
  * [Install the Lunr Search Extension Locally to Each Project](#install-the-lunr-search-extension-locally-to-each-project)
  * [Configure Supplemental UI Directories](#configure-supplemental-ui-directories)
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

## Per-Project Installation and Configuration

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

#### Include AsciiDoc, Markdown, and YAML in GitHub Repo Stats

1. Add the following code to .gitattributes:

```gitattributes
# Include .adoc, .md, and .yml in repo language stats
*.adoc linguist-detectable
*.md linguist-detectable
*.yml linguist-detectable
```

For more detail, see GitHub Linguist's [overrides for detectable languages](https://github.com/github-linguist/linguist/blob/main/docs/overrides.md#detectable).

#### Exclude Generated Code from GitHub Repo Stats

1. Add the following code to **.gitattributes**:

```gitattributes
# Exclude generated HTML from repo language stats
*.html linguist-generated
build/site/**.xml linguist-generated
build/site/**.js linguist-generated
build/site/**.css linguist-generated
```
For more detail, see GitHub Linguist's [overrides for generated code](https://github.com/github-linguist/linguist/blob/main/docs/overrides.md#generated-code).

#### Exclude Vendored Code from GitHub Repo Stats

1. Add the following code to **.gitattributes**:

```gitattributes
# Exclude vendored code from repo language stats
<directory_name>/node_modules/** linguist-vendored
<directory_name>/package-lock.json linguist-vendored
<directory_name>/package.json linguist-vendored
```
For more detail, see GitHub Linguist's [overrides for vendored code](https://github.com/github-linguist/linguist/blob/main/docs/overrides.md#vendored-code).

#### Include README.md in GitHub Repo Stats

1. Add the following code to **.gitattributes**:

```gitattributes
# Include README.md in repo language stats
README.md -linguist-documentation
```

For more detail, see GitHub Linguist's [overrides for documentation](https://github.com/github-linguist/linguist/blob/main/docs/overrides.md#documentation).

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
> The playbook file's extension must be **.yml**.   

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

1. Register an existing UI with the following code:

```yml
ui:
  bundle:
    url: <url>
    snapshot: true
```

> [!Tip]
> Register the following URL for the default Antora UI: `https://gitlab.com/antora/antora-ui-default/-/jobs/artifacts/HEAD/raw/build/ui-bundle.zip?job=bundle-stable`

2. To customize an existing UI, see [Configure Supplemental UI Directories](#configure-supplemental-ui-directories) below. 

For more detail and options, see:
* [UI Keys](https://docs.antora.org/antora/latest/playbook/configure-ui/)
* [UI Bundle URL](https://docs.antora.org/antora/latest/playbook/ui-bundle-url/)
* [UI Output Directory](https://docs.antora.org/antora/latest/playbook/ui-output-dir/)
* [Default Layout for Pages](https://docs.antora.org/antora/latest/playbook/ui-default-layout/)

### Organize Antora Content Files

1. Organize your content with a structure similar to this example of the standard file and directory set:

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

> [!IMPORTANT]
> * The **modules** directory must contain **either** *or* **both** of the following:
>
>   * a **ROOT** module directory
>   * at least one named module directory
> * Each **ROOT** or named module directory must contain at least one child directory.
>   * `attachments`, `examples`, `images`, `pages`, and `partials` are reserved directory names.
>   * Child directories can optionally contain subdirectories.
> * Including **nav.adoc** in the **ROOT** or named module directory is optional.

For more detail, see:

* [How to Organize Your Content Files](https://docs.antora.org/antora/latest/organize-content-files/)
* [Repositories and Content Source Roots](https://docs.antora.org/antora/latest/content-source-repositories/)
* [Content Source Versioning Methods](https://docs.antora.org/antora/latest/content-source-versioning-methods/)
* [Standard File and Directory Set](https://docs.antora.org/antora/latest/standard-directories/)

### Configure antora.yml

> [!IMPORTANT]
> The **antora.yml** file's extension must be **.yml**.  

1. Create the file **antora.yml** in the content root directory at the same level as the modules directory:

```text
<content_root_name>
  antora.yml
  modules
```

2. Add the following key-value pairs to **antora.yml**:

<a name="antora.yml-sample"></a>
```yml
name: <component_name>
version: <version_number_or_name>
title: <component_title>
nav:
- modules/<ROOT_or_named_module_directory>/nav.adoc
```

> [!TIP]
> If your content has multiple module directories, register the path to each module's nav.adoc under the `nav:` key as a separate line prefixed with a hyphen and space: 
>
> ```yml
> nav:
> - modules/ROOT/nav.adoc
> - modules/<named_module_1>/nav.adoc
> - modules/<named_module_2>/nav.adoc
>``` 

#### Key-Value Pairs for antora.yml 

There are two required key-value pairs for antora.yml.

| Required Key | Value |
| --- | --- |
| `name:` | Lowercase, alphanumeric name; optionally separated by underscores, hyphens, or periods |
| `version:` | Lowercase, alphanumeric identifier; optionally separated by underscores, hyphens, or periods &bull; Can be a named identifier (such as `sequoia`) or semantic identifier (such as `'7.0'` or `'7.x'`) &bull; For other options, see [Version Key](https://docs.antora.org/antora/latest/component-version-key/#key) |

> [!IMPORTANT]
> If the version key's value begins with a number, enclose it with single quotation marks.

> [!TIP]
> To include uppercase letters, spaces, or special characters when identifying the version, see [Customize the Display Version](https://docs.antora.org/antora/latest/component-display-version/). 

There are several optional key-value pairs for antora.yml. The following table lists some examples.

| Optional Key | Value |
| --- | --- |
| `title:` | Overrides the name key's value for user-facing display &bull; Can contain uppercase letters, spaces, and special characters &bull; Should be consistent across all versions of a component to avoid confusion |
| `nav:` | Registers **nav.adoc** for each module of the component &bull; See the [sample above](#antora.yml-sample) for the value's syntax |

For more detail and other options, see:

* [What's a Component Version?](https://docs.antora.org/antora/latest/component-version/)
* [What’s antora.yml?](https://docs.antora.org/antora/latest/component-version-descriptor/)
* [Define a Component Version](https://docs.antora.org/antora/latest/component-name-and-version/)
* [Identify a Prerelease Version](https://docs.antora.org/antora/latest/component-prerelease/)
* [Assign Attributes to a Component Version](https://docs.antora.org/antora/latest/component-attributes/)
* [Version Facets](https://docs.antora.org/antora/latest/version-facets/)

### Configure Each Module's nav.adoc

| Type | Syntax |
| --- | --- |


For more detail and options, see: 

* [Navigation Files and Lists](https://docs.antora.org/antora/latest/navigation/files-and-lists/)
* [Create a Navigation File with One List](https://docs.antora.org/antora/latest/navigation/single-list/)
* [Create a Navigation File with Multiple Lists](https://docs.antora.org/antora/latest/navigation/multiple-lists/)

### Install the Lunr Search Extension Locally to Each Project

1. Open **VS Code**.
1. Select **CTRL+`** to open **Terminal**.
1. Run the following command:

```
npm i @antora/lunr-extension
```

For more detail, see the Antora Lunr Extension [README](https://gitlab.com/antora/antora-lunr-extension/-/blob/main/README.adoc?ref_type=heads).

#### Register Lunr Search in the Antora Playbook

1. Add this code to the Antora playbook:

```yml
antora:
  extensions:
  - require: '@antora/lunr-extension'
```
For more detail and options, see the Antora Lunr Extension [README](https://gitlab.com/antora/antora-lunr-extension/-/blob/main/README.adoc?ref_type=heads).

### Configure Supplemental UI Directories

1. In the root of the playbook project, add a `supplemental-ui` folder.
1. Add UI components to this folder.

> [!IMPORTANT]
> The structure of the **supplemental-ui** folder must match that of the original UI, yet the folder need only contain the files necessary for customization.
> For example, if using the [Antora default UI](https://gitlab.com/antora/antora-ui-default/-/tree/master/src), your supplemental-ui folder might look like this:
> ```text
> supplemental-ui
>  partials
>   footer-content.hbs
>   head-styles.hbs 
>   header-content.hbs

3. Customize the supplemental UI components as your project requires.

> [!TIP]
> You can copy the full code from an original UI component into the corresponding file in the **supplemental-ui** folder. You can then customize that code in the local component. This will overwrite the equivalant UI component when Antora builds the site.    

For more detail, see:

* [Supplemental UI](https://docs.antora.org/antora/latest/playbook/ui-supplemental-files/)
* [The relationship between the supplement UI and CSS](https://gitlab.com/antora/antora/-/issues/149#note_140294252)

#### Register the Supplmental UI in the Antora Playbook

1. Register the **supplmental-ui** folder with the following code:

```yml
ui:
  bundle:
    url: <url>
    snapshot: true
  supplemental_files: supplmental-ui
```

> [!Tip] 
> Register the following URL for the default Antora UI: `https://gitlab.com/antora/antora-ui-default/-/jobs/artifacts/HEAD/raw/build/ui-bundle.zip?job=bundle-stable`

For more detail, see [Supplemental UI](https://docs.antora.org/antora/latest/playbook/ui-supplemental-files/).

### Generate Sites Locally

For more detail, see [Run Antora to Generate Your Site](https://docs.antora.org/antora/latest/run-antora/).

### Deploy Sites Online

...