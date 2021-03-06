# Human Readable CSS Style Guide
Human Readable CSS Style Guide with WYSIWYG HTML Editor, apply to Web Components.

人間に読みやすいコンポーネント指向のCSS記述法

そのまま使える WYSIWYG HTML Editor を含む。

最終更新：2016年5月13日 Yoshiki HAYAMA @storywriter

本プロジェクトはオープンソースプロジェクトである。
プロジェクトの代表は Yoshiki HAYAMA @storywriter http://storywriter.jp/ である。

WYSIWYG HTML Editor のデモは http://storywriter.jp/hrcss/ で公開している。

このプロジェクトの概念について、わかりやすいプレゼン資料は http://www.slideshare.net/storywriterjp/css-2016513-codegrid に公開している。


## 原則

- 人間にとって読みやすいこと。

- シンプルに使うことができること。

- スタイルシートの知識だけで、コンポーネントが作成できること。すなわち JavaScript がわからないウェブ制作者にも、コンポーネントが作成できること。
 - 本仕様中には、HTML5 の data 属性を用いれば、もっとシンプルになる箇所は多々ある。しかし、本仕様では、できるかぎり class 属性のなかに押し込めた。つまり「CSSの世界」のなかに閉じることで、JavaScript を知らないウェブ制作者にも、CSSの知識さえあれば、コンポーネントの編集まではできるようにした。
 - これは、本仕様が、何十人、何百人というような大人数で、何年も運用していくような、大規模な制作現場でも耐えられることを目指しているからだ。大規模な環境での制作になるほど、個人ごとのスキルに跛行があり、時間とともにメンバーは入れ替わる。すべての制作者が JavaScript をしっかりと理解していることなど、大規模な現場ではあり得ない。

- HTML/CSS実装の、ベストプラクティスの集積であること。

- HTMLおよびCSSが、W3Cの仕様でいうところの「堅牢」であること。すなわち、HTMLおよびCSSが Valid であること。

- 広く普及した技術で操作できること。具体的には jQuery で操作できること。

- できるだけ依存する JavaScript ライブラリを少なくすること。
 - 具体的には、WYSIWYG HTML Editor が依存するのは jQuery 本体と jQuery UI Core、そして jQuery UI Interactions Sortable の3つのライブラリのみである。
 - これは、WYSIWYG HTML Editor がさまざまな用途、とくに、さまざまなCMSの管理画面から呼び出されることを想定しており、そのときに他ライブラリとの競合を最小限に抑えるためである。

- コンポーネント指向であること。ここでいう「コンポーネント」とは「Web Components」という意味ではなく、いわゆる制作現場て用いられる、インタフェースの最小要素としてのコンポーネントを指す。（参考：コンポーネントという単語は、制作会社によってさまざまな呼び名がある。エレメント、モジュール、オブジェクト、ブロック、パーツ...。たいていは、どれも同じものを指している）

- コンポーネントの用途と、ネストできる要素を定義できること。

- 「Web Components」にもシームレスに対応すること。

- 既存のHTML/CSSと同居できること。
 - 大規模な環境ほど、一夜にしてすべてのコンテンツを移行できるなどあり得ない。ふつうのHTML/CSSと混在することができること。

- わかりやすいサンプルとして、 Bootstrap と Font Awesome ですぐ利用できること。


## 思想

### 第1の指針：セレクタ名は人間への指示のために書く。

- CSSが、大規模な運用になるにつれ、CSSの保守性をいかに維持するか、という試みがされてきた。例えば、OOCSS、BEM、SMACSS といったものだ。

- OOCSS、BEM、SMACSS のような「コーディング規約」は、どれも、ウェブサイトやウェブページを、領域に分割し、それぞれに管理を分けよう、という考え方をしている。そのため、セレクタには、領域の名前をつけることが多い。たとえば `.header__title` という具合だ。おそらくこれは、ページのヘッダ部分のタイトルだろう。

- この記述を、ちょっと別の角度から見てみよう。`.header__title` という命名は、じつにセマンティックだ。だが、`class`の値がセマンティックなのは、誰のためだろうか。

- `<header>` 要素でマークアップされた要素は、マシンリーダブルである。すなわち、人間以外の、たとえばロボットが読んで、意味を理解することができる。

- しかし`class="header__title"`と書かれていても、マシンはこれを解釈しない。マシンのため「だけ」であれば、`class="header__title"`とあっても、`class="a"`とあっても、マシンは困らない。

- ここで我々は気がつく。CSSの「スタイルガイド」や「コーディング規約」は、マシンリーダブルのために書くのではない。ヒューマンリーダブル、すなわち、人間が人間に読ませるために書くのだ。

- あらたてめて、先の例を見てみよう。`.header__title`は、領域の名前をつけている。ここまでの議論をふまえて考えると、これは「セマンティック」のためのようで、じつは「指示」を書いているのだ。他の人間に「この部品はヘッダのためのものだから、他では使うな」という「指示」を書いている。

- CSSが大規模な運用でからまるのは、「スコープ定義がない」からである、と言われるが、これは勘違いだ。BEMのように、徹底した設計することで、スコープをつくることはできる。

- 現実の問題として、CSSが大規模な運用でからまるのは、言語仕様のせいではない。きちんと設計したCSSでも、そのスコープを無視したり、都合よく解釈して、コードを勝手に拡張する輩がいるからだ。それはあなたの隣の人かもしれないし、ひょっとしたら1ヶ月後のあなた自身かもしれない。

- セレクタの命名が、人間への「指示」だとするならば、それは領域の名前だけでなく、もっともっと、具体的な指示を含めてよいのではないだろうか。

- たとえば、`.header__title`というセレクタ名は、意識のない制作者によって`<main>`要素のなかで使われるかもしれないが、`.header-title__you-can-use-this-selector-just-only-in-header`という名称であれば、――それは美しくはないかもしれないが――より多くの制作者が、このセレクタを、正しく使うことができるだろう。

- CSSがスパゲッティ化すると、リファクタリングは困難だ。たとえば、ある1つのCSSファイルが、10,000のウェブページから読み込まれていることがある。1つのセレクタの編集が、10,000ページのどこに影響するのか、特定するのは困難を極める。特定できたとしても、ほかに影響を与えないように、それを修正するのは、さらに困難だ。そのため、たいていの場合は、そのリスクと手間を避けて、新しいセレクタを書いて終わらせようとする。そうして、CSSはさらに肥大化し、複雑になっていく。

- 制作チームが、物理的に（あるいは心理的に）離れたところにいると、この問題は、より噴出しやすくなる。スキルも考え方も、そして権限もバラバラのメンバーが、ひとつの巨大なウェブサイトにかかわろうとすると、設計思想を共通するのは、より難しくなる。そして、CSSはかんたんにスパゲッティ化していく。

- 多くの、そしてスキルも考え方も異なる制作者が、同じように制作するために、セレクタは「指示」のために命名しよう。


### 第2の指針：コンポーネント指向であるために、セレクタのなかに必要な情報を含める。

- CSSがコンポーネント指向であるためには、次の2点が要る。1つ目は、組み合わせてコンポーネントにしたとき、それ自身の用途を説明するすべがあること。2つ目は、そのコンポーネントにネストできる要素を定義できること。誰かがつくったセレクタを、ほかの誰か（1ヶ月後の本人を含む）が再利用するには、それが何のために、どこから呼び出されるものであるかが、わからないければ、再利用できないのだ。

- 世の中で、「スタイルガイド」「エレメント一覧表」「コンポーネント集」「モジュールリスト」といった名前で呼ばれるたぐいのものは、多くある。各組織、各プロダクトごとに存在していることある。そして、その多くが、うまく運用できないという悩みを抱えている。

- その大きな原因は、「部品」だけを提供していることだ。部品をどのように使うか、そしてどのように使ってはいけないか、ネストしてよい要素は何か、ネストしてはいけない要素は何か、それらの情報がなければ、スタイルガイドを正しく運用することはできない。

- なぜなら、スタイルガイドで提供されるべき部品の大きさは、その対象となるプロダクトによって異なるからだ。

- たとえば Bootstrap で定義されている部品は、さまざまなウェブサイトに適用できるよう、自由度が大きく設計されている。だから、Bootstrap のスタイルガイドをそのまま参考にして、あるプロダクトに限定されたスタイルガイドをつくろうとすると、なんでもできてしまう、自由度が高すぎるスタイルガイドができてしまう。特定のプロダクトのスタイルガイドであれば、Bootstrap のスタイルガイドより、もっともっとコードを固定して、部品を限定したものにしなければならないだろう。

- このように、スタイルガイドには粒度があり、それを定義する情報が要る。

- しかし、CSSの標準の文法には、その制約を記述するための方法がない。

- そのため、多くの組織では、別のガイドラインとして、新たな分厚いドキュメントを用意したりする。そうすると、制作者は、ものをつくるときに、複数のドキュメントを参照せねばならず、こんがらがったり、面倒くさがったりして、けっきょくは、そのスタイルガイドは守られない。

- より正しく言うと、別のガイドラインを参照させるということ自体が、制作の現場としては難易度が高すぎる、非現実的に近い作業なのである。

- この問題を解決し、CSSをコンポーネント指向にするためには、セレクタそのものに、そのコンポーネントが何者であるか、ネストできる要素が何であるか、記述するようにする。セレクタだけを見れば、それが何者であるか、明らかであるようにすればよい。

- ひとつ配慮しておくべき点は、class属性のなかに情報を含めるのがよく、data属性を（できるだけ）避けるようにしたほうが、より多くの制作者にとって、わかりやすくなる、ということだ。何十人、何百人というような大人数で、何年も運用していくような、大規模な制作現場では、個人ごとのスキルに跛行があり、時間とともにメンバーは入れ替わる。そのため、すべての制作者が data属性になじんでいることは、残念ながら、あり得ない。class属性にこだわり、いわゆる「CSSの世界」に閉じたほうが、より運用を安定させることができる。


### 第3の指針：セレクタは読みやすく、そして理解しやすく書く。

- 過去に「良いコード」とは何かを調べたことがある。効率や体裁など、さまざまな要素があるが、まとめていくと、ある1点においては必ず共通していた。――すなわち、「読みやすいコードは良いコードである」ということだ。

- そして、読みやすいとは、第一には視認性がよい、ということだった。先にあげた例の`.header-title__you-can-use-this-selector-just-only-in-header`は、意味はわかりやすいが、視認性がよいかというと疑問だ。

- 意味と読みやすさ。この2つを、両立させるようにするとよい。ポイントは「空白をとること」「区切り文字を入れること」。さまざまな記号を試したが、「半角スペース」と「( )」の組み合わせが、もっとも見やすかった。

- また「半角スペース」で区切ることで、既存の CSS セレクタとは別個に、「指示」のためのセレクタを追加することができる。たとえば、`class="header-title ( 指示のためのセレクタ )"`といった具合だ。


### 第4の指針：コンポーネント指向であるために、WYSIWYG HTML Editor を標準装備している。

- 上記まで指針を立てて、すべてを複数のメンバーで共有したとしても、それでも、コンポーネントにしたHTMLを、統一して運用するのは、なかなかうまくいかない。コードを読んで、ルールのとおりに実装する、というときに、細部でどうしても行き違いや、解釈の差が生まれる。それほどに、CSSの大規模な運用とは難しいものだ。

- そこで、スタイルガイドにそってコンポーネントを組み立てHTMLを仕上げるための WYSIWYG HTML Editor も、スタイルガイドとともに提供するとよい。

- コードを読んだり、複雑なスタイルガイドのルールを理解しなくても、その WYSIWYG HTML Editor を使っていれば、自然とスタイルガイドが守れるようにする。

- WYSIWYG HTML Editor のデモは http://storywriter.jp/hrcss/ で公開している。

- また、Human Readable CSS で記述した設定ファイルは、そのままウェブページとして表示できるので、スタイルガイドとして使うことができる。別資料として管理する必要がない。スタイルガイドとして表示したサンプルは http://storywriter.jp/hrcss/user-components/sample.html で公開している。


## 解法（具体的なコード）


### 技術的な着眼点

#### CSSの視点

- CSS仕様のセレクタ名として使える文字列は限られている。

https://www.w3.org/TR/css3-selectors/#lex

- 注目すべきは、「-」から始まるセレクタ名は、CSSとしては不適合となる点。言い換えると、「-」から始まる文字列は、CSSとして登場することはない。

#### HTMLの視点

- いっぽうで、HTML仕様で、class属性の値として含める文字列には制約はない。つまり、「-」から始まる文字列が含まれていても、HTMLとしては（驚くべきことに！）「適合」になる。（なお、 XHTML1.0 Transitional では &amp; だけは「不適合」だったが、HTML5では、それも「適合」となった）

https://www.w3.org/TR/html/dom.html#classes

- つまり：
 - class属性には、じつは何を書いてもよい。そして、書いた文字列を、CSSファイルのなかで使わなくてもよい。
 - 「-」から始まる文字列は、CSSのセレクタ名として用いられることはない。
 - 極端には、class属性値は日本語でもよい。（アスキー文字である必要はない）

#### JavaScriptの視点

- また、jQuery の仕様として、興味深いことに「-」から始まるセレクタも操作することができる。つまり`$( '.-任意のセレクタ' )`という jQuery のコードは、正しく動作する。

- 備考：`[class*=-attribute]`のような書き方もできる。


#### ユーザビリティの視点

- 視認性をよくするためには、「空白をとること」「区切り文字を入れること」。長い文字列は、視認性がよくない。「指示」のためのセレクタは、半角スペースで、既存のセレクタと分け、「( )」内に記述する。たとえば、`class="header-title ( -editable )"`のように書く。

- また「半角スペース」で区切ることで、既存の CSS セレクタとは別個に、「指示」のためのセレクタを追加することができる、という実装面のメリットも得られる。



### 具体的なコードサンプル

#### 基本的な文法

```html
<div class="( -block )">
  <div class="( -element )">
    <p class="lead ( -element -editable )">...</p>
```

文法の基本：

- 人間に「指示」するための指示文を (  ) で囲む。
- 人間に「指示」するための指示文は「-」から始める。
- カッコと文字列は、半角スペースで区切る。
- 指示文が複数あるときは、半角スペースで区切って、ひとつの (  ) に入れる。
- 既存のCSSと混在してかまわない。

主となる指示文：

- ( -block )：BEMのブロック要素。
- ( -element )：BEMのエレメント要素。
- ( -editable )：文字列の編集ができる。
- ( -attribute:xxx )：xxx属性の編集ができる。
- ( -child:xxx )：xxxセレクタをもつ要素しか子要素にとらない。
- ( -parent:xxx )：xxxセレクタをもつ要素しか親要素にとらない。

補助的な指示文：（よくあるケースを指示文にしたもの）

- ( -list )：リストである。（子要素は -listitem である）
- ( -listitem )：リストアイテムである。（親要素は -list である）
- ( -table )：テーブルである。（子要素は -tbody か、-tr である）
- ( -tbody )：テーブルの行グループ thead, tbody, tfoot である。（親要素は -table で、子要素は -tr である）
- ( -tr )：テーブルの行 tr である。（親要素は -table か -tbody で、子要素は -td である）
- ( -td )：テーブルのセル td, th である。（親要素は -tr である）

WYSIWYG HTML Editorのための文字列：

- ( -wysiwyg )：編集可能領域である。
- ( -ignore )：`<tr>`,`<td><th>`,`<thead><tbody><tfoot>`は、`<table>`の子要素として実装しないと、table 要素として認識しない。そのとき、`<table class="table ( -ignore )"><td class="( -td )">`のように、`<table>`自身はコンポーネントから無視させるために使う。


#### 最終的に生成されるHTML

```html

<div class="contentHeader">

  <h1 class="( -editable )">Lorem ipsum dolor sit amet</h1>
  <p class="contenHeader-description ( -editable )"><em>Lorem</em> ipsum dolor sit amet, consectetur adipisicing elit,</p>

</div>

<div class="contentMain ( -wysiwyg )">

  <div class="textAndImage ( -block )">

    <div class="textAndImage-left ( -child:-element )">

      <p class="( -element -editable )">Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut</p>

      <ol class="listitem-ol ( -element -list -child:listitem-li )">
        <li class="listitem-li ( -listitem -editable -parent:listitem-ol )">labore et dolore magna aliqua.</li>
        <li class="listitem-li ( -listitem -editable -parent:listitem-ol )">Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut</li>
      </ol>

      <p class="linkArrow ( -element )"><i class="fa fa-circle ( -attribute:class )"></i><a href="#" class="( -editable )">aliquip ex ea commodo consequat.</a></p>

    </div>

    <div class="textAndImage-right ( -child:imgCaption )">

      <p><img src="..." alt="..." class="( -editable -attribute:alt )"></p>

      <p class="imgCaption ( -element -editable )">Duis aute irure</p>

    </div>

  </div>

</div>
```


#### テンプレートHTML

```html

<div class="contentHeader">

  <h1 class="( -editable )"></h1>
  <p class="contenHeader-description ( -editable )"></p>

</div>

<div class="contentMain ( -wysiwyg )">

</div>
```


#### コンポーネント定義HTML


```html

<div class="textAndImage ( -block )">
  <div class="textAndImage-left ( -child:-element )">
  </div>
  <div class="textAndImage-right ( -child:imgCaption )">
    <p><img src="..." alt="..." class="( -editable -attribute:alt )"></p>
  </div>
</div>

<p class="( -element -editable )"></p>

<ol class="listitem-ol ( -element -list -child:listitem-li )">
  <li class="listitem-li ( -listitem -editable -parent:listitem-ol )"></li>
</ol>

<p class="linkArrow ( -element )"><i class="fa fa-circle ( -attribute:class )"></i><a href="#" class="( -editable )"></a></p>

<p class="imgCaption ( -element -editable )"></p>
```


#### 参考：最終的に生成されるHTMLを日本語にしたときのイメージ

```html

<div class="contentHeader">

  <h1 class="( -テキスト編集可 )">Lorem ipsum dolor sit amet</h1>
  <p class="contenHeader-description ( -テキスト編集可 )"><em>Lorem</em> ipsum dolor sit amet, consectetur adipisicing elit,</p>

</div>

<div class="contentMain ( -WYSIWYG編集可 )">

  <div class="textAndImage ( -ブロック )">

    <div class="textAndImage-left ( -子要素はエレメントのみ可 )">

      <p class="( -エレメント -テキスト編集可 )">Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut</p>

      <ol class="リスト ( -エレメント -子要素はリストアイテムのみ可 )">
        <li class="リストアイテム ( -テキスト編集可 -親要素はリストのみ可 )">labore et dolore magna aliqua.</li>
        <li class="リストアイテム ( -テキスト編集可 -親要素はリストのみ可 )">Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut</li>
      </ol>

      <p class="linkArrow ( -エレメント )"><i class="fa fa-circle ( -class属性のみ編集可 )"></i><a href="#" class="( -テキスト編集可 )">aliquip ex ea commodo consequat.</a></p>

    </div>

    <div class="textAndImage-right ( -子要素は.imgCaptionのみ可 )">

      <p><img src="..." alt="..." class="( -テキスト編集可 -alt属性のみ編集可:alt )"></p>

      <p class="imgCaption ( -エレメント -テキスト編集可 )">Duis aute irure</p>

    </div>

  </div>

</div>
```

### 実装対象のイメージ

- この WYSIWYG HTML Editor は、大規模なウェブサイトの運用を念頭においており、何らかのCMSに組み込んで利用することを想定している。

 - ただし、CMSに組み込むさい、CMSのコンテンツ管理画面に埋め込むことは「想定していない」。埋め込む先は、コンテンツ管理画面から呼び出される「プレビュー画面」を想定している。

 - 人間は、目に見えているものと、じっさいに仕上がるものに差があると、難しく感じる。せっかく WYSIWYG にしたのに、コンテンツ管理画面に埋め込むと、たいていは管理画面の諸々の情報が邪魔をして、完全に見たままを再現することはできない。そこで、見た目と最終形が同じになる「プレビュー画面」に、この WYSIWYG HTML Editor を埋め込むとよい。
 
- この WYSIWYG HTML Editor のためのコンポーネント集は、そのままふつうのウェブページとして表示することができる。つまり、コンポーネントの管理を別資料にする必要がない。

- コンポーネント集のデモは http://storywriter.jp/hrcss/user-components/sample.html で公開している。


## 歴史

- 本プロジェクトは、もともとは2009年ごろ、コンポーネントベースの WYSIWYG HTML Editor の構想からはじまった。

- 2012年ごろに、 WYSIWYG HTML Editor の最初のプロトタイプが登場した。このプロトタイプは、一部のユーザーに公開された。

- 2014年〜2015年、羽山の長年の運用経験から、大規模ウェブサイトでの HTML と CSS の運用における課題をまとめ、そのなかから、Human Readable CSS のベースとなる記述方法を考案した。

- 2016年、日本のフロントエンドエンジニアが集まるイベント「CodeGrid四周年記念パーティー」に、羽山が登壇するのを機に、Human Readable CSS にあわせて、WYSIWYG HTML Editor を再実装。5月1日に公開した。


------
この文書は日本語で書かれているが、英語や他言語に翻訳などして、広めていただけると嬉しいです。

------


