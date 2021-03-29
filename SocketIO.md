---
title: socketIO
description: 
published: true
date: 2020-11-22T16:02:32.878Z
tags: javascript, socket, websockets, featherjs, socket.io
editor: markdown
dateCreated: 2020-06-07T15:25:39.199Z
---

![socket.io__0[1].png](/socket.io__0[1].png =81x81){.align-left}
is an realtime bidirectional connection between client and server.

---
# Usage

`NPM` Installation:
```
npm install socket.io
```
---
**Server config:**
```js
const app = require('express')();
const http = require('http').createServer(app);
const io = require('socket.io')(http);

app.get('/', (req, res) => {
  res.sendFile(__dirname + '/index.html');
});

io.on('connection', (socket) => {
  console.log('a user connected');
});

http.listen(3000, () => {
  console.log('listening on *:3000');
});
```

**Client config:**
```js
client config
```
