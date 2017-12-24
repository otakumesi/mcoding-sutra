# HTML5 CSS3 モダンコーディングメモ

## モダンな書き方
- CSSを書く時に具体的な要素名を指定しない
  - つまり、すべての要素にclassをつけてclass名でスタイルをあてる
- CSSにはid要素を使わない
  - HTMLやJavaScriptからの要素の特定に使う
    - IDはIDENTITYとして使われるべき
    - 影響範囲を狭める
- リセットCSS
  - ブラウザ間のCSSの差異をなくす
    - UAStyleSheetと呼ばれるブラウザが初期で持ってるCSSをリセットしてくれる
    - ex. 
      - https://meyerweb.com/eric/tools/css/reset/
      - https://github.com/necolas/normalize.css/


## HTML5に追加された基本的な要素
- header
- main
- footer
- nav
- section
  - セクションごとに区切られる領域に描く

## creafix
- floatを解除するためのハック
  - http://kojika17.com/2013/06/clearfix-2013.html
  - floatとは要素を浮動化させて、指定の方向に回り込ませる属性


## 最初に定義しておくべきスタイル
- フォントの種類
- ベースのフォントサイズ
- テキストの文字色
- リンクの文字色


## フォントサイズ
### em
親要素のfont-sizeを1としたときの大きさの倍率

### rem
root-emの略で、ルート要素（html要素）を1としたときの倍率

- html要素のフォントサイズを10pxにしておくと、remで使用する際に倍率の計算がし易い。
- 各種ブラウザでは基本的なフォンtのサイズは16pxとなっている。
- そのため、html要素で初期化する場合は62.5%と書くと良い。


### 要素のボックスモデル
コンテンツは4つの領域を持っている
- margin
  - border
    - padding
      - content
box-sizing属性はwidthとheightで指定する領域を変えられる（初期値はcontent）

## イメージも最小構成にしておくと再利用性が高まる
- 1pxのgif画像
  - 繰り返して背景にする
  - 透明にしておくことでバックグラウンドの色を変えられる

## background
- backgroundのショートハンドプロパティを個別のプロパティで上書きしたいときは必ず後に記述する
  - そうでないと初期値が入力される
    - background-color: transparent;
    - background-image: none;
    - background-repeat: repeat;
    - background-position: 0% 0%;
    - background-size: auto auto;
    - background-attachment: scroll;

## 親要素をa要素のクリック領域で覆いたい時のプラクティス

    .logo a {
      display: block;
      width: 100%;
      height: 100%;
    }


## マージンの相殺
- block属性の場合に隣接した要素同士でmarginの相殺が起こる
  - 隣接したmarginの片方が相殺されて消える
    - そのため、marginの値はmarginの大きい方の要素の値になる
  - display: inline-block;やfloatがかかっている場合は起こらない
- 入れ子になった要素同士でも相殺は起こる
  - 基本的に子要素のmarginは親要素を突き抜けて余白を作る
  - borderやpadding、インラインコンテンツが存在する場合はその限りではない
  - 親要素と子要素の間に余白を取りたい場合はpading-topを利用する
    - なぜならmargin指定の場合は親要素を突き抜けて外に出てしまうから


## height
- line-heightとheightの高さを同じにするとテキストを縦方向に中央寄せできる


## letter-spacing
- 文字同士の間隔を設定する（ちょっと読みやすくなるかも）


## transition
- CSSプロパティの値が変化する際に掛かる時間や変化の方法を制御することができる。
  - アニメーション効果を表現できる。
  - transitionには以下のようなプロパティがあり、個別に指定できる
    - transition-property
      - トランジションを適用するCSSプロパティを指定できる。初期値はall。
    - transition-duraiton
      - 値の変更完了までの所要時間。初期値は0s。
    - transition-timing-function
      - 変化の仕方の種類。初期値はease。
    - transition-delay
      - 開始の待ち時間。初期値は0s。


## 文書の構造の構造としては統一したいが、見た目には表示したくないときのプラクティス
    .hidden {
      desiplay: none;
    }

## section
- HTML5で追加された要素
- セクションごとに区切られる時に利用される要素
- 見出しを持つことが推奨されている

## time
- HTML5で追加された要素
- 日時を意味する要素
  - datetime属性をつけることで要素内の言葉の意味する情報を機械（クローラー）に伝えることができる
    - ex. `<time datetime="2017-12-24T0:9:30">今朝</time>`

### line-height
指定した値は子要素に引き継がれる
再利用性の高いコードを書くためには倍率指定（単位のない数字）を指定したほうが良さげ。

- 初期値はnormal。ブラウザが計算。
- 後は単位付きの数字や割合。
  - この数値を基準に子要素にも適用する
- 単位のない数値の場合はフォントサイズの倍率になる。
  - 子要素には倍率が適用される

# h1, h2, ...
font-weight: bold;が初期値に指定されている

# height, max-hegiht, min-width
そのままの高さを表す場合はheightだが、最大値だけを指定したい場合はmax-height
max-heightならば要素の高さが足りなければ、高さはその値に調整される。
min-heightはその逆

# liのための擬似クラス
- nth-child
- nth-of-typeA

# hoverによって背景色の色を変えたいとき
- a要素をblockとして透過画像などの背景を入れたほうが良い
  - a要素の背景変更によってその下の要素の背景が上書きされてしまうため

# 改行によるスペースのworkaround
- 改行をしない
- タグの中で改行をする
- 改行をコメントアウトする
- inlineやinline-block以外にする
- float-leftを使用する
- `display: table`を使う
- `display: flex`を使う

# text-overflow
文字列が枠からはみ出したり、開業しそうになったときの設定
## 「...」で省略する
```css
text-overflow: ellipsis; /* ...で省略 */
white-space: nowrap; /* 折り返し禁止 */
overflow: hidden; /* 省略した部分は隠す */
```

# ulとolの使い分け
順序に意味があるかないか。意味があるならol

# vertical-align
inlineの要素やtable-cellの場合に有効で、縦方向の配置を指定できる。

# transform
要素をいろいろアレできる
- scale(n), scale(x, y), scaleX(x), scaleY(y)
  - 拡大と縮小
- skewX(ndeg), skewY(ndeg)
  - deg分だけ要素を傾斜させる
- translate(npx), translate(npx, npx), translateX(xpx), translateY(ypx)
  - px分だけ移動させる
- rotate(ndeg)
  - 要素をndeg分だけ回転させる
- https://developer.mozilla.org/ja/docs/Web/CSS/transform
- https://caniuse.com/#feat=transforms2d

## transform-origin
変形時の基準点を指定できる

# ベンダープレフィックス
仕様が未確定な機能を選考で実装する時に、独自の拡張実装であることを明示するためにつける識別子。
草案段階の機能につけられる。
- https://caniuse.com

# CSSカウンタ
CSSでカウントできる
- counter-reset
  - カウンタの初期化
- counter
  - カウンタの宣言
- counter-increment
  - カウンタのインクリメント
- content: count(${counter})
  - カウンタの表示
