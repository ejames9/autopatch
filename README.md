# autopatch

### A node program for automatically re-publishing and semver incrementing npm packages/modules.
## Installation
### npm:
```
$ npm i autopatch --save-dev
```
## Usage:
I developed this package alongside another package, [**keyListener**](https://www.npmjs.com/package/@ejames9/keylistener), and it works very well with it. It will of course work without it, but i'd recommend checking it out for cueing the package updates when you want them. The example below will be using the `keyListener` package.
```js
const patcher = require('autopatch')
```
Then you may use it like such:

```js
const packageRootPath = 'path/to/your/amazing/npmModule'

// This function is from the `keylistener` package...
gulp.keys((ch, key)=> {
// if you pressed `ctrl-p`
  if (key.ctrl && key.name === 'p') {
// Run the patcher...
    patcher(packageRootPath)
  }
})
```
The only argument the patcher needs is either a relative or absolute path to your npm module.

**-NOTE** If the working directory of the package you are trying to update is not clean (There are unstaged and committed changes), the patcher will attempt to autoclean the directory, re-patch then republish. If there is still an error after the autoclean, the patcher will fail.

You may add a `patchLimit` property to the package you are updating to automatically trigger a `minor` update bump when the patch limit has been
exceeded. For example, if we ran the patcher for the 200th time on the below package, the version would update from "0.1.199" to "0.2.0".
```json
{
  "name": "@ejames9/keylistener",
  "version": "0.1.7",
  "description": "a node program which can be used for listening for/reacting to keystrokes..",
  "main": "index.js",
  "patchLimit": 199
}
```

This package grew out of a very specific need for me. Hopefully you may find it useful too. Happy Coding!!
