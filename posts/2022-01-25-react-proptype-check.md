---
title: ""
date: 2022-01-25T17:06:29+08:00
layout: layouts/post.njk
draft: true
---

```
import PropTypes from 'prop-types'

```

See: [Typechecking with PropTypes](https://reactjs.org/docs/typechecking-with-proptypes.html)

| `any` | Anything |
| ----- | -------- |
|       |          |

#### Basic

| `string` |               |
| -------- | ------------- |
| `number` |               |
| `func`   | Function      |
| `bool`   | True or false |

#### Enum

| `oneOf`*(any)*            | Enum types |
| ------------------------- | ---------- |
| `oneOfType`*(type array)* | Union      |

#### Array

| `array`        |      |
| -------------- | ---- |
| `arrayOf`*(…)* |      |

#### Object

| `object`          |                                      |
| ----------------- | ------------------------------------ |
| `objectOf`*(…)*   | Object with values of a certain type |
| `instanceOf`*(…)* | Instance of a class                  |
| `shape`*(…)*      |                                      |

#### Elements

| `element` | React element |
| --------- | ------------- |
| `node`    | DOM node      |

#### Required

| `(···).isRequired` | Required |
| ------------------ | -------- |
|                    |          |