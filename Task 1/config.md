# Provide some example of config file separation for dev and prod environments

## A perfect and flawless configuration setup should ensure:

- keys can be read from file AND from environment variable
- secrets are kept outside committed code
- config is hierarchical for easier findability

### Consider the following config file:

```js
var config = {
  production: {
    mongo : {
      billing: '****'
    }
  },
  default: {
    mongo : {
      billing: '****'
    }
  }
}

exports.get = function get(env) {
  return config[env] || config.default;
}
```


### And it's usage:

```js
const config = require('./config/config.js').get(process.env.NODE_ENV);
const dbconn = mongoose.createConnection(config.mongo.billing);
```
