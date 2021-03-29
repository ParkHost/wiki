---
title: Gitlab
description: 
published: true
date: 2021-02-04T07:37:18.592Z
tags: git, gitlab, self hosted
editor: markdown
dateCreated: 2020-08-25T10:34:34.146Z
---

![docs-gitlab[1].svg](/docs-gitlab[1].svg){.align-left} One interface. 
One conversation. 
One permission model. 
Thousands of features.

----


# Intro

Gitlab let you use the perfect GIT structure on a self hosted environment.
This let you build some amazing DevOPS environment which brings the OPS's with the DEV's together.


# Docker config

## Docker compose file
> ***first set the environment variable:***
> ```js
> export GITLAB_HOME=/srv/gitlab
> ```


```yml

version: '3'

services:
  web:
    image: 'gitlab/gitlab-ce:latest'
    container_name: 'gitlab_test'
    restart: always
    hostname: 'gitlab.parkhost.eu'
    environment:
      GITLAB_OMNIBUS_CONFIG: |
        external_url 'https://gitlab.example.com'
        nginx['listen_port'] = 8080
        nginx['listen_https'] = false
        letsencrypt['enable'] = false
        gitlab_rails['gitlab_signin_enabled'] = false
        gitlab_rails['omniauth_enabled'] = true
        gitlab_rails['omniauth_allow_single_sign_on'] = ['azure_oauth2']
        gitlab_rails['omniauth_auto_sign_in_with_provider'] = 'azure_oauth2'
        gitlab_rails['omniauth_block_auto_created_users'] = true
        gitlab_rails['omniauth_sync_profile_from_provider'] = ['azure_oauth2']
        gitlab_rails['omniauth_sync_profile_attributes'] = ['name','email']
        gitlab_rails['omniauth_block_auto_created_users'] = false
        gitlab_rails['omniauth_providers'] = [
          {
            "name" => "azure_oauth2",
            "args" => {
      				"client_id" => "{{AAD Client ID}}",
      				"client_secret" => "{{AAD Client Secret}}",
      				"tenant_id" => "{{AAD TENTANT ID}}",
            }
          }
        ]

    volumes:
        - $GITLAB_HOME/gitlab/data:/var/opt/gitlab
        - $GITLAB_HOME/gitlab/logs:/var/log/gitlab
        - $GITLAB_HOME/gitlab/config:/etc/gitlab
```


## /etc/gitlab/gitlab.rb
> 
> Optional - config needs some tweaking to get the most out of OAuth login
{.is-info}



```bash
external_url 'https://gitlab.example.com'
nginx['listen_port'] = 5050 # Custom Port
nginx['listen_https'] = false # set this if reverse proxy
letsencrypt['enable'] = false # no need if reverse proxy handles TLS

# Azure AD Oauth config:
gitlab_rails['omniauth_enabled'] = true
gitlab_rails['omniauth_allow_single_sign_on'] = ['azure_oauth2']
gitlab_rails['omniauth_auto_link_ldap_user'] = true
gitlab_rails['sync_profile_from_provider'] = ['azure_oauth2']
gitlab_rails['sync_profile_attributes'] = ['name', 'email', 'location']
gitlab_rails['omniauth_providers'] = [
  {
    "name" => "azure_oauth2",
    "args" => {
      "client_id" => "{{AAD Client ID}}",
      "client_secret" => "{{AAD Client Secret}}",
      "tenant_id" => "{{AAD TENTANT ID}}",
    }
  }
]



```