---
title: Rocket.Chat
description: Chat  Application
published: true
date: 2020-09-09T14:46:09.718Z
tags: 
editor: markdown
dateCreated: 2020-09-09T14:31:58.050Z
---

![rocktchat.png](/rocktchat.png =125x125){.align-left}

**Control your:**
communication,
manage your data,
Lead with the open-source power.


---

# Overview

Communicate and collaborate with your team, share files, chat in real-time, or switch to video/audio conferencing.
Watch the video to see how Rocket.Chat provides the ideal platform for your team or business needs.

> [Rocket.Chat Repo on Github](https://github.com/RocketChat/Rocket.Chat)
{.is-success}


# Azure OAuth Settings:

- URL: https://login.microsoftonline.com/common
- Token Path: /oauth2/token
- Token Sent Via: Header
- Identity Path: /openid/userinfo
- Authoize Path: /oauth2/authoize
- Scope: openid
- Param Name for acess token: access_token
- Id: {{ Azure Client ID }}
- Secrect: {{ Azure Secret }}
- Login Style: Popup

---

## Todo:

- [ ] Set dynamically the Account fields (Username, Email, Name, (Avatar?))

# Docker

## Docker-Compose details:

```yaml
version: '2'

services:
  rocketchat:
    image: rocketchat/rocket.chat:latest
    command: >
      bash -c
        "for i in `seq 1 30`; do
          node main.js &&
          s=$$? && break || s=$$?;
          echo \"Tried $$i times. Waiting 5 secs...\";
          sleep 5;
        done; (exit $$s)"
    restart: unless-stopped
    volumes:
      - ./uploads:/app/uploads
    environment:
      - PORT=3000
      - ROOT_URL=  {{ DOMAIN_URL  }}
      - MONGO_URL=mongodb://mongo:27017/rocketchat
      - MONGO_OPLOG_URL=mongodb://mongo:27017/local
      - MAIL_URL=smtp://smtp.office365.com
      - HOSTNAME=rocketchat
    depends_on:
      - mongo
    labels:
      - "traefik.backend=rocketchat"
      - "traefik.frontend.rule=Host: {{ DOMAIN_URL }}"
    networks:
      default:
        ipv4_address: {{ IP_ADDRESS }}


  mongo:
    image: mongo:4.0
    restart: unless-stopped
    volumes:
     - ./data/db:/data/db
     #- ./data/dump:/dump
    command: mongod --smallfiles --oplogSize 128 --replSet rs0 --storageEngine=mmapv1
    labels:
      - "traefik.enable=false"

  # this container's job is just run the command to initialize the replica set.
  # it will run the command and remove himself (it will not stay running)
  mongo-init-replica:
    image: mongo:4.0
    command: >
      bash -c
        "for i in `seq 1 30`; do
          mongo mongo/rocketchat --eval \"
            rs.initiate({
              _id: 'rs0',
              members: [ { _id: 0, host: 'localhost:27017' } ]})\" &&
          s=$$? && break || s=$$?;
          echo \"Tried $$i times. Waiting 5 secs...\";
          sleep 5;
        done; (exit $$s)"
    depends_on:
      - mongo

networks:
  default:
    external:
      name: rocketchat_default

```

## Todo:

- [ ] Upgrade to Version >3
- [ ] Create custom Network
