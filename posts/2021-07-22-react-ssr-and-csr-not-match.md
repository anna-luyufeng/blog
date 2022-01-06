---
title: "[React] 解決 Server Side Render 與 Client Side Render Hydrate 結果不一致警告訊息"
date: 2022-01-05T11:17:15+08:00
layout: layouts/post.njk
---

## 什麼是 Hydrate？

ReactDOM 提供 2 種將 React Component 注入 DOM 的方法

```jsx
// 純 CSR
ReactDOM.render(element, container[, callback])

// SSR
ReactDOM.hydrate(element, container[, callback]);
```

- `render` 任何存在於 container 的 DOM element 都會被替換。
- `hydrate` 會檢查 SSR pre-render 的 DOM（ [`ReactDOMServer.renderToString(element)`](https://reactjs.org/docs/react-dom-server.html)）與 CSR DOM 結構是否相符（預期應為一樣，因此才會跳警告訊息），並將相對應的事件加上，使之成為 CSR Component，因此可以重複利用 DOM element，相較 `render` 更有效率。

## 如何避免當 SSR 與 CSR DOM 結構不相同時的警告訊息？

在 React 官網 [ReactDOM - hydrate()](https://reactjs.org/docs/react-dom.html#hydrate) 裡面有一段就有提到解法：

> If you intentionally need to render something different on the server and the client, you can do a two-pass rendering. Components that render something different on the client can read a state variable like `this.state.isClient`, which you can set to `true` in `componentDidMount()`. This way the initial render pass will render the same content as the server, avoiding mismatches, but an additional pass will **happen synchronously right after hydration**. **Note that this approach will make your components slower because they have to render twice**, so use it with caution.

以下為 Functional Component 結合 React Custom Hook 範例：

```jsx

const useBrowserMounted = () => {
  const [browserMounted, setBrowserMounted] = useState(false);

  useEffect(() => {
    setBrowserMounted(true);
  }, []);

  return browserMounted;
};
```

```jsx
export default function App() {
  const browserMounted = useBrowserMounted();
  
  return (
    <ReduxProvider store={context.store}>
      <ApplicationContext.Provider
        value={{
          context: {
            browserMounted,
          },
        }}
      >
        <MyComponent />
      </ApplicationContext.Provider>
    </ReduxProvider>
  );
}

```

```jsx
export default function MyComponent() {
	const { browserMounted } = useContext(ApplicationContext).context;
  
	if (!browserMounted) {
    return null;
  }
  
  return <div>My Component</div>
}
```

