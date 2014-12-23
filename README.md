node-ral
===========

[![Build Status](https://travis-ci.org/fex-team/node-ral.svg?branch=master)](https://travis-ci.org/fex-team/node-ral)
[![Coverage Status](https://coveralls.io/repos/fex-team/node-ral/badge.png)](https://coveralls.io/r/fex-team/node-ral)

## Usage

### Install

```bash
npm install node-ral
```

### RAL init

```javascript
var RAL = require('node-ral').RAL;

RAL.init({
    //path to config files
    confDir : __dirname + path.sep + './config',
    logger : {
        "log_path" : __dirname + path.sep + '../logs'
    },
    //specify the server's idc, ral will priority use backend with same idc
    currentIDC : 'tc'
});
```

### config file

Every file in confDir will be loaded as config

```javascript
// config/config.js
module.exports = {
    'SOME_SERVICE': {
        unpack: 'json',
        pack: 'form',
        method: 'POST',
        encoding: 'gbk',
        balance: 'random',
        protocol: 'http',
        retry: 2,
        timeout: 500,
        server: [
            { host: '127.0.0.1', port: 8080}
        ]
    }
};
```

Also support json config file

```json
{
    "SOME_SERVICE": {
        "unpack": "json",
        "pack": "form",
        "method": "POST",
        "encoding": "gbk",
        "balance": "random",
        "protocol": "http",
        "server": [
            { "host": "127.0.0.1", "port": 8080}
        ]
    }
}
```

### Start a request

```javascript
var RAL = require('node-ral').RAL;

var request = RAL('SOME_SERVICE', {
    path: '/user/info'
    data: {
        'name': 'hefangshi',
        'city': 'Beijing',
        'gender': 'Male'
    }
});

request.on('data', function(data){
    data.status.should.be.eql(0);
});
```

more usage can be found in /test/ral.js

## Support

- Balance
    - [X] RandomBalance
    - [X] RoundRobinBalance
- Converter
    - [X] JSON
    - [X] String
    - [X] Form
    - [X] QueryString
    - [X] Raw
    - [X] FormData
    - [X] Stream
- Protocol
    - [X] HTTP
