# HTML5 CSS3 モダンコーディングメモ

## デザインで利用する要素を選ぶ上で重要な要素
* そのサイトが達成したことはなにか
* どの数字を重要視するのか
* それによって効果的な要素、見た目を選ぶ

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

## コーディングの流れ
* ワイヤーの作成
* ベースのCSSの作成
  * 文字色、フォントサイズなど...
* ベースのコーディング
  * ざっくりとしたレイアウト、classづけ
* 個別要素の実装
  * まずは余白の確保
  * 個別の実装...

割とプログラミングっぽい

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

### `font-size: 0`にしてinline要素の改行を消すテクなどは多様される

## 要素のボックスモデル
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

## 基本的にinline要素の高さを調整するには
line-height

## 縦に中央配置する方法
* line-heightとheightの高さを同じにするとテキストを縦方向に中央寄せできる
* displayをtable, table-cellにして、vertical-align: midlle
* inline要素にしてvertical-align: middle

### letter-spacing
- 文字同士の間隔を設定する（ちょっと読みやすくなるかも）


### transition
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


### 文書の構造の構造としては統一したいが、見た目には表示したくないときのプラクティス
    .hidden {
      desiplay: none;
    }

### section
- HTML5で追加された要素
- セクションごとに区切られる時に利用される要素
- 見出しを持つことが推奨されている

### time
- HTML5で追加された要素
- 日時を意味する要素
  - datetime属性をつけることで要素内の言葉の意味する情報を機械（クローラー）に伝えることができる
    - ex. `<time datetime="2017-12-24T0:9:30">今朝</time>`

#### line-height
指定した値は子要素に引き継がれる
再利用性の高いコードを書くためには倍率指定（単位のない数字）を指定したほうが良さげ。

- 初期値はnormal。ブラウザが計算。
- 後は単位付きの数字や割合。
  - この数値を基準に子要素にも適用する
- 単位のない数値の場合はフォントサイズの倍率になる。
  - 子要素には倍率が適用される

## h1, h2, ...
font-weight: bold;が初期値に指定されている

## height, max-hegiht, min-width
そのままの高さを表す場合はheightだが、最大値だけを指定したい場合はmax-height
max-heightならば要素の高さが足りなければ、高さはその値に調整される。
min-heightはその逆

## liのための擬似クラス
- nth-child
- nth-of-typeA

## hoverによって背景色の色を変えたいとき
- a要素をblockとして透過画像などの背景を入れたほうが良い
  - a要素の背景変更によってその下の要素の背景が上書きされてしまうため

## 改行によるスペースのworkaround
- 改行をしない
- タグの中で改行をする
- 改行をコメントアウトする
- inlineやinline-block以外にする
- float-leftを使用する
- `display: table`を使う
- `display: flex`を使う

## text-overflow
文字列が枠からはみ出したり、開業しそうになったときの設定
### 「...」で省略する
```css
text-overflow: ellipsis; /* ...で省略 */
white-space: nowrap; /* 折り返し禁止 */
overflow: hidden; /* 省略した部分は隠す */
```

## ulとolの使い分け
順序に意味があるかないか。意味があるならol

## vertical-align
inlineの要素やtable-cellの場合に有効で、縦方向の配置を指定できる。

## transform
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

### transform-origin
変形時の基準点を指定できる

## ベンダープレフィックス
仕様が未確定な機能を選考で実装する時に、独自の拡張実装であることを明示するためにつける識別子。
草案段階の機能につけられる。
- https://caniuse.com

## CSSカウンタ
CSSでカウントできる
- counter-reset
  - カウンタの初期化
- counter
  - カウンタの宣言
- counter-increment
  - カウンタのインクリメント
- content: count(${counter})
  - カウンタの表示

## 子孫セレクタ、子セレクタ、隣接セレクタ
* .ancestor .descendant
  * `ancestor`より下のすべての`.descendant`に適用する
* .parent > .child
  * `.parent`のすぐ下の子要素の`.child`にのみ適用する
* .parent > .me + .neighbor
  * `.parent`の下の.meに隣接している`.neighbor`にのみ適用する

## HTML5での要素の分類
* メタデータ
  * head内の文書情報の定義や外部ファイルの読み込み
* フロー
  * body下の要素のほとんど
* セクショニング
  * 明示的に文書のアウトラインを定義する
    - ariticle
    - aside
    - nav
    - section
* ヘッディング
  * 見出し（セクショニングの見出しや暗黙的なアウトラインを定義する）
    * h1〜h6
* フレージング
  * いわゆるインライン要素、段落に入る要素にあたる
  * 基本的にフレージングの中にはフレージングの要素しか入らない
* エンベデッド
  * 外部リソースを埋め込む要素
    * ex. audio, canvas, iframe, ...
* インタラクティブ
  * ユーザーが操作することを想定している要素
    * ex. button, iframe, input, ...

## 上下でmarginの見え方が変わってしまう場合
どちらかにline-heightなどが入ってしまい、片方のmarginの見た目などが大きくなることがある
そういときは上下を別で指定してline-heightの大きさを考慮してみると良い

## CSS上の::beforeと::after 
HTMLコード上には現れない擬似的な要素を作り出してくれる
beforeは親要素内の最初に、afterは親要素内の最後に配置される
```
<p class="sample">
  ::before
    Sample Text.
  ::after
</p>
```
中身は`content`属性によって定義する
定義可能なのは以下のもののみ
* 文字列
* 画像
* 親要素の属性値
* CSSカウンタの数値

- なにも入力したくない場合は空文字を入力する必要がある
- inline属性なので高さをもたせたい場合はblockにする必要がある

block要素に変更して要素を覆うマスクのようなものが作れたり、「続きを読む」みたいなものを載せることができる

## ネガティブマージンの使い方
* 子要素であるa要素を親要素全体の領域に広げる必要があり、paddingが邪魔な時
  * padding分だけネガティブマージンで埋める
  * その上で、そのa要素でpaddingを作れば良い
  * ネガティブマージンでpaddingを埋めるということは、実質親要素のpaddingを相殺している

## JavaScriptの読み込み場所
パフォーマンスの問題でドキュメントの最後に読み込まれることが多い
* HTMLは上から解釈をされ、途中でJavaScriptの読み込みが始まるとそれが終わるまで描画が止まるから

## CSSのプラクティス
* 再利用をするための基礎的なclassとそれを拡張するためのclassに分ける
ex. `item`、`item-m`、`item-l`
- itemにはデフォルトの設定をすべて設定
- item-mには拡張のための設定を書く
利用時には`class="item item-m"`のようにする

## 要素はドキュメント内のセマンティック的な立ち位置を意味する
`section`を使うならば、その要素内のコンテンツはsectionで区切られているということを意味する
同じく`header`であるならば、そこはサイトのheader的な意味を持つと解釈される

## transition
いくつかのアニメーションに動きを表す関数がある
ex.
- linear
- ease
- ease-in
- ease-out
- ease-in-out

## フロントの設計思想
### グレースフルグラデーションｎ
最新のブラウザをターゲットにしつつも、レガシーブラウザでもレベルを落として表示する
### プログレッシブエンハンスメント
レガシーブラウザをターゲットにしつつも、モダンブラウザではリッチな見せ方をする

## flexbox
gloatやtableなどの上位互換
簡単にレイアウトが作れる

レガシーブラウザなどでは対応していなかったりする
- shimや自動的にベンダープレフィックスを付与してくれたりするビルドツールを使うなら利用もあり

* https://www.webcreatorbox.com/tech/flexbox
* https://www.webcreatorbox.com/tech/flexbox-tips
* https://www.webcreatorbox.com/tech/css-flexbox-cheat-sheet

## background-size
* cover
全体を覆うことができる
* http://www.htmq.com/css3/background-size.shtml

## ::before, ::afterの小技
**::before, ::afterをinline-block属性にして並べることで、heightとwidthを設定した要素を元のコンテンツの左右に並べることができる
例: --- (content) --- みたいなデザインを作れる

## セレクタの詳細度
どのセレクタが「強い」かを意味する
CSSが競合した時に優先されるもの
同じ詳細度の場合は書かれたものが後のものが優先される

### 詳細度の強さ
style属性 > id > class > 擬似クラス > 属性 > 要素型、疑似要素

## 変更に強いCSSのために
意味合い的な命名をすることを心がけるとよい
→直接的な見た目に関わる命名は避けた方が良い

## シングルクラス設計とマルチクラス設計
### シングルクラス
1つの要素に対して1つのクラスをつけてスタイルをすべて表現する

### マルチクラス
1つの要素に対して複数のクラスをつけて、一つのクラスに重複をまとめる
詳細度による上書きを利用して複数のクラスを表現する
CSSを簡潔にできる分、HTMLが肥大化しがち

#### CSSプリプロセッサを使う
マルチクラスをextendなどを利用して作ることができるため、マルチクラスの問題を解決できる

## header要素はブロック要素
::beforeや::afterなどを利用する時にinlineやinline-blockにしたくなるかも

## display: table
table, table-cellによって従来のテーブルのようなレイアウトをCSSだけで実現できる
`border-collapse: separate;`と`border-spacing`を組み合わせると子要素のtable-cellの間隔を調整できる

## position
- static
- relative
- absolute
- fixed

## heightやwidthのTIPS
%指定をする場合は基本的に親要素の高さが指定されている必要がある
しかし、positionがabsoluteやfixedの場合には、その限りではない

* absoluteやfixedが指定された場合は自動的にblock属性になる

### 高さを指定しない場合
子要素の高さの合計値になる

## marginやpaddingによって高さを確保する
marginやpaddingの%指定は親コンテンツの横幅を元に算出するため、横幅から縦幅を計算したい時に利用できる

## 疑似要素は要素の子要素として存在する
そのため、`target::after`というふうに書いたclassを複数持たせて修飾できる
* 疑似要素のポリモーフィズム的なのを実現できる

## .zindex
要素の重ね純を指定する
大きい数値順になる

## ベクターファイルの利点
どれだけ拡大をしてもキレイに表示できる
ex. svg, アイコンフォント
- http://ascii.jp/elem/000/000/996/996503/

## HTML5で追加されたinput
- search
- tel
- url
- email
- dat
- time
- number
- range
- color

## formで大きさを定義するときのTIPS
form要素で大きさを定義して、inputをblock要素として大きさを%を使って定義する

## rgbaの指定方法
rgba(red, green, blue, transparecy)
### 16進数
- red
- green
- blue
### 0~1
- transparecy
## opacityとrgba指定の透明度の違い
### opacity
要素全体を透過させる
### rgba指定
色のみを透過させる
→つまり、rgbaを使ったbackground-colorだけ、colorだけが透過される
