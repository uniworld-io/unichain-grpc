
<<<<<<< HEAD
# Unichain gRPC <Deprecated>
=======
# Unichain gRPC
>>>>>>> bd823f9... add source code

A lightweight JavaScript library for Unichain

This code is based on [giekaton](https://github.com/giekaton/libra-grpc) and [Libra](https://libra.org) project

#### Node.js
To install Unichain gRPC on Node.js, open your terminal and run:
```
npm install unichain-grpc --save
```

### Usage
```js
var unichain = require('unichain-grpc');

// Init gRPC client
var client = new unichain.Client('testnet-1.unichain.world:8000');

// Get account state
var params = {
  address: Buffer.from('435fc8fc85510cf38a5b0cd6595cbb8fbb10aa7bb3fe9ad9820913ba867f79d4', 'hex')
};
client.request('get_account_state', params, function(err, result) {
  console.log(err, result);
});

// If a callback is not provided, a Promise is returned
client.request('get_account_state', params).then(function(result) {
  console.log(result);
});
```
[See more examples](/test/test.js)

### API

#### Get account state
Get the latest state for an account.

```js
var params = {
  address: Buffer.from('435fc8fc85510cf38a5b0cd6595cbb8fbb10aa7bb3fe9ad9820913ba867f79d4', 'hex')
};
client.request('get_account_state', params, function(err, result) {
  console.log(err, result);
});
```

#### Get account transaction
Get the committed transaction by account and sequence number.

```js
var params = {
  account: Buffer.from('435fc8fc85510cf38a5b0cd6595cbb8fbb10aa7bb3fe9ad9820913ba867f79d4', 'hex'),
  sequence_number: 1,
  fetch_events: true
};
client.request('get_account_transaction_by_sequence_number', params, function(err, result) {
  console.log(err, result);
});
```

#### Get events
Get event by account and path.

```js
var params = {
  access_path: {
    address: Buffer.from('435fc8fc85510cf38a5b0cd6595cbb8fbb10aa7bb3fe9ad9820913ba867f79d4', 'hex')
  },
  start_event_seq_num: 2,
  ascending: true,
  limit: 10
};
client.request('get_events_by_event_access_path', params, function(err, result) {
  console.log(err, result);
});
```

#### Get transactions
Get the committed transaction by range

```js
var params = {
  start_version: 1,
  limit: 10,
  fetch_events: true
};
client.request('get_transactions', params, function(err, result) {
  console.log(err, result);
});
```

### Utils

#### Deserialize raw txn bytes
Deserialize the raw bytes into a raw transaction object

```js
var rawTxnBytes = 'CiAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACiQTjj/zqDoBRr0AQq/AUxJQlJBVk0KAQAHAUoAAAAGAAAAA1AAAAAGAAAADFYAAAAFAAAADVsAAAAEAAAABV8AAAAzAAAABJIAAAAgAAAAB7IAAAANAAAAAAAAAQACAAMAAQQAAgACBAIDAgQCBjxTRUxGPgxMaWJyYUFjY291bnQJTGlicmFDb2luBG1haW4PbWludF90b19hZGRyZXNzAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAQIABAAMAAwBEQECEiQIARIgGw7O7WUWHZkVsSi1zRwRzkktcCs7ls26I/IZpt1t7qYSChIIAOH1BQAAAAA=';
var rawTx = unichain.utils.deserializeRawTxnBytes(rawTxnBytes);
console.log('Raw transaction', rawTx);
```


## License

[MIT](LICENSE).
