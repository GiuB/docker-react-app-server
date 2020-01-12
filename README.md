Created using this guide:
https://dev.to/numtostr/running-react-and-node-js-in-one-shot-with-concurrently-2oac

Step to reproduce:

1. npm init -y
2. yarn global add create-react-app
3. create-react-app client
4. Create node index.js file as this:

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

5. yarn add -D concurrently
