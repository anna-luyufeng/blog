---
title: "UI 狀態應該要程式邏輯獨立處理"
date: 2019-11-18T07:41:21Z
layout: layouts/post.njk
draft: true
---

原文連結：[No, disabling a button is not app logic. - DEV Community]( https://dev.to/davidkpiano/no-disabling-a-button-is-not-app-logic-598i)

假設一個按鈕點擊後會送出 HTTP Request：

```jsx
function DogFetcher() {
  const [isLoading, setIsLoading] = useState(false);
  const [dog, setDog] = useState(null);

  return (
    <div>
      <figure className="dog">{dog && <img src={dog} alt="doggo" />}</figure>

      <button
        onClick={() => {
          setIsLoading(true);
          fetch(`https://dog.ceo/api/breeds/image/random`)
            .then(data => data.json())
            .then(response => {
              setDog(response.message);
              setIsLoading(false);
            });
        }}
      >
        {isLoading ? "Fetching..." : "Fetch dog!"}
      </button>
    </div>
  );
```



「如果有些人沒什麼耐心，快速按了好幾下按鈕，不就會在短時間內發送超多次 Request？」

「那把 `isLoading` 綁在按鈕的 `disabled` 屬性上讓使用者不能點就好啦！」

像這樣：

```jsx
function DogFetcher() {
  // ...

  <button
    onClick={() => {
      // ... excessive amount of ad-hoc logic
    }}
    disabled={isLoading}
  >
    {isLoading ? "Fetching..." : "Fetch dog!"}
  </button>

  // ...
}
```

但作者認為「發送 Request」與「按鈕狀態」兩個其實是獨立的，**當已經送出 Request，須避免同時間再送 Request**。

```jsx
function DogFetcher() {
  const [isLoading, setIsLoading] = useState(false);
  const [dog, setDog] = useState(null);

  // 獨立 function 處理 HTTP Request
  function fetchDog() {
    if (isLoading) return; // 👈 在第一次 Request 完成前不再送

    setIsLoading(true);
    fetch(`https://dog.ceo/api/breeds/image/random`)
      .then(data => data.json())
      .then(response => {
        setDog(response.message);
        setIsLoading(false);
      });
  }

  return (
    <div>
      <figure className="dog" onDoubleClick={fetchDog}>
        {dog && <img src={dog} alt="doggo" />}
      </figure>

      <button onClick={fetchDog}>
        {isLoading ? "Fetching..." : "Fetch dog!"}
      </button>
    </div>
  );
}
```

### 若是有多種狀態（loading、success、failure、cancel⋯⋯等）該如何處理？

作者使用 `useReducer` 與 `useEffect `的 React hooks 做示範

1. 建立變數 `status` 來儲存狀態值：idle、loading、success、failure
2. 定義不同事件
   - `FETCH` 表示發生 HTTP Request
   - `RESOLVE` 表示 HTTP Request 成功，並且回傳 `data`
   - `REJECT` 表示 HTTP Request 失敗，並且回傳 `error`
   - `CANCEL` 表示取消 HTTP Request
3. 建立 useReducer 將事件綁定在 UI 上（點擊後 dispatch event）
4. useEffect 會同步狀態

```jsx
function dogReducer(state, event) {
  switch (event.type) {
    case "FETCH":
      return {
        ...state,
        status: "loading"
      };
    case "RESOLVE":
      return {
        ...state,
        status: "success",
        dog: event.data
      };
    case "REJECT":
      return {
        ...state,
        status: "failure",
        error: event.error
      };
    case "CANCEL":
      return {
        ...state,
        status: "idle"
      };
    default:
      return state;
  }
}

const initialState = {
  status: "idle",
  dog: null,
  error: null
};
```

```jsx
function DogFetcher() {
  const [state, dispatch] = useReducer(dogReducer, initialState);
  const { error, dog, status } = state;

  useEffect(() => {
    // ... fetchDog?
  }, [state.status]);

  return (
    <div>
      {error && <span style={{ color: "red" }}>{error}</span>}
      <figure className="dog" onDoubleClick={() => dispatch({ type: "FETCH" })}>
        {dog && <img src={dog} alt="doggo" />}
      </figure>

      <button onClick={() => dispatch({ type: "FETCH" })}>
        {status === "loading" ? "Fetching..." : "Fetch dog!"}
      </button>
      <button onClick={() => dispatch({ type: "CANCEL" })}>Cancel</button>
    </div>
  );
}
```

```jsx
// ...
  useEffect(() => {
    if (state.status === "loading") {
      let canceled = false;

      fetchRandomDog()
        .then(data => {
          if (canceled) return;
          dispatch({ type: "RESOLVE", data });
        })
        .catch(error => {
          if (canceled) return;
          dispatch({ type: "REJECT", error });
        });

      return () => {
        canceled = true;
      };
    }
  }, [state.status]);
// ...
```

### 這樣做的好處

- 無論 UI 如何變化，任何情況都適用
- 不論按鈕是否被 disable，連續點擊多次都不會出現非預期的行為
- 容易放進自製的 hook
- 容易被測試
- 容易重複使用在元件內
- 容易重複使用在任何框架內

---

- [到底React Hooks有何特別（二）？淺談useEffect及useReducer | Blog | Tecky Academy](https://tecky.io/en/blog/到底react-hooks有何特別-二-淺談useeffect及usereducer/)