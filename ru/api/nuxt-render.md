---
title: "API: nuxt.render(req, res)"
description: Вы можете использовать Nuxt.js как middleware для вашего Node.js сервера.
---

# nuxt.render(req, res)

- Тип: `Function`
- Аргументы:
  1. [Request](https://nodejs.org/api/http.html#http_class_http_incomingmessage)
  2. [Response](https://nodejs.org/api/http.html#http_class_http_serverresponse)
- Возвращает: `Promise`

> Вы можете с помощью `nuxt.render` использовать Nuxt.js как middleware для вашего Node.js сервера.

Пример с [Express](https://github.com/expressjs/express):

```js
const { Nuxt, Builder } = require('nuxt')

const app = require('express')()
const isProd = (process.env.NODE_ENV === 'production')
const port = process.env.PORT || 3000

// Мы создаем экземпляр nuxt.js с параметрами
const config = require('./nuxt.config.js')
config.dev = !isProd
const nuxt = new Nuxt(config)

// Рендерим каждый маршрут с Nuxt.js
app.use(nuxt.render)

// Создаём сборку только в dev режиме с hot-reloading
if (config.dev) {
  new Builder(nuxt).build()
  .then(listen)
  .catch((error) => {
    console.error(error)
    process.exit(1)
  })
}
else {
  listen()
}

function listen() {
  // Слушаем сервер
  app.listen(port, '0.0.0.0')
  console.log('Server listening on `localhost:' + port + '`.')
}
```

<p class="Alert">Рекомендовано вызывать `nuxt.render` после всех других middleware, поскольку функция будет обрабатывать рендеринг вашего веб приложения и не вызовет `next()`</p>