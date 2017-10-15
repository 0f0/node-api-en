<!-- YAML
added: v0.1.99
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/11985
    description: The `msg` parameter can be an Uint8Array now.
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/10473
    description: The `address` parameter is always optional now.
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/5929
    description: On success, `callback` will now be called with an `error`
                 argument of `null` rather than `0`.
  - version: v5.7.0
    pr-url: https://github.com/nodejs/node/pull/4374
    description: The `msg` parameter can be an array now. Also, the `offset`
                 and `length` parameters are optional now.
-->

* `msg` {Buffer|Uint8Array|string|Array} Message to be sent.
* `offset` {number} Integer. Offset in the buffer where the message starts.
* `length` {number} Integer. Number of bytes in the message.
* `port` {number} Integer. Destination port.
* `address` {string} Destination hostname or IP address.
* `callback` {Function} Called when the message has been sent.

Broadcasts a datagram on the socket. The destination `port` and `address` must
be specified.

The `msg` argument contains the message to be sent.
Depending on its type, different behavior can apply. If `msg` is a `Buffer`
or `Uint8Array`,
the `offset` and `length` specify the offset within the `Buffer` where the
message begins and the number of bytes in the message, respectively.
If `msg` is a `String`, then it is automatically converted to a `Buffer`
with `'utf8'` encoding. With messages that
contain  multi-byte characters, `offset` and `length` will be calculated with
respect to [byte length][] and not the character position.
If `msg` is an array, `offset` and `length` must not be specified.

The `address` argument is a string. If the value of `address` is a host name,
DNS will be used to resolve the address of the host.  If `address` is not
provided or otherwise falsy, `'127.0.0.1'` (for `udp4` sockets) or `'::1'`
(for `udp6` sockets) will be used by default.

If the socket has not been previously bound with a call to `bind`, the socket
is assigned a random port number and is bound to the "all interfaces" address
(`'0.0.0.0'` for `udp4` sockets, `'::0'` for `udp6` sockets.)

An optional `callback` function  may be specified to as a way of reporting
DNS errors or for determining when it is safe to reuse the `buf` object.
Note that DNS lookups delay the time to send for at least one tick of the
Node.js event loop.

The only way to know for sure that the datagram has been sent is by using a
`callback`. If an error occurs and a `callback` is given, the error will be
passed as the first argument to the `callback`. If a `callback` is not given,
the error is emitted as an `'error'` event on the `socket` object.

Offset and length are optional but both *must* be set if either are used.
They are supported only when the first argument is a `Buffer` or `Uint8Array`.

Example of sending a UDP packet to a random port on `localhost`;

```js
const dgram = require('dgram');
const message = Buffer.from('Some bytes');
const client = dgram.createSocket('udp4');
client.send(message, 41234, 'localhost', (err) => {
  client.close();
});
```

Example of sending a UDP packet composed of multiple buffers to a random port
on `127.0.0.1`;

```js
const dgram = require('dgram');
const buf1 = Buffer.from('Some ');
const buf2 = Buffer.from('bytes');
const client = dgram.createSocket('udp4');
client.send([buf1, buf2], 41234, (err) => {
  client.close();
});
```

Sending multiple buffers might be faster or slower depending on the
application and operating system. It is important to run benchmarks to
determine the optimal strategy on a case-by-case basis. Generally speaking,
however, sending multiple buffers is faster.

**A Note about UDP datagram size**

The maximum size of an `IPv4/v6` datagram depends on the `MTU`
(_Maximum Transmission Unit_) and on the `Payload Length` field size.

- The `Payload Length` field is `16 bits` wide, which means that a normal
  payload exceed 64K octets _including_ the internet header and data
  (65,507 bytes = 65,535 − 8 bytes UDP header − 20 bytes IP header);
  this is generally true for loopback interfaces, but such long datagram
  messages are impractical for most hosts and networks.

- The `MTU` is the largest size a given link layer technology can support for
  datagram messages. For any link, `IPv4` mandates a minimum `MTU` of `68`
  octets, while the recommended `MTU` for IPv4 is `576` (typically recommended
  as the `MTU` for dial-up type applications), whether they arrive whole or in
  fragments.

  For `IPv6`, the minimum `MTU` is `1280` octets, however, the mandatory minimum
  fragment reassembly buffer size is `1500` octets. The value of `68` octets is
  very small, since most current link layer technologies, like Ethernet, have a
  minimum `MTU` of `1500`.

It is impossible to know in advance the MTU of each link through which
a packet might travel. Sending a datagram greater than the receiver `MTU` will
not work because the packet will get silently dropped without informing the
source that the data did not reach its intended recipient.

