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

### 2.4.1 デストラクチャリング
- 入れ子のデストラクチャリング
  - https://ja.javascript.info/destructuring-assignment#ref-1918

### 2.5.2 async/await
- Promise を使いやすくするための糖衣構文
- ```js
  // handling Promise 1.
  fetch("https://api.randomuser.me/?nat=US&results=1").then(res =>
    console.log(res.json())
  );

  // handling Promise 2.
  const getFakePerson = async () => {
    const res = await fetch("https://api.randomuser.me/?nat=US&results=1");
    const { results } = await res.json();
    console.log(results);
  };
  getFakePerson();
  ```
  - 1.と2.は等価。
  - 2.は、await キーワードを使って fetch を呼び出しているため、それ以降のコードは
Promise が成功するまで実行されない。

  - awaitで失敗する可能性がある場合は、try/catchを利用する

<br/>

- > 非同期関数は常にプロミスを返します。非同期関数の返値が明示的にプロミスでない場合は、暗黙的にプロミスでラップされます。
  - https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Statements/async_function#%E8%A7%A3%E8%AA%AC
- イベント処理をPromiseでラップしてみる
  - https://zenn.dev/awyaki/scraps/8ee8319e0956a5
- 複数APIへのリクエストをfetch関数で同時実行するプラクティス
  - https://qiita.com/SRAUFactory/items/c4a60b362cb6de57d10d

### 2.7 - ECMAScriptモジュール
- ECMAScriptモジュールの構文
  - import/export の記法
    - https://jsprimer.net/basic/module/

### 3.1 関数型とは
- 高階関数
  - > ある関数が別の関数を引数として受け取るか、もしくは関数を戻り値として返すか、ひとつでも該当すれば高階関数を名乗れす
- 命令型, 宣言型プログラミング
  - https://zenn.dev/mo_ri_regen/articles/declared-vs-imperative
- イミュターブルなデータとは
  - > イミュータブルなデータはコピーの例と同じです。関数型プログラミングでは、データに変更を加えるとき、必ずコピーを作成してから変更します。
- 純粋関数
  - > 引数の値のみを参照して、それをもとに計算し、値を返す関数を純粋関数といいます。純粋関数は、少なくともひとつの引数を取り、値もしくは他の関数を戻り値として返します。純粋関数には副作用はありません。すなわち、グローバル関数に値を書き込んだり、アプリケーションの状態を変更したりしません。また、純粋関数は、引数をイミュータブルなデータとして扱います。
  - ```js
    const frederick = {
      name: "Frederick Douglass",
      canRead: false,
      canWrite: false
    };
    const selfEducate = person => ({
      ...person, // 引数はimmutable, person.canRead = trueとしない
      canRead: true,
      canWrite: true
    });
    ```
  - 純粋関数のメリット：https://zenn.dev/riku/books/36d9873ee1c0e6/viewer/026276
  - 関数を書く際の注意
    - > 1. 関数は少なくともひとつの引数を受け取らなければいけない
      > 2. 関数は値もしくは他の関数を戻り値として返却しなければならない
      > 3. 関数は引数や関数外で定義された変数に直接変更を加えてはならない
### 3.3.4 高階関数
- カリー化
  - https://ja.javascript.info/currying-partials#ref-290


### 5.1.2 BabelによるJSXの変換
- JSXをサポートしているブラウザはないため、コンパイルが必要。
- JSXをReactAPIにコンパイルする
  - https://babeljs.io/repl

### 5.3 webpackを使ってビルド環境を構築する
- > JSX および ES.next の変換、コンポーネント間の依存関係の管理、画像や CSS の最適化
  > HTML の\<script>タグに依存ファイルを記述する場合、それぞれのファイルは別々の HTTP リクエストによりダウンロードされるため、ファイル数が増えるとリクエスト数が増え、その分遅延が大きくなります。依存ファイルを単一のファイルにまとめることで、この遅延を削減できます。
- Hot Module Replacement
  - ソースコードの変更の監視と、リアルタイムに変更箇所を変更

### 5.3.3 Source Map
- 依存モジュールを単一ファイルにビルドすることで、元ファイルの行番号がわかららなくなるため、ブラウザで問題箇所が特定できても元ファイルのどこを修正してよいかわからなくなる
  - https://webpack.js.org/configuration/devtool/
  - デベロッパーツールの[Sources] > webpack://..フォルダにソースが格納されている

### 6.3.1 refを使ったデータアクセス
- > ref はコンポーネントの描画結果である DOM ノードへの参照を保持するオブジェクト
- ```js
  // 省略, jsx
  return (
      <form onSubmit={submit}>
        <input ref={txtTitle} type="text" placeholder="color title..." required />
        <input ref={hexColor} type="color" required />
        <button>ADD</button>
      </form>
    );
  }
  // submit logic
  const submit = e => {
    e.preventDefault();
    const title = txtTitle.current.value; // text inputのvalueを参照
    const color = hexColor.current.value; // color inputのvalueを参照
    onNewColor(title, color);
    txtTitle.current.value = ""; // immutableでない => 宣言型プログラミングパターンに反する記述
    hexColor.current.value = ""; // immutableでない <=> 制御されていないコンポーネント(uncontrolled component)
  };
  ```

  - uncontrolled componentがどうしても必要になるケース
    - > たとえば React 以外のライブラリとデータをやり取りする場合は、DOM に直接アクセスする必要があります。ただ、そのような場面以外では、なるべく次に紹介する<b>制御されたアプローチ</b>を取るようにしてください

  - (RHFがrefを使ってvalueを参照するのは妥当か疑問)

### 6.3.2 制御されたコンポーネント
- > 制御されたコンポーネント(controlled component)では、ユーザーの入力値は React により管理されるため、DOM ノードに直接アクセスする必要はなく、ref も不要です。その結果、コードは宣言的になり、入力のバリデーションのコードを追加するのも容易になります
  - ```js
    const [title, setTitle] = useState(''); // useRefの代わりにuseStateを利用する
    const [color, setColor] = useState('#000000')
    ```

### 6.3.3 カスタムフック
- chapter-06/6.3/6.3.3/src/hooks.js

### 6.4.2 コンテキストとステートの併用
- > コンテキストプロバイダーを使えばデータを公開することが可能ですが、<b>データを変更することはできません</b>。それをするには、さらに親のコンポーネントの助けが必要になります。つまり、親コンポーネントでステートを保持して、その値を Provider コンポーネントに設定します。ステートが更新されると、親コンポーネントが再描画され、結果的に Provider の配下のコンポーネントツリーが新しいデータで再描画されます。
  - ```js
      export default function ColorProvider ({ children }) { // chapter-06/6.4/6.4.3/src/ColorProvider.js
        const [colors, setColors] = useState(colorData);
        return ( // setColors関数のデータも公開
          <ColorContext.Provider value={{ colors, setColors }}>
            {children}
          </ColorContext.Provider>
        );
      }
    ```
    - setColorsを公開することで、任意の子コンポーネントがcolorを操作できるため賛否がある

### 6.4.4 コンテキストとカスタムフックの併用
- > コンテキストをコンシューマーにいっさい公開することなく、データを共有する
  - https://github.com/citronn/learning-react-2e-ja/blob/ab0546cf5cc3e390bfdef196bd110837aa402ee5/chapter-06/6.4/6.4.4/src/ColorProvider.js#L6
  - https://zenn.dev/takepepe/articles/context-custom-hooks
