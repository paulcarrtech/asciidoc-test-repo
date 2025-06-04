# DRAFT - My Asciidoctor CLI Cheatsheet

## Asciidoctor Commands

### Asciidoctor - Apply a Custom Stylesheet

```sh
-a stylesheet=<directory_name/file_name.css>
```

### Asciidoctor - Specify the Output File and (Optional) Directory

```sh
-o <optional_directory_name>/<file_name.html>
```

### Asciidoctor - Specify Only the Output Directory

```sh
-D <directory_name>
```

## Asciidoctor PDF Commands

### Asciidoctor PDF - Apply a Built-In Theme

```sh
--theme <built-in_theme_name>
```

Built-in theme names include:

* *base*
* *default*
* *default-with-font-fallbacks*
* *default-for-print*
* *default-for-print-with-font-fallbacks*
* *default-sans*
* *default-sans-with-font-fallbacks*

### Asciidoctor PDF - Apply a Custom Theme

```sh
--theme <directory_name>/<file_name>.yml
```

### Asciidoctor PDF - Specify the Output Directory

```sh
-D <directory_name>
```

