# System Timezone
[![Build Status](https://travis-ci.org/jeriveromartinez/unix-system-timezone.svg?branch=master)](https://travis-ci.org/jeriveromartinez/unix-system-timezone)

A simple package that checks various system configuration files in an attempt to determine what *this* computer's timezone is (in Olson notation).  

This is a 100% javasctipt package that should work on any version of `node > 8.0.0`.

We do this via 4 methods:

1. If `process.env.TZ` is set, return it
2. If `/etc/timezone` is present, return the contents of the file
3. If `/etc/localtime` is present, and is a symlink to a file in `/usr/share/zoneinfo`, we can follow the link to know the proper timezone
4. If `/etc/localtime` is present, but not a symlink, we MD5 the contents and compare it to all other files in, `/usr/share/zoneinfo`, and then return the name of the first match.

## Examples:

```javascript
var system_timezone = require('system-timezone');

// This is a slow, sync call.  It would be best to call it once at boot and cache the response
// If a timezone cannot be determined, an Error will be thrown.
console.log( system_timezone() ); // America/Los_Angeles
```
