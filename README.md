<!--
SPDX-FileCopyrightText: 2021 Anders Rune Jensen

SPDX-License-Identifier: CC0-1.0
-->

:warning: **This repo was moved to https://github.com/ssbc/ssb-subset-rpc.** This archival will remain in this GitHub org `ssb-ngi-pointer` to demonstrate the outcome of the work done by the SSB NGI Pointer team during 2020 and 2021. The SSB NGI Pointer team is no longer active because we completed our grant project.

# SSB Subset RPC

A secret stack plugin with an RPC to fetch message subsets.

Implements the
[spec](https://github.com/ssb-ngi-pointer/ssb-subset-replication-spec)

## Installation

**Prerequisites:**

- Requires **Node.js 10** or higher
- Requires `ssb-db2`

```
npm install --save ssb-subset-rpc
```

Add this plugin like this:

```diff
 const sbot = SecretStack({ appKey: caps.shs })
     .use(require('ssb-db2'))
+    .use(require('ssb-subset-rpc'))
     // ...
```

## API

### getSubset

examples:

```js
pull(
  sbot.getSubset({
    op: 'and',
    args: [
      { op: 'type', string: 'post' },
      { op: 'author', feed: '@6CAxOI3f+LUOVrbAl0IemqiS7ATpQvr9Mdw9LC4+Uv0=.ed25519' }
    ]
  }),
  pull.collect((err, results) => {
    console.logs("posts for arj", results)
  })
)

pull(
  sbot.getSubset({
    op: 'and',
    args: [
      { op: 'type', string: 'post' },
      { op: 'author', feed: '@6CAxOI3f+LUOVrbAl0IemqiS7ATpQvr9Mdw9LC4+Uv0=.ed25519' }
    ]
  }, {
    descending: true,
    pageSize: 10
  }),
  pull.collect((err, results) => {
    console.logs("latest 10 posts for arj", results)
  })
)
```

## License

LGPL-3.0
