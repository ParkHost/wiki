---
title: socketIO
description: 
published: true
date: 2020-06-17T09:28:09.764Z
tags: javascript, socket, websockets, featherjs, socket.io
editor: markdown
---

![socket.io__0[1].png](/socket.io__0[1].png =125x125){.align-left}
is an realtime bidirectional connection between client and server.

# Installation
```
npm install socket.io
```

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
