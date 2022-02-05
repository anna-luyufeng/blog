---
title: "[Snapask] Dragonfruit Migration"
date: 2022-01-16T17:03:42+08:00
layout: layouts/post.njk
draft: true
---

替換路徑

```jsx
// Components
import Button from '@snapask/common-components/components/Button'; 
=> import { Button } from '@snapask/common-components'

// Icon
import { NextArrow } from '@snapask/common-components/components/Icon';


// Constants, Hooks ... Utils
@snapask/common-components/service
@snapask/common-components/constants
@snapask/common-components/utils


@snapask/common-components/dist/service
@snapask/common-components/dist/constants
@snapask/common-components/dist/utils
```

