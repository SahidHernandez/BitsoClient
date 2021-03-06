# BitsoClient

Easy to use client integration with bitso.com

```
const bitso = new BitsoClient({
  key:      "KEY",
  secret:   "SECRET"
})

@param {Object} options
@param {string} options.key
@param {string} response.secret
```

```
bitso["path"](options, [, cb]);

@param {Object} options
@param {Object} options.params

@callback options.success
@param {data} response.body

@callback options.error
@param {data} response.body

@callback cb
@param {err}  response
@param {data} response
```

How to use:

```
const BitsoClient = require('bitso-client');

const bitso = new BitsoClient({
  key:      "KEY",
  secret:   "SECRET"
})

bitso.ticker({
  params: {
    book: 'btc_mxn'
  },
  success:  data=>console.log('data', data),
  error:    data=>console.log('error', data)
})

bitso.balance({
  success:  data=>console.log('data', data),
  error:    data=>console.log('error', data)
})

```

Parameters are normalized as literal object:

```
//POST https://api.bitso.com/v3/orders/
bitso.orders({
  params: {
    book: 'btc_mxn',
    side: 'buy',
    type: 'market'
  },
  method: "POST",
  success: (data)=>console.log('data', data),
  error: (data)=>{
    console.log('error', data)
  }
})
```

Same for action paths:

```
//GET https://api.bitso.com/v3/transfer/<transfer_id>

bitso["orders/:transfer_id:"]({
  params: {
    transfer_id: 'some-transfer-id'
  },
  success:  data=>console.log('data', data),
  error:    data=>console.log('error', data)
})
```

It allows to define the METHOD:

```
//DELETE https://api.bitso.com/v3/orders/<oid>/

bitso["orders/:oid:"]({
  params: {
    oid: 'some-o-id'
  },
  method:   "DELETE"
  success:  data=>console.log('data', data),
  error:    data=>console.log('error', data)
})
```

Paths definition are available on `rest_spec.json` feel free to contribute if some other is missing
