## Reactのリソース

オフィシャルなサイトへのリンクを以下にまとめます

- [Reactのドキュメント](https://facebook.github.io/react/index.html)
- [Reactのソースコード](https://github.com/facebook/react)
- [Reactのブログ](https://facebook.github.io/react/blog/)
- [ReactのNodeパッケージ](https://www.npmjs.com/package/react)
- [webpackのドキュメント](https://webpack.js.org/)
- [Jestのドキュメント](https://facebook.github.io/jest/)
- [React Routerのドキュメント](https://reacttraining.com/react-router/)


### 2.2.4.2 アロー関数とスコープ
- レキシカルスコープ
  - https://developer.mozilla.org/ja/docs/Web/JavaScript/Closures#lexical_scoping  
- クロージャ
  - > 組み合わされた（囲まれた）関数と、その周囲の状態（レキシカル環境）への参照の組み合わせ
  - ```js
      const counter = () => {
         let count = 0;

         const increment = () => {
            return (count += 1);
         };

         return increment;
      };
      ```
<br/>

- [JavaScript: 通常の関数とアロー関数の違いは「書き方だけ」ではない。異なる性質が10個ほどある。](https://qiita.com/suin/items/a44825d253d023e31e4d)