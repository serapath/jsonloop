# jsonloop
JSON.{parse, stringify} compatible for circular JSON

https://www.npmjs.com/package/jsonloop

https://serapath.github.io/jsonloop/

# use
`npm install jsonloop`
```js
const jsonloop = require('jsonloop')
const defaultSeperator = '.'
const cJSON = jsonloop(defaultSeperator)

var obj2 = { foo: { bar: [{ x: 'y'}, { y: 'x' }], xx: { yy: 'zz' } }, a: 'b' }
obj2.foo.bar.push(obj2.foo.xx)

const json = cJSON.stringify(obj2, 0, 2)
console.log(json) /* {
  "foo": {
    "bar": [
      {
        "x": "y"
      },
      {
        "y": "x"
      },
      {
        "yy": "zz"
      }
    ],
    "xx": "#.foo.bar.2"
  },
  "a": "b"
} */
const obj2 = cJSON.parse(json)
console.log(obj2) /*{
  "foo": {
    "bar": [
      {
        "x": "y"
      },
      {
        "y": "x"
      },
      {
        "yy": "zz"
      }
    ],
    "xx": { yy: "zz" }
  },
  "a": "b"
} */
```