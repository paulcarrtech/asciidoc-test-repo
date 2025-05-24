# DRAFT - My Asciidoctor Windows 11 Installation Guide

## Install VS Code

### Install VS Code Asciidoctor Extension

## Install Ruby

1. Download and install [RubyInstaller](https://rubyinstaller.org/downloads/).

## Install Asciidoctor

1. Open **PowerShell**.
1. Run the following command:

```
gem install asciidoctor
```

For more detail, see [Gem Install](https://docs.asciidoctor.org/asciidoctor/latest/install/ruby-packaging/#gem-install). **But ignore** the instructions about RVM.

## Install Asciidoctor PDF

1. Open **PowerShell**.
1. Run the following command:

```
  gem install asciidoctor-pdf
```

For more detail, see [Install Asciidoctor PDF](https://docs.asciidoctor.org/pdf-converter/latest/install/#install-asciidoctor-pdf).

## Configure a GitHub Repository

### Add AsciiDoc and Markdown Languages to GitHub Repo Stats

1. Add the following code to **.gitattributes**:

```
# Include LMLs in repo language stats
*.md linguist-detectable
*.adoc linguist-detectable
```

### Remove Generated HTML from GitHub Repo Stats

1. Add the following code to **.gitattributes**:

```
# Exclude generated HTML from repo language stats
*.html linguist-generated
```

### Remove Vendored Code from GitHub Repo Stats

1. Add the following code to **.gitattributes**:

```
<directory_name>/asciidoctor-default.css linguist-vendored
```
