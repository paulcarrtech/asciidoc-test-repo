# DRAFT - My Antora Windows 11 Installation Guide

The following instructions assume a GitHub repository is ready to start working from.

## First-Time Installation

### Install Volta

1. Open **PowerShell**.
1. Run the following command:

```
winget install Volta.Volta
```

For more detail, see Volta's [Getting Started](https://docs.volta.sh/guide/getting-started) guide.

### Install Node.js

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

### Configure the GitHub Repository

#### Configure .gitattributes

##### Exclude Vendored Code from GitHub Repo Stats

1. Add the following code to **.gitattributes**:

```
# Exclude vendored code from repo language stats
<directory_name>/node_modules/** linguist-vendored
<directory_name>/package-lock.json linguist-vendored
<directory_name>/package.json linguist-vendored
```

#### Configure GitHub Pages

### Set Up Playbooks

For more detail, see [Antora Playbook Introduction](https://docs.antora.org/antora/latest/playbook/).

### Organize Content Files

For more detail, see [How to Organize Your Content Files](https://docs.antora.org/antora/latest/organize-content-files/).

### Generate Sites

For more detail, see [Run Antora to Generate Your Site](https://docs.antora.org/antora/latest/run-antora/).