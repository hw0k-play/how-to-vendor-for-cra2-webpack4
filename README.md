# CRA v2 + Webpack 4 환경에서 공용 Vendor 생성하기

### 왜 만들었어요?

제가 리액트를 사용할 때 레퍼런스하려고 만들었습니다. 마음껏 참고하셔도 좋습니다!



### 어떻게 해요?

`config/webpack.config.js`에서 표시된 두 부분을 변경해주세요.

##### Before
```js
entry: [
  require.resolve('react-dev-utils/webpackHotDevClient'),
  paths.appIndexJs
]
```
```js
splitChunks: {
  chunks: 'all',
  name: true
}
```
##### After
```js
entry: { // 변경
  app: [
    require.resolve('react-dev-utils/webpackHotDevClient'),
    paths.appIndexJs
  ],
  vendor: [
    'react',
    'react-dom',
    // 기타 추가할 공용 라이브러리
  ]
}
```
```js
splitChunks: {
  chunks: 'all',
  name: 'vendor' // 변경
}
```
