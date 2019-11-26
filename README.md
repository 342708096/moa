# Moa
a demo for learning Koa

### 传统 nodejs 使用方法
```js
const http = require('http')
const server = http.createServer((req, res) => {
  res.writeHead(200)
  res.end('hello nodejs')
})

server.listen(3000, () => {
  console.log('server started at port 3000')
})
```

我们希望可以像 koa 那样写代码，如下：

```js
const Moa = require('./moa')
const app = new Moa()

app.use((req, res) => {
  res.writeHeader(200)
  res.end('hello, Moa')
})

app.listen(3000, () => {
  console.log('server started at port 3000')
})
```
所以我们需要创建一个 `moa.js` 文件，该文件主要内容是创建一个类 *Moa*， 主要包含 `use()` 和 `listen()` 两个方法

```js
const http = require('http')

class Moa {
  use(callback) {
    this.callback = callback
  }
  listen(...args) {
    const server = http.createServer((req, res) => {
      this.callback(req, res)
    })

    server.listen(...args)
  }
}

module.exports = Moa
```