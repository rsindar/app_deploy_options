# Option 4 – one playbook, environment chosen by inventory

```
option4/
├── ansible.cfg                 # no default inventory -> you must choose an env
├── deploy.yml                  # single, environment-agnostic playbook
├── inventories/
│   ├── test/
│   │   ├── hosts.yml
│   │   └── group_vars/app/{vars.yml,vault.yml}
│   └── prod/
│       ├── hosts.yml
│       └── group_vars/app/{vars.yml,vault.yml}
└── roles/app/
    ├── meta/argument_specs.yml # validates vars, marks password no_log
    └── tasks/main.yml
```

Run:
```
ansible-playbook -i inventories/test deploy.yml
ansible-playbook -i inventories/prod deploy.yml --ask-vault-pass
```

Encrypt secrets once:
```
ansible-vault encrypt inventories/*/group_vars/app/vault.yml
```
