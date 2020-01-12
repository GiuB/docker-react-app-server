Created using this guide:
https://dev.to/numtostr/running-react-and-node-js-in-one-shot-with-concurrently-2oac

Note:
In the first tutorial he use `concurrently` library to run multiple node (client & index.js as a server) and, in `client` folder, set a "proxy" if react does not respond, fallback to index node server.

Step to reproduce:

1. npm init -y
2. yarn global add create-react-app
3. create-react-app client
4. Create a Dockerfile into `client` folder

```node
FROM node:lts-slim

RUN mkdir -p /usr/src/app

WORKDIR /usr/src/app

EXPOSE 3000

CMD [ "npm", "start" ]
```

5. Create node index.js file as this:

```node
#!/usr/bin/env node

const http = require('http');

// Port Environment variable
const PORT = process.env.PORT || 5000;

// Creating the node server
const SERVER = http.createServer();

// Firing up the server on selected port
SERVER.listen(PORT);

SERVER.on('listening', () => {
  console.log('[Server]::LISTEN:%s', PORT);
});

// Callback function for checking connecting or error
SERVER.on('error', error => {
  throw new Error(`[Server]::ERROR:${error.message}`);
});
```
