---
title: "[Web] 間隔符號 `・` 會因字型而有所不同"
date: 2022-01-05T16:03:21+08:00
layout: layouts/post.njk
---

```jsx
<div>{`${authorName}・${publishDate}`}</div>
```



Noto Sans TC

![101432856-9c6ed280-3944-11eb-898d-44ace9beb725](/img/101432856-9c6ed280-3944-11eb-898d-44ace9beb725.png)

AvertaStd

![101432868-a09af000-3944-11eb-8a21-94f9d964848d](/img/101432868-a09af000-3944-11eb-8a21-94f9d964848d.png)



## 用 CSS 繪製

```jsx
<div>
  {authorName}
  <span className={styles.dot}/>
  {publishDate}
</div>
```

```css
.dot {
  display: inline-block;
  width: 2px;
  height: 2px;
  background-color: $text100;
  margin: 0 0.5rem;
}
```

## 用 SVG 繪製並做成獨立元件

```jsx
import { number, string } from 'prop-types';
import cx from 'classnames';

import useStyles from 'hooks/useStyles';

import styles from './TextDot.scss';

/**
 * Mock character "・" to prevent it shows differently in different font families.
 */
export default function TextDot({ sizePx, className }) {
  useStyles(styles);
  return (
    <span
      style={{ paddingLeft: `${sizePx}px` }}
      className={cx(styles.root, className)}
    >
      <svg width={sizePx} className={styles.circle} viewBox="0 0 50 50">
        {/* r is slightly smaller than viewBox for better circle appearance */}
        <circle r="23" cx="25" cy="25" />
      </svg>
    </span>
  );
}

TextDot.propTypes = {
  sizePx: number,
  className: string,
};

TextDot.defaultProps = {
  sizePx: 2,
  className: '',
};
```

```scss
.root {
  position: relative;
  margin: 0 0.57em;
}

.circle {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  height: auto;
  vertical-align: middle;

  & circle {
    fill: currentColor;
  }
}
```

```jsx
<div>
  {authorName}
  <TextDot sizePx={4} />
  {publishDate}
</div>
```

