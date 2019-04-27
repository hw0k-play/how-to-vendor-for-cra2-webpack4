# CRA v2 + Webpack 4 환경에서 Vendor 설정하기

### Vendor? 먹는 건가요?

Vendor는 한 프로젝트 안에서 전역으로 사용하는 `3rd-party library`들을 빌드 시 분기해놓은 파일입니다. 코드 스플리팅을 진행하기 위해 꼭 설정해야 하는 파일입니다.



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
