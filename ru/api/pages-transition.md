---
title: "API: Свойство transition"
description: Nuxt.js использует компонент `<transition>`, чтобы позволить вам создавать поразительные переходы/анимации между вашими страницами. 
---

# Свойство transition

> Nuxt.js использует компонент [`<transition>`](https://ru.vuejs.org/v2/guide/transitions.html#Анимирование-одиночного-элемента-компонента), чтобы позволить вам создавать поразительные переходы/анимации между вашими страницами.

- **Тип:** `String` или `Object` или `Function`

Чтобы установить пользовательский переход для определенного пути, просто добавьте ключ `transition` к компоненту страницы.

```js
export default {
  // Может быть типом String
  transition: ''
  // или Object
  transition: {}
  // или Function
  transition (to, from) {}
}
```

## String

Если ключ `transition` задан строкой, то он будет использован как `transition.name`.

```js
export default {
  transition: 'test'
}
```

Nuxt.js будет использовать эти настройки для установки компонента следующим образом:

```html
<transition name="test">
```

## Object

Если ключ `transition` задан как объект:

```js
export default {
  transition: {
    name: 'test',
    mode: 'out-in'
  }
}
```

Nuxt.js будет использовать эти настройки для установки компонента следующим образом:

```html
<transition name="test" mode="out-in">
```

Ниже приведены возможные значения, которые может иметь обьект `transition`:


| Ключ               | Тип       | По-умолчанию | Определение                                                                                                                                                                                                                 |
|--------------------|-----------|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`             | `String`  | `"page"`     | Имя перехода, применяемое ко всем переходам путей. 
                                                                            |
| `mode`             | `String`  | `"out-in"`   | Режим перехода, применяемое ко всем путям, смотрите [документацию Vue](https://ru.vuejs.org/v2/guide/transitions.html#Режимы-переходов) 
                                                                            |
| `css`              | `Boolean` | `true`       | Надо ли применять CSS transition классы. По-умолчанию `true`. Если установить `false`, то будут срабатывать только JavaScript хуки через компонентные события. 
                                                                            |
| `duration`         | `Integer` | n/a          | Длительность (в миллисекундах) перехода. Смотрите [документацию Vue](https://ru.vuejs.org/v2/guide/transitions.html#Указание-длительности-перехода).                                                                                                                                            |
| `type`             | `String`  | n/a          | Определенный тип событий перехода, который будет ожидаться, чтобы определить время окончания перехода. Доступные значения: `"transition"` и `"animation"`. По-умолчанию, автоматически определяется тип, который имеет самую длительную продолжительность.                                                          |
| `enterClass`       | `String`  | n/a          | Начальное состояние пользовательского класса перехода. Смотрите [документацию Vue](https://ru.vuejs.org/v2/guide/transitions.html#Пользовательские-классы-переходов). 
                                                                            |
| `enterToClass`     | `String`  | n/a          | Конечное состояние пользовательского класса перехода. Смотрите [документацию Vue](https://ru.vuejs.org/v2/guide/transitions.html#Пользовательские-классы-переходов).         
                                                                            |
| `enterActiveClass` | `String`  | n/a          | Класс, который применяется по всей продолжительности перехода Смотрите [документацию Vue](https://ru.vuejs.org/v2/guide/transitions.html#Пользовательские-классы-переходов).  
                                                                            |
| `leaveClass`       | `String`  | n/a          | Начальное состояние пользовательского класса перехода. Смотрите [документацию Vue](https://ru.vuejs.org/v2/guide/transitions.html#Пользовательские-классы-переходов). 
                                                                            |
| `leaveToClass`     | `String`  | n/a          | Конечное состояние пользовательского класса перехода. Смотрите [документацию Vue](https://ru.vuejs.org/v2/guide/transitions.html#Пользовательские-классы-переходов).         
                                                                            |
| `leaveActiveClass` | `String`  | n/a          | Класс, который применяется по всей продолжительности перехода Смотрите [документацию Vue](https://ru.vuejs.org/v2/guide/transitions.html#Пользовательские-классы-переходов).  
                                                                            |

Вы также можете объявить методы в `transition` для [JavaScript хуков](https://ru.vuejs.org/v2/guide/transitions.html#JavaScript-хуки):

- `beforeEnter(el)`
- `enter(el, done)`
- `afterEnter(el)`
- `enterCancelled(el)`
- `beforeLeave(el)`
- `leave(el, done)`
- `afterLeave(el)`
- `leaveCancelled(el)`

*Примечание: Также рекомендуется добавить `css: false` для JavaScript-переходов, чтобы Vue пропускал определение CSS. Это также предотвращает случайное вмешательство CSS правил в переход.*

## Function

Если ключ `transition` задан как функция:

```js
export default {
  transition (to, from) {
    if (!from) return 'slide-left'
    return +to.query.page < +from.query.page ? 'slide-right' : 'slide-left'
  }
}
```

Переходы применяемые при навигации:

- `/` to `/posts` => `slide-left`,
- `/posts` to `/posts?page=3` => `slide-left`,
- `/posts?page=3` to `/posts?page=2` => `slide-right`.
