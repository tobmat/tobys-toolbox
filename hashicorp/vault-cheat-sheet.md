# Vault cheat sheet

### Vault setup

```
# add to bashrc
complete -C /usr/local/bin/vault vault. # add auto-complete for vault commands
export VAULT_ADDR='https://<vault url>'. # default vault address so we don’t have to pass on login

```

Help - Access help for any command via adding --help

#### Login

```
vault login -method=ldap username=toby.matherly
```

#### Helpful commands

```
# lookup current token
vault token lookup

# list secrets
vault kv list <secret path>

# show all secrets in a given key
vault kv get <secret path>/<key name>

# show specific value from a key
vault kv get -field=<field name> <secret path>/<key name>

# update a field within a key - not available in older versions of vault
vault kv patch <secret path>/<key name> <field name>=<field value>

# add / replace key - NOTE: this will overright existing key!
# use comma to add multiple fields to a secret
vault kv put <secret path>/<key name> <field name>=<field value>

# list secret store details
vault secrets list --detailed

# delete secret
vault delete secret/mgmt/infra/avi/test
OR
# in v2 deleted secrets can be restored if this command was used
vault kv delete secret/mgmt/infra/avi/test


```
