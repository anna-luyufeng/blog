---
title: ""
date: 2022-01-26T23:34:21+08:00
layout: layouts/post.njk
draft: true
---



### Enforce stateless React Components to be written as a pure function [react/prefer-stateless-function](react/prefer-stateless-function)

stateless?

react/no-did-mount-set-state

react/no-did-update-set-state

react/jsx-no-bind

react/sort-comp

Prevent usage of unsafe target='_blank' (react/jsx-no-target-blank)

自動加 rel='noreferrer'



```
=============

       summary               unimported v1.19.1 (node)
─────────────────────────────────────────────────────────────────────────────────
       entry file          : app/index.js

       unresolved imports  : 0
       unused dependencies : 25
       unimported files    : 53


─────┬───────────────────────────────────────────────────────────────────────────
     │ 25 unused dependencies
─────┼───────────────────────────────────────────────────────────────────────────
   1 │ app-root-dir
   2 │ babel-plugin-lodash
   3 │ babel-runtime
   4 │ better-npm-run
   5 │ compression
   6 │ concurrently
   7 │ cookie-parser
   8 │ cors
   9 │ debug
  10 │ es6-promise
  11 │ fingerprintjs2
  12 │ formidable
  13 │ git-rev-sync
  14 │ i18next-express-middleware
  15 │ i18next-node-fs-backend
  16 │ multer
  17 │ normalize.css
  18 │ react-plx
  19 │ react-slick
  20 │ react-visibility-sensor
  21 │ redux-actions
  22 │ styled-components
  23 │ uglifyjs-webpack-plugin
  24 │ unzip
  25 │ webpack-isomorphic-tools
─────┴───────────────────────────────────────────────────────────────────────────


─────┬───────────────────────────────────────────────────────────────────────────
     │ 53 unimported files
─────┼───────────────────────────────────────────────────────────────────────────
   1 │ app/components/Accordion/Accordion.stories.js
   2 │ app/components/fields/LineSelect/LineSelect.stories.js
   3 │ app/components/fields/OutlineSelect/OutlineSelect.stories.js
   4 │ app/constants/academyArticleTypes.js
   5 │ app/constants/accountKit.js
   6 │ app/constants/appsflyerStatus.js
   7 │ app/constants/deliveryType.js
   8 │ app/constants/languages.js
   9 │ app/constants/navItemType.js
  10 │ app/constants/newebConvenienceStoreTypes.js
  11 │ app/constants/quotaType.js
  12 │ app/constants/uploadDocumentsFields.js
  13 │ app/constants/userEventTrack.js
  14 │ app/containers/Mission/components/ScheduleSlideShow/constants/studentSchedule.js
  15 │ app/containers/TutorSignup/components/TutorInfo/components/BasicInformation/components/PhoneBlock/context/index.js
  16 │ app/containers/TutorSignup/components/TutorInfo/components/BasicInformation/components/RadioGroup/components/Radio/Radio.jsx
  17 │ app/containers/TutorSignup/components/TutorInfo/components/BasicInformation/components/RadioGroup/RadioGroup.jsx
  18 │ app/mocks/cookies.js
  19 │ app/mocks/fileMock.js
  20 │ app/mocks/objCamelcaseParser.js
  21 │ app/mocks/snapaskComponents.js
  22 │ app/services/branch.js
  23 │ app/utils/productImpression.js
  24 │ app/utils/urlParameter.js
  25 │ bin/server.js
  26 │ bin/serverhooks.js
  27 │ bin/webpack-dev-server.js
  28 │ coverage/lcov-report/prettify.js
  29 │ coverage/lcov-report/sorter.js
  30 │ ecosystem.config.js
  31 │ postcss.config.js
  32 │ server/apis/zendesk.js
  33 │ server/config/index.js
  34 │ server/express/index.js
  35 │ server/server.js
  36 │ server/services/auth.js
  37 │ server/services/getGeoIpInfo.js
  38 │ server/services/getUserLocale.js
  39 │ server/services/message.js
  40 │ server/utils/aasaUtils/index.js
  41 │ server/utils/cacheUtils/index.js
  42 │ server/utils/checkXSS.js
  43 │ server/utils/cleanbuild.js
  44 │ server/utils/i18nUtils/index.js
  45 │ server/utils/i18nUtils/localeMapping.js
  46 │ server/utils/loadNamespaces.js
  47 │ server/utils/render.js
  48 │ server/utils/sitemapUtils/index.js
  49 │ server/utils/sitemapUtils/sitemapRoutes.js
  50 │ wallaby.js
  51 │ webpack-isomorphic-tools.js
  52 │ webpack.config.js
  53 │ webpack/webpack-dev-server.js
─────┴───────────────────────────────────────────────────────────────────────────
```

```

       summary               unimported v1.19.1 (node)
───────────────────────────────────────────────────────────────────────
       entry file          : app/index.js

       unresolved imports  : 0
       unused dependencies : 25
       unimported files    : 36


─────┬─────────────────────────────────────────────────────────────────
     │ 25 unused dependencies
─────┼─────────────────────────────────────────────────────────────────
   1 │ app-root-dir
   2 │ babel-plugin-lodash
   3 │ babel-runtime
   4 │ better-npm-run
   5 │ compression
   6 │ concurrently
   7 │ cookie-parser
   8 │ cors
   9 │ debug
  10 │ es6-promise
  11 │ fingerprintjs2
  12 │ formidable
  13 │ git-rev-sync
  14 │ i18next-express-middleware
  15 │ i18next-node-fs-backend
  16 │ multer
  17 │ normalize.css
  18 │ react-plx
  19 │ react-slick
  20 │ react-visibility-sensor
  21 │ redux-actions
  22 │ styled-components
  23 │ uglifyjs-webpack-plugin
  24 │ unzip
  25 │ webpack-isomorphic-tools
─────┴─────────────────────────────────────────────────────────────────


─────┬─────────────────────────────────────────────────────────────────
     │ 36 unimported files
─────┼─────────────────────────────────────────────────────────────────
   1 │ app/components/Accordion/Accordion.stories.js
   2 │ app/components/fields/LineSelect/LineSelect.stories.js
   3 │ app/components/fields/OutlineSelect/OutlineSelect.stories.js
   4 │ app/mocks/cookies.js
   5 │ app/mocks/fileMock.js
   6 │ app/mocks/objCamelcaseParser.js
   7 │ app/mocks/snapaskComponents.js
   8 │ bin/server.js
   9 │ bin/serverhooks.js
  10 │ bin/webpack-dev-server.js
  11 │ coverage/lcov-report/prettify.js
  12 │ coverage/lcov-report/sorter.js
  13 │ ecosystem.config.js
  14 │ postcss.config.js
  15 │ server/apis/zendesk.js
  16 │ server/config/index.js
  17 │ server/express/index.js
  18 │ server/server.js
  19 │ server/services/auth.js
  20 │ server/services/getGeoIpInfo.js
  21 │ server/services/getUserLocale.js
  22 │ server/services/message.js
  23 │ server/utils/aasaUtils/index.js
  24 │ server/utils/cacheUtils/index.js
  25 │ server/utils/checkXSS.js
  26 │ server/utils/cleanbuild.js
  27 │ server/utils/i18nUtils/index.js
  28 │ server/utils/i18nUtils/localeMapping.js
  29 │ server/utils/loadNamespaces.js
  30 │ server/utils/render.js
  31 │ server/utils/sitemapUtils/index.js
  32 │ server/utils/sitemapUtils/sitemapRoutes.js
  33 │ wallaby.js
  34 │ webpack-isomorphic-tools.js
  35 │ webpack.config.js
  36 │ webpack/webpack-dev-server.js
─────┴─────────────────────────────────────────────────────────────────

```



