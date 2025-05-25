# DRAFT - My Asciidoctor Windows 11 Installation Guide

The following instructions assume a GitHub repository is ready to start working from.

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

### Install Ruby

1. Download and install [RubyInstaller](https://rubyinstaller.org/downloads/).

### Install Asciidoctor

1. Open **PowerShell**.
1. Run the following command:

```
gem install asciidoctor
```

For more detail, see Asciidoctor's [Gem Install](https://docs.asciidoctor.org/asciidoctor/latest/install/ruby-packaging/#gem-install) guide. **But ignore** the instructions about RVM.

#### Install Asciidoctor PDF

1. Open **PowerShell**.
1. Run the following command:

```
  gem install asciidoctor-pdf
```

For more detail, see [Install Asciidoctor PDF](https://docs.asciidoctor.org/pdf-converter/latest/install/#install-asciidoctor-pdf).

## Per-Project Installation

### Configure the GitHub Repository

#### Include AsciiDoc, Markdown, and YAML in GitHub Repo Stats

1. Add the following code to **.gitattributes**:

```
# Include .adoc, .md, and .yml in repo language stats
*.adoc linguist-detectable
*.md linguist-detectable
*.yml linguist-detectable
```

#### Remove Generated HTML from GitHub Repo Stats

1. Add the following code to **.gitattributes**:

```
# Exclude generated HTML from repo language stats
*.html linguist-generated
```

#### Remove Vendored Code from GitHub Repo Stats

1. Add the following code to **.gitattributes**:

```
# Exclude vendored code from repo language stats
<directory_name>/asciidoctor-default.css linguist-vendored
```
#### Include README.md in GitHub Repo Stats

1. Add the following code to **.gitattributes**:

```
# Include README.md in repo language stats
README.md -linguist-documentation
```