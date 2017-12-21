node-client
===========

Node.js SDK for the BlockCypher Web services. See [http://dev.blockcypher.com](http://dev.blockcypher.com/) for detailed documentation.

This version uses promises instead of callbacks

To install, just use npm:

```bash
npm install blockcypher-promise
```

Examples
--------

```javascript
bcypher = require('blockcypher-promise');

const bcapi = new bcypher('btc','main','YOURTOKEN');

(async () => {
  //get chain info
  const chain = await bcapi.getChain();

  //get block height without any optional URL params
  const block = await bcapi.getBlock(300000);

  //get block height with an optional "txstart" param, as outlined in docs here: http://dev.blockcypher.com/
  const block2 = await bcapi.getBlock(300000, {txstart:2});

  //let's try a post request, like making a new webhook
  const webhook = {
    event: "unconfirmed-tx",
    address: "15qx9ug952GWGTNn7Uiv6vode4RcGrRemh",
    url: "https://my.domain.com/callbacks/new-tx"
  };
  const createdWebHook = await bcapi.createHook(webhook);

  //Now let's list all of our webhooks
  const hooksLis = await bcapi.listHooks(printResponse);
});
```
