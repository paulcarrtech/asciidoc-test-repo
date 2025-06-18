# DRAFT - My Asciidoctor Windows 11 Installation Guide

The following instructions assume a GitHub repository is ready to start working from.

## Contents

* [First-Time Installation](#first-time-installation)
  * [Install VS Code](#install-vs-code)
  * [Install Ruby](#install-ruby)
  * [Install Asciidoctor](#install-asciidoctor)
* [Per-Project Installation and Configuration](#per-project-installation-and-configuration)
  * [Configure GitHub Linguist](#configure-github-linguist)

## First-Time Installation

### Install VS Code

1. Download and install [Visual Studio Code](https://code.visualstudio.com/download) (VS Code).

#### Install the VS Code AsciiDoc Extension

1. Install Asciidoctor's AsciiDoc extension for VS Code:
    * from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=asciidoctor.asciidoctor-vscode)
    * or from the VS Code extensions browser:
      * select **View > Extensions** 
      * or select **CTRL+SHIFT+X**
    * or from VS Code *Quick Open*
      * select **Go > Go to File** 
      * or select **CTRL+P** 
      * and run the following command:

```
ext install asciidoctor.asciidoctor-vscode  
``` 

### Install Git

1. Download a [standalone Git installer](https://git-scm.com/downloads/win).

> [!IMPORTANT]
> Ignore the instructions for installing Git with **winget**. 

2. Run the installer as an adminstrator.

### Install Ruby

1. Download and install [RubyInstaller](https://rubyinstaller.org/downloads/).

### Install Asciidoctor

1. Open **PowerShell**.
1. Run the following command:

```
gem install asciidoctor
```

For more detail, see Asciidoctor's [Gem Install](https://docs.asciidoctor.org/asciidoctor/latest/install/ruby-packaging/#gem-install) guide. 

> [!IMPORTANT]
> **Ignore** the instructions about RVM.

#### Install Asciidoctor PDF

1. Open **PowerShell**.
1. Run the following command:

```
  gem install asciidoctor-pdf
```

For more detail, see [Install Asciidoctor PDF](https://docs.asciidoctor.org/pdf-converter/latest/install/#install-asciidoctor-pdf).

## Per-Project Installation and Configuration

### Configure GitHub Linguist

> [!TIP]
> These Linguist configuration steps affect how language stats are displayed *only on public* repositories.
>
> Skip these steps for private repositories.

#### Include AsciiDoc, Markdown, and YAML in GitHub Repo Stats

1. Add the following code to **.gitattributes**:

```gitattributes
# Include .adoc, .md, and .yml in repo language stats
*.adoc linguist-detectable
*.md linguist-detectable
*.yml linguist-detectable
```
For more detail, see GitHub Linguist's [overrides for detectable languages](https://github.com/github-linguist/linguist/blob/main/docs/overrides.md#detectable).

#### Exclude Generated HTML from GitHub Repo Stats

1. Add the following code to **.gitattributes**:

```gitattributes
# Exclude generated HTML from repo language stats
*.html linguist-generated
```
For more detail, see GitHub Linguist's [overrides for generated code](https://github.com/github-linguist/linguist/blob/main/docs/overrides.md#generated-code).

#### Exclude Vendored Code from GitHub Repo Stats

1. Add the following code to **.gitattributes**:

```gitattributes
# Exclude vendored code from repo language stats
<directory_name>/asciidoctor-default.css linguist-vendored
```

For more detail, see GitHub Linguist's [overrides for vendored code](https://github.com/github-linguist/linguist/blob/main/docs/overrides.md#vendored-code).

#### Include README.md in GitHub Repo Stats

1. Add the following code to **.gitattributes**:

```gitattributes
# Include README.md in repo language stats
README.md -linguist-documentation
```

For more detail, see GitHub Linguist's [overrides for documentation](https://github.com/github-linguist/linguist/blob/main/docs/overrides.md#documentation).