# DRAFT - My Antora CLI Cheatsheet

## Build an Antora Site

```
npx antora <directory_name/playbook_name>.yml
```

If Antora fails early in its process, yet there are no aparent issues with the playbook and module(s) path structure, try the following command:
    
```
npx antora --clean --fetch --log-level debug <directory_name/playbook_name>.yml
```