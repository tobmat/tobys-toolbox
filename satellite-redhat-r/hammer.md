---
description: CLI Access
---

# Hammer

#### From satellite instance, logged in as root&#x20;

CLI config file:&#x20;

`/root/.hammer/cli_config.yml `

`hammer ping`  # gives response time and status of candlepin, candlepin\_auth, pulp, and foreman\_tasks&#x20;

#### HOST&#x20;

`hammer host -h `# list all host commands&#x20;

`hammer host list` # list all instances registered to satellite&#x20;

#### DOMAIN&#x20;

`hammer domain -h` # list help for all domain commands &#x20;

`hammer domain list `# list all domains&#x20;

`hammer domain info --id 5` # get details about specific domain&#x20;

#### ORGANIZATION&#x20;

hammer organization list&#x20;

hammer organization info --name Genesys # list details about given organization&#x20;

#### CAPSULE&#x20;

`hammer capsule list `

`hammer capsule info --id 1` # includes capsule details&#x20;

Note – proxy command gives same results&#x20;

#### PRODUCT – What is difference between product and repo in Satellite?&#x20;

`hammer product list --organization Genesys` # product / repo list&#x20;

#### REPOSITORY&#x20;

`hammer repository list --organization Genesys | awk -F '|' '{ print $2 }'` # prints repo names in org&#x20;

#### CONTENT HOST&#x20;

`hammer content-host list --organization Genesys `&#x20;

#### SHELL – interactive shell for hammer&#x20;

`hammer shell `

#### SUBNET&#x20;

`hammer subnet list `

`hammer subnet info --id 1 `
