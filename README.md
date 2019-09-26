# or don't.
Repo created to reproduce the [issue #4087](https://github.com/strapi/strapi/issues/4087#) regarding strapi

Commands ran in bash(cf ./console.log.md for the full thing):
```
mkdir strapdemo
cd strapidemo
strapi new cms --quickstart
```
My browser opened, I filled the form and ended up in the main dashboard. Back into bash:
```
C^ // (close server)
strapi start // (still working)
npm install --save axios
strapi start // (still working)
npm audit fix // (as prompted after getting axios)
npm i // (as prompted by npm audit fix)
npm audit fix
strapi start // output below
```

Output of the last `strapi start`: 
```
internal/modules/cjs/loader.js:775
    throw err;
    ^

Error: Cannot find module 'strapi-utils'
Require stack:
- /home/me/.nvm/versions/node/v12.10.0/lib/node_modules/strapi/bin/strapi.js
    at Function.Module._resolveFilename (internal/modules/cjs/loader.js:772:15)
    at Function.Module._load (internal/modules/cjs/loader.js:677:27)
    at Module.require (internal/modules/cjs/loader.js:830:19)
    at require (internal/modules/cjs/helpers.js:68:18)
    at Object.<anonymous> (/home/me/.nvm/versions/node/v12.10.0/lib/node_modules/strapi/bin/strapi.js:13:17)
    at Module._compile (internal/modules/cjs/loader.js:936:30)
    at Object.Module._extensions..js (internal/modules/cjs/loader.js:947:10)
    at Module.load (internal/modules/cjs/loader.js:790:32)
    at Function.Module._load (internal/modules/cjs/loader.js:703:12)
    at Function.Module.runMain (internal/modules/cjs/loader.js:999:10) {
  code: 'MODULE_NOT_FOUND',
  requireStack: [
    '/home/me/.nvm/versions/node/v12.10.0/lib/node_modules/strapi/bin/strapi.js'
  ]
}

```

Turns out you shouldn't `npm audit fix` into your working strapi unless you're feeling very brave. So far I haven't succeed in fixing it; I actually avoided the problem by generating a fresh app and migrate my stuff there.