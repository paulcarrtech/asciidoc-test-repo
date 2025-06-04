# My Antora CLI Cheatsheet

## Build an Antora Site

```bash
npx antora <directory_name/playbook_name>.yml
```

If Antora fails early in its process, yet there are no aparent issues with the playbook and path structure, try the following command:
    
```bash
npx antora --clean --fetch --log-level debug antora-playbook.yml
```