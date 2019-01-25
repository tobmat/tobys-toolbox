---
description: CLI Access
---

# Hammer

#### From satellite instance, logged in as root 

CLI config file: 

`/root/.hammer/cli_config.yml` 

`hammer ping`  \# gives response time and status of candlepin, candlepin\_auth, pulp, and foreman\_tasks 

#### HOST 

`hammer host -h` \# list all host commands 

`hammer host list` \# list all instances registered to satellite 

#### DOMAIN 

`hammer domain -h` \# list help for all domain commands  

`hammer domain list` \# list all domains 

`hammer domain info --id 5` \# get details about specific domain 

#### ORGANIZATION 

hammer organization list 

hammer organization info --name Genesys \# list details about given organization 

#### CAPSULE 

`hammer capsule list` 

`hammer capsule info --id 1` \# includes capsule details 

Note – proxy command gives same results 

#### PRODUCT – What is difference between product and repo in Satellite? 

`hammer product list --organization Genesys` \# product / repo list 

#### REPOSITORY 

`hammer repository list --organization Genesys | awk -F '|' '{ print $2 }'` \# prints repo names in org 

#### CONTENT HOST 

`hammer content-host list --organization Genesys`  

#### SHELL – interactive shell for hammer 

`hammer shell` 

#### SUBNET 

`hammer subnet list` 

`hammer subnet info --id 1` 

