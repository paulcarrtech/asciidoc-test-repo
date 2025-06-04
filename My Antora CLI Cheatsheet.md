# My Antora CLI Cheatsheet

## Build an Antora Site

```sh
npx antora <directory_name/playbook_name>.yml
```

If Antora fails early in its process, yet there are no aparent issues with the playbook and path structure, try the following command:
    
```sh
npx antora --clean --fetch --log-level debug antora-playbook.yml
```