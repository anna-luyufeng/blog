---
title: "[NPM] Unmet and incorrect peer dependency"
date: 2022-01-20T16:37:46+08:00
layout: layouts/post.njk
draft: true
---

Peer Dependency?

**Dependency**: A library/package you project needs to run.
**Peer dependency**: Used to indicate a library/package your project will hook in to.

```bash
" > eslint-plugin-react@6.10.3" has incorrect peer dependency "eslint@^2.0.0 || ^3.0.0"
# eslint^5.0.0, eslint-plugin-react^6.10.3

yarn upgrade eslint-plugin-react@latest --dev

"html-react-parser > react-dom-core@0.0.3" has unmet peer dependency "fbjs@*".
yarn upgrade html-react-parser@latest
```

```bash
" > react-router-config@1.0.0-beta.4" has unmet peer dependency "react-router@^4.2.0".
```

