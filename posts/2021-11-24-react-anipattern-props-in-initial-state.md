---
title: "[React] 別將 props 設為 state 的初始值"
date: 2021-11-24T06:56:51Z
layout: layouts/post.njk
draft: true
---

use props to set the initial state => when props have changed, the state won't change.

```jsx
// 💩
export default function useForm({ initialValues }) {
  const [formData, setFormData] = useState(initialValues); // 👈 當 props 變動時，state 並不會跟著變
}

// 👍
export default function useForm({ initialValues }) {
  const [formData, setFormData] = useState({});

  useEffect(() => {
    setFormData(initialValues); // 👈 當 props 變動時再更新 state
  }, [initialValues]);
}
```

https://vhudyma-blog.eu/react-antipatterns-props-in-initial-state/