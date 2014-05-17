# 序

> ロールモデルが重要なのだ。 <br/>
> -- アレックス・マーフィー巡査 / ロボコップ

Rubyディベロッパーとして、私は常にあることに悩まされてきました -
Pythonディベロッパーは偉大なプログラミングスタイルガイド
([PEP-8](http://www.python.org/dev/peps/pep-0008/))
を持っていますが、
我々には公式のコーディングスタイルやベストプラクティスを
一切持ち合わせていません。
そして、私はそれこそが問題であると確信しています。
また、Rubyが持っているような素晴らしいハッカーコミュニティは、
誰もが羨むようなドキュメントを作り出す力があるはずであるとも確信しています。

このガイドは、私達の社内製Rubyコーディングガイドから生まれました
(著者は[私](https://github.com/bbatsov))。
私がこのガイドを書くと決めたときは、一般のRubyコミュニティのメンバーに
興味を持ってもらえるだろうか、社内製のガイドはあまり必要とされていないのではないか
と考えていました。
しかし、コミュニティ駆動の、コミュニティに認められた、
Rubyのための慣習、語法、スタイル規定は、
確実にRubyコミュニティに有益たりえるのではないでしょうか。

このガイドを発端に、私は世界中の優れたRubyコミュニティのメンバーから、
たくさんのフィードバックを受けています。
全ての提案、サポートに感謝します！
お互いに、また全てのRubyディベロッパーにとって有益なリソースを、
一緒に作ることができています。

ところで、もしあなたがRailsが好きであれば、
こちらの補足も確認してみてください。
[Ruby on Rails 3 & 4 Style Guide](https://github.com/bbatsov/rails-style-guide).

# The Ruby Style Guide

このRuby style guideは、他のRubyプログラマーが保守できるコードを書くための
ベストプラクティスを採用することをおすすめします。
実際の使われ方を反映したスタイルガイドは使われるようになり、
理想論にとどまり、それを採用することがリスクと感じる人々に拒絶されるような
スタイルガイドは全く使われなくなります &nbdash;
たとえそれがどんなに素晴らしいものであっても。

このガイドは、関連するルールに基づいていくつかのセクションに分かれています。
ルールの後ろにその論理的根拠も付け加えるように努めています
(自明であると判断したもの以外は)。

私はこれら全てのルールをどこからともなく考えついたわけではありません -
これらのほとんどは、私のプロフェッショナルソフトウェアエンジニアとしての
豊富な経験と、Rubyコミュニティのメンバーからの意見や提案、
また、["Programming Ruby 1.9"](http://pragprog.com/book/ruby4/programming-ruby-1-9-2-0)や、
["The Ruby Programming Language"](http://www.amazon.com/Ruby-Programming-Language-David-Flanagan/dp/0596516177)のような、
様々な高度で評価の高いRubyプログラミングリソースに基づいています。

このガイドはまだ未完成です - いくつかのルールはサンプルがなく、
いくつかのルールは説明が不十分です。
やがてこれらの課題は対応されます - 今後これらを記憶にとどめておきます。

PDFやHTMLのコピーはこのガイドを使って作成できます
[Transmuter](https://github.com/TechnoGate/transmuter)。

[RuboCop](https://github.com/bbatsov/rubocop)は、
このスタイルガイドに基づいたコード分析器です。

以下の言語の翻訳が利用可能です:

* [中国語(簡体)](https://github.com/JuanitoFatas/ruby-style-guide/blob/master/README-zhCN.md)
* [中国語(繁体)](https://github.com/JuanitoFatas/ruby-style-guide/blob/master/README-zhTW.md)
* [フランス語](https://github.com/porecreat/ruby-style-guide/blob/master/README-frFR.md)
* [スペイン語](https://github.com/alemohamad/ruby-style-guide/blob/master/README-esLA.md)
* [ベトナム語](https://github.com/scrum2b/ruby-style-guide/blob/master/README-viVN.md)

## 目次

* [レイアウト](#レイアウト)
* [構文](#構文)
* [命名規則](#命名規則)
* [コメント](#コメント)
    * [注釈](#注釈)
* [クラス](#クラス)
* [例外](#例外)
* [Collections](#collections)
* [文字列](#文字列)
* [正規表現](#正規表現)
* [パーセントリテラル](#パーセントリテラル)
* [メタプログラミング](#メタプログラミング)
* [雑則](#雑則)
* [ツール](#ツール)

## レイアウト

> ほとんどすべての人が、彼ら自身のではないスタイルは
> 不快で合理的でないと確信している。
> 「彼ら自身の」を除けば、おそらく正しいのだが、、、
> -- Jerry Coffin (on indentation)

* ソースファイルのエンコーディングには`UTF-8`を用いましょう。
* インデントには**スペース**2つ(別名ソフトタブ)。 (ハード)タブを用いてはいけません。

    ```Ruby
    # 悪い例 - 4つのスペース
    def some_method
        do_something
    end

    # 良い例
    def some_method
      do_something
    end
    ```

* Unix-styleの改行にしましょう。
(*BSD/Solaris/Linux/OS X ユーザーはデフォルトで設定されています。
  Windows ユーザーは特に注意が必要です。)
    * もしGitを使っていれば、プロジェクトにWindowsの改行が紛れ込まないように、以下の設定を追加したほうがよいかもしれません:

    ```bash
    $ git config --global core.autocrlf true
    ```

* 命令文や式の区切りに`;`を用いてはいけません。
  当然、１行につき式１つにしましょう。

    ```Ruby
    # 悪い例
    puts 'foobar'; # 余分なセミコロンです。

    puts 'foo'; puts 'bar' # ２つの式が１行にあります。

    # 良い例
    puts 'foobar'

    puts 'foo'
    puts 'bar'

    puts 'foo', 'bar' # 特にputsでは適用されます。
    ```

* 本文のないクラスは１行のフォーマットが好まれます。

    ```Ruby
    # 悪い例
    class FooError < StandardError
    end

    # 悪くない例
    class FooError < StandardError; end

    # 良い例
    FooError = Class.new(StandardError)
    ```

* １行のメソッドは避けましょう。
  いくらか使われているところもありますが、
  それらの定義構文の仕様が望ましくないとさせるいくつかの特殊性があります。
  ともかく - １行メソッドには多くとも式１つまでにすべきです。

    ```Ruby
    # 悪い例
    def too_much; something; something_else; end

    # 悪くない例 - 最初の ; は必要です。
    def no_braces_method; body end

    # 悪くない例 - ２つ目の ; は任意です。
    def no_braces_method; body; end

    # 悪くない例 - 文法上は正しいです。ただし、; がない記述は少し読みづらいです。
    def some_method() body end

    # 良い例
    def some_method
      body
    end
    ```

    本文が空のメソッドはこのルールの例外です。

    ```Ruby
    # good
    def no_op; end
    ```

* 演算子の前後、コンマ、コロン、セミコロンの後ろに、`{`の前後、`}`の前にはスペースを入れましょう。
  スペースはRubyのインタープリタには(ほとんどの場合)重要ではありませんが、
  スペースの適切な使用は、読みやすいコードを容易に書くための鍵です。

    ```Ruby
    sum = 1 + 2
    a, b = 1, 2
    1 > 2 ? true : false; puts 'Hi'
    [1, 2, 3].each { |e| puts e }
    ```

    演算子についてただひとつの例外は、指数演算子です:

    ```Ruby
    # 悪い例
    e = M * c ** 2

    # 良い例
    e = M * c**2
    ```

    `{` と `}`は、構文の明確化のために有用です。
    だから、文字列に式を埋め込む時と同様に、
    ブロックやハッシュ構文に使われます。
    ハッシュ構文には、２つのスタイルが許容できます。

    ```Ruby
    # 良い例 - スペースを { の後と } の前に入れる
    { one: 1, two: 2 }

    # 良い例 - スペースを { の後と } の前に入れない
    {one: 1, two: 2}
    ```

    １つ目の構文は、わずかながら少し読みやすいです(そして、ほぼ間違いなく一般的なRubyコミュニティで人気があります)。
    ２つ目の構文は、ブロックとハッシュを視覚的に差別化できるという点で有利です。
    どちらでも片方を採用すれば、常に同じ構文を採用しましょう。

    文字列に埋め込む構文も、２つのスタイルが許容できます:

    ```Ruby
    # 良い例 - スペースを入れない
    "string#{expr}"

    # 良い例 - ほぼ間違いなくにこちらのほうが読みやすい
    "string#{ expr }"
    ```

    １つ目の式は、他の式よりも非常に人気があり、一般的にこちらを使うように進められる書き方です。
    一方２つ目は、(間違いなく)少し読みやすいです。
    ハッシュと同じように - 片方を採用すれば、常に同じ方を採用しましょう。

* `(`、 `[`の後と、`]`、 `)`の前にはスペースは入れません。

    ```Ruby
    some(arg).other
    [1, 2, 3].size
    ```

* `!`の後にはスペースは入れません。

    ```Ruby
    # 悪い例
    ! something

    # 良い例
    !something
    ```

* `when`は`case`と同じ深さに揃えましょう。
  多くの人が同意できないのを知っていますが、
  このスタイルは"The Ruby Programming Language"、"Programming Ruby"
  双方で確立されたものなのです。

    ```Ruby
    # 悪い例
    case
      when song.name == 'Misty'
        puts 'Not again!'
      when song.duration > 120
        puts 'Too long!'
      when Time.now.hour > 21
        puts "It's too late"
      else
        song.play
    end

    # 良い例
    case
    when song.name == 'Misty'
      puts 'Not again!'
    when song.duration > 120
      puts 'Too long!'
    when Time.now.hour > 21
      puts "It's too late"
    else
      song.play
    end
    ```

* 条件式を変数に代入するときは、
  その式の通常のアラインメントを維持しましょう。

    ```Ruby
    # 悪い例 - かなり複雑です
    kind = case year
    when 1850..1889 then 'Blues'
    when 1890..1909 then 'Ragtime'
    when 1910..1929 then 'New Orleans Jazz'
    when 1930..1939 then 'Swing'
    when 1940..1950 then 'Bebop'
    else 'Jazz'
    end

    result = if some_cond
      calc_something
    else
      calc_something_else
    end

    # 良い例 - 何が行われているか明らかです
    kind = case year
           when 1850..1889 then 'Blues'
           when 1890..1909 then 'Ragtime'
           when 1910..1929 then 'New Orleans Jazz'
           when 1930..1939 then 'Swing'
           when 1940..1950 then 'Bebop'
           else 'Jazz'
           end

    result = if some_cond
               calc_something
             else
               calc_something_else
             end

    # 良い例 (少しだけ幅の効率がよいです)
    kind =
      case year
      when 1850..1889 then 'Blues'
      when 1890..1909 then 'Ragtime'
      when 1910..1929 then 'New Orleans Jazz'
      when 1930..1939 then 'Swing'
      when 1940..1950 then 'Bebop'
      else 'Jazz'
      end

    result =
      if some_cond
        calc_something
      else
        calc_something_else
      end
    ```

* 定義式の間には空行をいれ、
  メソッド内の論理的段落ごとに分割しましょう。

    ```Ruby
    def some_method
      data = initialize(options)

      data.manipulate!

      data.result
    end

    def some_method
      result
    end
    ```

* メソッド呼び出しの最後の引数の後ろのコンマは避けましょう。
  引数が複数行にわかれていない時は、特に避けましょう。

    ```Ruby
    # 悪い例 - 簡単に引数を移動・追加・削除できますが、それでもお奨めできません。
    some_method(
                 size,
                 count,
                 color,
               )

    # 悪い例
    some_method(size, count, color, )

    # 良い例
    some_method(size, count, color)
    ```

* メソッドの引数に初期値を割り当てるとき、
  `=`演算子の周りにはスペースを入れましょう。

    ```Ruby
    # 悪い例
    def some_method(arg1=:default, arg2=nil, arg3=[])
      # do something...
    end

    # 良い例
    def some_method(arg1 = :default, arg2 = nil, arg3 = [])
      # do something...
    end
    ```

    いくつかのRuby本は最初のスタイルを提案しているけど、
    ２つ目の方が、実用的により優れています
    (そして、ほぼ間違いなく少し読みやすいです)。

* 不要な`\`を用いた行の継続は避けましょう。
  実際、文字列連結以外での行の継続は避けましょう。

    ```Ruby
    # 悪い例
    result = 1 - \
             2

    # 良い例 (しかしそれでも地獄のように醜い)
    result = 1 \
             - 2

    long_string = 'First part of the long string' \
                  ' and second part of the long string'
    ```

* メソッドチェーンを他の行につなげるときは、`.`は次の行に置きましょう。

    ```Ruby
    # 悪い例 - ２行目を理解するのに１行目を調べなければなりません
    one.two.three.
      four

    # 良い例 - ２行目で何が行われているかすぐに理解できます
    one.two.three
      .four
    ```

* メソッド呼び出しが複数行に及ぶときは、引数は揃えましょう。
  １行の長さの制約のために、引数を揃えるのに適していない時は、
  最初の引数以降をインデント１つ分で揃えるスタイルも許容できます。

    ```Ruby
    # 初期値 (１行がとても長いです)
    def send_mail(source)
      Mailer.deliver(to: 'bob@example.com', from: 'us@example.com', subject: 'Important message', body: source.text)
    end

    # 悪い例 (インデント２つで揃えています)
    def send_mail(source)
      Mailer.deliver(
          to: 'bob@example.com',
          from: 'us@example.com',
          subject: 'Important message',
          body: source.text)
    end

    # 良い例
    def send_mail(source)
      Mailer.deliver(to: 'bob@example.com',
                     from: 'us@example.com',
                     subject: 'Important message',
                     body: source.text)
    end

    # 良い例 (普通のインデントです)
    def send_mail(source)
      Mailer.deliver(
        to: 'bob@example.com',
        from: 'us@example.com',
        subject: 'Important message',
        body: source.text
      )
    end
    ```

* 複数行に及ぶ配列は、要素を揃えましょう。

    ```Ruby
    # 悪い例 - インデント１つです
    menu_item = ["Spam", "Spam", "Spam", "Spam", "Spam", "Spam", "Spam", "Spam",
      "Baked beans", "Spam", "Spam", "Spam", "Spam", "Spam"]

    # 良い例
    menu_item = [
      "Spam", "Spam", "Spam", "Spam", "Spam", "Spam", "Spam", "Spam",
      "Baked beans", "Spam", "Spam", "Spam", "Spam", "Spam"
    ]

    # 良い例
    menu_item =
      ["Spam", "Spam", "Spam", "Spam", "Spam", "Spam", "Spam", "Spam",
       "Baked beans", "Spam", "Spam", "Spam", "Spam", "Spam"]
    ```

* 可読性のため、大きな数値にはアンダースコアをつけましょう。

    ```Ruby
    # 悪い例 - 0はいくつありますか？
    num = 1000000

    # 良い例 - 人の頭でもより簡単に解析できます
    num = 1_000_000
    ```

* APIのドキュメントのため、RDocの規約に従いましょう。
  コメント行と`def`の間に空行を入れてはいけません。
* １行は80字までにしましょう。
* 行末のスペースは避けましょう。
* ブロックコメントは使ってはいけません。
  前にスペースが入ると機能しませんし、
  通常のコメントと違い、簡単に見分けが付きません。

    ```Ruby
    # 悪い例
    == begin
    comment line
    another comment line
    == end

    # 良い例
    # comment line
    # another comment line
    ```

## 構文

* `::`は、定数(クラスやモジュールも含みます)や
  コンストラクタ(例えば`Array()`や`Nokogiri::HTML()`)を参照するときにのみ使いましょう。
  通常のメソッド呼び出しでは`::`の使用は避けましょう。

    ```Ruby
    # 悪い例
    SomeClass::some_method
    some_object::some_method

    # 良い例
    SomeClass.some_method
    some_object.some_method
    SomeModule::SomeClass::SOME_CONST
    SomeModule::SomeClass()
    ```

* 引数があるとき、`def`は`()`と共に使いましょう。
  引数がない場合は`()`は除きましょう。

     ```Ruby
     # 悪い例
     def some_method()
       # body omitted
     end

     # 良い例
     def some_method
       # body omitted
     end

     # 悪い例
     def some_method_with_arguments arg1, arg2
       # body omitted
     end

     # 良い例
     def some_method_with_arguments(arg1, arg2)
       # body omitted
     end
     ```

* あなたが使ってはならない理由を正確に知っていなければ、決して`for`を使ってはいけません。
  代わりにイテレータが使われるべきです。
  `for`は`each`の観点で実装されています(だから、あなた方は遠回りでも使っています)が、
  `for`は(`each`と違い)新しいスコープを導入せず、
  そのブロック内で定義された変数は、ブロックの外からも見えるようになってしまいます。

    ```Ruby
    arr = [1, 2, 3]

    # 悪い例
    for elem in arr do
      puts elem
    end

    # elemはルーブの外からも参照できることに注意しましょう
    elem #=> 3

    # 良い例
    arr.each { |elem| puts elem }

    # elemはeachブロックの外からは参照できません
    elem #=> NameError: undefined local variable or method `elem'
    ```

* `then`は複数行にまたがる`if/unless`では使ってはいけません。

    ```Ruby
    # 悪い例
    if some_condition then
      # 本文省略
    end

    # 良い例
    if some_condition
      # 本文省略
    end
    ```

* 複数行にまたがる`if/unless`では、条件式は常に`if/unless`と同じ行に置きましょう。

    ```Ruby
    # 悪い例
    if
      some_condition
      do_something
      do_something_else
    end

    # 良い例
    if some_condition
      do_something
      do_something_else
    end
    ```

* `if/then/else/end`構文よりも三項演算子(`?:`)を好みます。
  そちらの方がより明快で簡潔です。

    ```Ruby
    # 悪い例
    result = if some_condition then something else something_else end

    # 良い例
    result = some_condition ? something : something_else
    ```

* 三項演算子は１つの式につき１つまでにしましょう。
  つまり、三項演算子はネストしてはいけません。
  このケースでは`if/else`の方がよいです。

    ```Ruby
    # 悪い例
    some_condition ? (nested_condition ? nested_something : nested_something_else) : something_else

    # 良い例
    if some_condition
      nested_condition ? nested_something : nested_something_else
    else
      something_else
    end
    ```

* `if x: ...`は使ってはいけません - Ruby 1.9現在は廃止されました。
  代わりに三項演算子を使いましょう。

    ```Ruby
    # 悪い例
    result = if some_condition: something else something_else end

    # 良い例
    result = some_condition ? something : something_else
    ```

* `if x; ...`を使ってはいけません。代わりに三項演算子を使いましょう。

* １行の`case`文では`when x then ...`を使いましょう。
  代わりの表現である`when x: ...`は、Ruby 1.9で廃止されました。

* `when x; ...`を使ってはいけません。前のルールを見てください。

* `not`の代わりに`!`を使いましょう。

    ```Ruby
    # 悪い例 - 評価順のため、()が必要になります
    x = (not something)

    # 良い例
    x = !something
    ```

* `!!`は避けましょう。

    ```Ruby
    # 悪い例
    x = 'test'
    # obscure nil check
    if !!x
      # body omitted
    end

    x = false
    # 二重否定はbooleanとして役に立ちません。
    !!x # => false

    # 良い例
    x = 'test'
    unless x.nil?
      # body omitted
    end
    ```

* `and`と`or`の使用は禁止です。それらにその価値はありません。
   常に、代わりに`&&`と`||`を使いましょう。

    ```Ruby
    # 悪い例
    # boolean式
    if some_condition and some_other_condition
      do_something
    end

    # 制御構文
    document.saved? or document.save!

    # good
    # boolean式
    if some_condition && some_other_condition
      do_something
    end

    # 制御構文
    document.saved? || document.save!
    ```

* 複数行にまたがる三項演算子`?:`は避けましょう; 代わりに`if/unless`を使いましょう。

* 本文が１行のときは、`if/unless`はガード節にするのが好まれます。
  他の良い代替案としては`&&/||`を使った制御構文があります。

    ```Ruby
    # 悪い例
    if some_condition
      do_something
    end

    # 良い例
    do_something if some_condition

    # もう１つの良い例
    some_condition && do_something
    ```

* 否定形のときは`if`より`unless`が好まれます。(もしくは`||`構文を使いましょう)。

    ```Ruby
    # 悪い例
    do_something if !some_condition

    # 悪い例
    do_something if not some_condition

    # 良い例
    do_something unless some_condition

    # もう１つの良い例
    some_condition || do_something
    ```

* `unless`を`else`付きで使ってはいけません。
  肯定条件を先にして書き換えましょう。

    ```Ruby
    # 悪い例
    unless success?
      puts 'failure'
    else
      puts 'success'
    end

    # 良い例
    if success?
      puts 'success'
    else
      puts 'failure'
    end
    ```

* `if/unless/while/until`構文では`()`の使用は避けましょう.

    ```Ruby
    # 悪い例
    if (x > 10)
      # body omitted
    end

    # 良い例
    if x > 10
      # body omitted
    end
    ```

* 複数行の`while/until`では、`while/until condition do`を使ってはいけません。

    ```Ruby
    # 悪い例
    while x > 5 do
      # 本文省略
    end

    until x > 5 do
      # 本文省略
    end

    # 良い例
    while x > 5
      # 本文省略
    end

    until x > 5
      # 本文省略
    end
    ```

* 本文が１行のときは、`while/until`はガード節にしましょう。

    ```Ruby
    # 悪い例
    while some_condition
      do_something
    end

    # 良い例
    do_something while some_condition
    ```

* 否定形のときは、`while`よりも`until`の方が好まれます。

    ```Ruby
    # 悪い例
    do_something while !some_condition

    # 良い例
    do_something until some_condition
    ```

* 後判定ループの場合、`begin/end/until`や`begin/end/while`より、`break`付きの`Kernel#loop`が好まれます。

   ```Ruby
   # 悪い例
   begin
     puts val
     val += 1
   end while val < 0

   # 良い例
   loop do
     puts val
     val += 1
     break unless val < 0
   end
   ```

* 内部DSL(例えばRake,Rails,RSpecなど)、
  Ruby内で"キーワード"となるステータスを持ったメソッド(例えば`attr_reader` や`puts`など)や
  アトリビュートにアクセスするメソッドでは、
  引数の周りの`()`を省略しましょう。
  それ以外のメソッドでは、メソッド呼び出しの時に`()`を付けましょう。

    ```Ruby
    class Person
      attr_reader :name, :age

      # 省略
    end

    temperance = Person.new('Temperance', 30)
    temperance.name

    puts temperance.age

    x = Math.sin(y)
    array.delete(e)

    bowling.score.should == 0
    ```

* 暗黙のオプションハッシュの外側の`{}`は省略しましょう。

    ```Ruby
    # 悪い例
    user.set({ name: 'John', age: 45, permissions: { read: true } })

    # 良い例
    user.set(name: 'John', age: 45, permissions: { read: true })
    ```

* 内部DSLの一部として使われるメソッドの引数では、外側の`()`、`{}`は省略しましょう

    ```Ruby
    class Person < ActiveRecord::Base
      # 悪い例
      validates(:name, { presence: true, length: { within: 1..10 } })

      # 良い例
      validates :name, presence: true, length: { within: 1..10 }
    end
    ```

* 引数のないメソッド呼び出しの`()`は省略しましょう。

    ```Ruby
    # 悪い例
    Kernel.exit!()
    2.even?()
    fork()
    'test'.upcase()

    # 良い例
    Kernel.exit!
    2.even?
    fork
    'test'.upcase
    ```

* １行のブロックでは`do...end`より`{...}`の方が好まれます。
  複数行のブロックでは`{...}`は避けましょう
  (複数行のメソッドチェーンは常に醜いです)。
  "制御構文"や"メソッド定義"では常に`do...end`を使いましょう
  (例えばRakefilesや特定のDSLなど)
  メソッドチェーンでの`do...end`は避けましょう。

    ```Ruby
    names = ['Bozhidar', 'Steve', 'Sarah']

    # 悪い例
    names.each do |name|
      puts name
    end

    # 良い例
    names.each { |name| puts name }

    # 悪い例
    names.select do |name|
      name.start_with?('S')
    end.map { |name| name.upcase }

    # 良い例
    names.select { |name| name.start_with?('S') }.map { |name| name.upcase }
    ```

    `{...}`を用いた複数行のメソッドチェーンをOKと主張する人もいるかもしれないが、
    自問してみてほしい - このコードは本当に読みやすいだろうか？
    また、このブロックの本文は素早く展開できるだろうか？

* 単に他のブロックに引数を渡すだけのブロックリテラルを避けるため、
  ブロック引数を明示することを検討しましょう。
  ただしブロックが`Proc`に変換されることでのパフォーマンスに気をつけましょう。

    ```Ruby
    require 'tempfile'

    # 悪い例
    def with_tmp_dir
      Dir.mktmpdir do |tmp_dir|
        Dir.chdir(tmp_dir) { |dir| yield dir }  # block just passes arguments
      end
    end

    # 良い例
    def with_tmp_dir(&block)
      Dir.mktmpdir do |tmp_dir|
        Dir.chdir(tmp_dir, &block)
      end
    end

    with_tmp_dir do |dir|
      puts "dir is accessible as parameter and pwd is set: #{dir}"
    end
    ```

* 制御構文上不要な`return`は避けましょう。

    ```Ruby
    # 悪い例
    def some_method(some_arr)
      return some_arr.size
    end

    # 良い例
    def some_method(some_arr)
      some_arr.size
    end
    ```

* 不要な`self`は避けましょう (自身のアトリビュートへの書き込みでのみ必要です)。

    ```Ruby
    # 悪い例
    def ready?
      if self.last_reviewed_at > self.last_updated_at
        self.worker.update(self.content, self.options)
        self.status = :in_progress
      end
      self.status == :verified
    end

    # 良い例
    def ready?
      if last_reviewed_at > last_updated_at
        worker.update(content, options)
        self.status = :in_progress
      end
      status == :verified
    end
    ```

* 当然の帰結として、ローカル変数でメソッドを隠すのは、
  それらが等価なものでない限り避けましょう。

    ```Ruby
    class Foo
      attr_accessor :options

      # ok
      def initialize(options)
        self.options = options
        # both options and self.options are equivalent here
      end

      # 悪い例
      def do_something(options = {})
        unless options[:when] == :later
          output(self.options[:message])
        end
      end

      # 良い例
      def do_something(params = {})
        unless params[:when] == :later
          output(options[:message])
        end
      end
    end
    ```

* 代入部分を`()`で囲まずに、`=`の返り値を条件式に用いてはいけません。
  これは、Rubyistの中では *条件式内での安全な代入* としてとても有名です。

    ```Ruby
    # 悪い例 (+ 警告が出ます)
    if v = array.grep(/foo/)
      do_something(v)
      ...
    end

    # 良い例 (MRIはこれでも文句を言いますが、RuboCopでは問題ありません)
    if (v = array.grep(/foo/))
      do_something(v)
      ...
    end

    # 良い例
    v = array.grep(/foo/)
    if v
      do_something(v)
      ...
    end
    ```

* 変数の初期化には、`||=`を自由に使いましょう。

    ```Ruby
    # nameがnilかfalseでなければ、Bozhidarで初期化します
    name ||= 'Bozhidar'
    ```

* boolean変数には`||=`を用いてはいけません
  (現在の値が`false`であったときに何が起こるか考えてみましょう)。

    ```Ruby
    # 悪い例 - たとえenabledがfalseでもtrueが入ります
    enabled ||= true

    # 良い例
    enabled = true if enabled.nil?
    ```

* 値が入っているかわからない変数の前処理のは`&&=`を用いましょう。
  `&&=`を使えば変数が存在するときのみ値を変更するので、
  存在確認に用いている不要な`if`を除去できます。

    ```Ruby
    # 悪い例
    if something
      something = something.downcase
    end

    # ok
    something = something.downcase if something

    # 良い例
    something = something && something.downcase

    # より良い例
    something &&= something.downcase
    ```

* 等価演算子`===`の露骨な使用は避けましょう。
  その名が示す通り、`case`の条件判定で用いられており、
  その外で用いられると混乱のもとになります。

    ```Ruby
    # 悪い例
    Array === something
    (1..100) === 7
    /something/ === some_string

    # 良い例
    something.is_a?(Array)
    (1..100).include?(7)
    some_string =~ /something/
    ```

* Perlスタイルの(`$:`や`$;`などのような)特別な変数の使用は避けましょう。
  それらは極めて不可解で、
  １行のスクリプト以外でそれらが使われるとやる気が削がれます。
  `English`ライブラリから提供される人にやさしいエイリアスを用いましょう。

    ```Ruby
    # 悪い例
    $:.unshift File.dirname(__FILE__)

    # 良い例
    require 'English'
    $LOAD_PATH.unshift File.dirname(__FILE__)
    ```

* メソッド名と引数の始まりの`(`の間にスペースを入れてはいけません。

    ```Ruby
    # 悪い例
    f (3 + 2) + 1

    # 良い例
    f(3 + 2) + 1
    ```

* メソッドの最初の引数が`(`で始まるならば、
  常にメソッド呼び出しに`()`を用いましょう。
  例えば次のように書きます
`f((3 + 2) + 1)`。

* Rubyインタープリタを走らせるときは、常に`-w`オプションを付けましょう。
  これまでのルールのどれかを忘れてしまった時に警告を出してくれます！

* １行の本文を持つラムダには新しいリテラルを持ちましょう。
  `lambda`は複数行にまたがるときに使いましょう。

    ```Ruby
    # 悪い例
    l = lambda { |a, b| a + b }
    l.call(1, 2)

    # 正しい例、ですがギクシャクしています
    l = ->(a, b) do
      tmp = a * 7
      tmp * b / 50
    end

    # 良い例
    l = ->(a, b) { a + b }
    l.call(1, 2)

    l = lambda do |a, b|
      tmp = a * 7
      tmp * b / 50
    end
    ```

* `Proc.new`より`proc`を好みます。

    ```Ruby
    # 悪い例
    p = Proc.new { |n| puts n }

    # 良い例
    p = proc { |n| puts n }
    ```

* ラムダやprocの呼び出しには`proc[]`や`proc.()`より`proc.call()`を好みます。

    ```Ruby
    # 悪い例 - 列挙型のアクセスに似ているように見えます
    l = ->(v) { puts v }
    l[1]

    # こちらも悪い例 - 珍しい構文です
    l = ->(v) { puts v }
    l.(1)

    # 良い例
    l = ->(v) { puts v }
    l.call(1)
    ```

* 使わないブロック引数には`_`を用いましょう。

    ```Ruby
    # bad
    result = hash.map { |k, v| v + 1 }

    # good
    result = hash.map { |_, v| v + 1 }
    ```

* `STDOUT/STDERR/STDIN`の代わりに`$stdout/$stderr/$stdin`を用いましょう。
  `STDOUT/STDERR/STDIN`は定数であり、
  Rubyでの定数は、実際は再割当てできますが(他のストリームへのリダイレクトも可能)、
  もし再割当てするとインタープリタからの警告が出るでしょう。

* `$stderr.puts`の代わりに`warn`を用いましょう。
  簡潔さや明快さはさておき、
  `warn`は必要であれば警告を抑制することができます
  (警告レベルを`-W0`を用いて0に設定することによって実現できます)。

* 不可解な`String#%`メソッドより`sprintf`や`format`を好みます。

    ```Ruby
    # 悪い例
    '%d %d' % [20, 10]
    # => '20 10'

    # 良い例
    sprintf('%d %d', 20, 10)
    # => '20 10'

    # 良い例
    sprintf('%{first} %{second}', first: 20, second: 10)
    # => '20 10'

    format('%d %d', 20, 10)
    # => '20 10'

    # 良い例
    format('%{first} %{second}', first: 20, second: 10)
    # => '20 10'
    ```

* 不可解な`Array#*`メソッドよりも`Array#join`を好みます。

    ```Ruby
    # 悪い例
    %w(one two three) * ', '
    # => 'one, two, three'

    # 良い例
    %w(one two three).join(', ')
    # => 'one, two, three'
    ```

* 引数が配列かどうかわからないが、それを配列として扱って処理したいとき、
  配列のチェックを明示するより、`[*var]`や`Array()`を代わりに使いましょう。

    ```Ruby
    # 悪い例
    paths = [paths] unless paths.is_a? Array
    paths.each { |path| do_something(path) }

    # 良い例
    [*paths].each { |path| do_something(path) }

    # 良い例 (そして少し読みやすいです)
    Array(paths).each { |path| do_something(path) }
    ```

* 複雑な比較ロジックの代わりに、
  可能な限り`Range`や`Comparable#between?`を用いましょう。

    ```Ruby
    # 悪い例
    do_something if x >= 1000 && x <= 2000

    # 良い例
    do_something if (1000..2000).include?(x)

    # 良い例
    do_something if x.between?(1000, 2000)
    ```

* `==`を明示した比較よりも判定メソッドを用いましょう。
  数値の比較はOKです。

    ```Ruby
    # 悪い例
    if x % 2 == 0
    end

    if x % 2 == 1
    end

    if x == nil
    end

    # 良い例
    if x.even?
    end

    if x.odd?
    end

    if x.nil?
    end

    if x.zero?
    end

    if x == 0
    end
    ```

* `BEGIN`ブロックの使用は避けましょう。

* `END`ブロックを使ってはいけません。代わりに`Kernel#at_exit`を使いましょう。

    ```ruby
    # 悪い例

    END { puts 'Goodbye!' }

    # 良い例

    at_exit { puts 'Goodbye!' }
    ```

* フリップフロップの使用は避けましょう。

* 制御構文で条件式のネストは避けましょう。
  不正なデータをアサートするにはガード節を好みます。
  ガード節は、可能な限り関数から出ていくために、
  関数の先頭付近で宣言される条件式です。

    ```Ruby
    # 悪い例
      def compute_thing(thing)
        if thing[:foo]
          update_with_bar(thing)
          if thing[:foo][:bar]
            partial_compute(thing)
          else
            re_compute(thing)
          end
        end
      end

    # 良い例
      def compute_thing(thing)
        return unless thing[:foo]
        update_with_bar(thing[:foo])
        return re_compute(thing) unless thing[:foo][:bar]
        partial_compute(thing)
      end
    ```

## 命名規則

> プログラミングでただひとつ難しいことは、キャッシュの無効化と命名である。 <br/>
> -- Phil Karlton

* 識別子は英語で名づけましょう。

    ```Ruby
    # 悪い例 - 識別子がnon-asciiな文字列です
    заплата = 1_000

    # 悪い例 - (キリル文字の代わりに)ラテン文字で書かれてはいますが、識別子がブルガリア語です
    zaplata = 1_000

    # 良い例
    salary = 1_000
    ```

* シンボル、メソッド、変数には`snake_case`を用いましょう。

    ```Ruby
    # 悪い例
    :'some symbol'
    :SomeSymbol
    :someSymbol

    someVar = 5

    def someMethod
      ...
    end

    def SomeMethod
     ...
    end

    # 良い例
    :some_symbol

    def some_method
      ...
    end
    ```

* クラスやモジュールには`CamelCase`を用いましょう。(HTTP, RFC, XMLのような頭字語は大文字を保ちましょう)。

    ```Ruby
    # 悪い例
    class Someclass
      ...
    end

    class Some_Class
      ...
    end

    class SomeXml
      ...
    end

    # 良い例
    class SomeClass
      ...
    end

    class SomeXML
      ...
    end
    ```

* 他の定数は`SCREAMING_SNAKE_CASE`を用いましょう。

    ```Ruby
    # 悪い例
    SomeConst = 5

    # 良い例
    SOME_CONST = 5
    ```

* 条件判定メソッド(boolean値が返る)には`?`を末尾に付けましょう
  (すなわり`Array#empty?`のように)。
  メソッドがboolean値を返さなければ、末尾に`?`を付けてはいけません。
* *危険* な可能性のあるメソッド
  (すなわち`self`のアトリビュートに変更が加えられるものや、
  `exit!`(`exit`と違ってファイナライザが走らない)のようなもの)
  は、 *危険* であることを示すため、
  末尾に`!`を付けましょう。

    ```Ruby
    # 悪い例 - '安全'なメソッドです
    class Person
      def update!
      end
    end

    # 良い例
    class Person
      def update
      end
    end

    # 良い例
    class Person
      def update!
      end

      def update
      end
    end
    ```

* 可能な限り、危険なメソッドの観点から安全なメソッドを定義しましょう。

    ```Ruby
    class Array
      def flatten_once!
        res = []

        each do |e|
          [*e].each { |f| res << f }
        end

        replace(res)
      end

      def flatten_once
        dup.flatten_once!
      end
    end
    ```

* 短いブロックと共に`reduce`を使うとき、引数は`|a, e|`と名づけましょう。
  (accumulator, element).
* バイナリ演算子を定義するとき、引数は`other`を用いましょう
  (`<<`と`[]`は意味が違ってくるので、このルールの例外です)。

    ```Ruby
    def +(other)
      # body omitted
    end
    ```

* `collect`より`map`、`detect`より`find`、`find_all`より`select`
  `inject`より`reduce`、`length`より`size`を好みます。
  これは厳しい要件ではありません;
  もしエイリアスを用いるほうが可読性が上がるのであれば、
  使うのもOKです。
  それらの同韻のメソッドはSmalltalkから継承されており、
  他の言語ではあまり一般的ではありません。
  `find_all`よりも`select`が推奨される理由は、
  `reject`と共に用いた時、その名前が極めて自己説明的だからです。

* `map`と`flatten`の組み合わせの代わりに、`flat_map`を用いましょう。
  これは深さが２以上の配列には適用できません。
  すなわち、`users.first.songs == ['a', ['b','c']]`のときは、
  `flat_map`より`map + flatten`を用いましょう。
  `flatten`は配列を全て平坦にするのに対し、`flat_map`は配列を１次元だけ平坦にします。

    ```Ruby
    # 悪い例
    all_songs = users.map(&:songs).flatten.uniq

    # 良い例
    all_songs = users.flat_map(&:songs).uniq
    ```

* `reverse.each`の代わりに`reverse_each`を用いましょう。
  `reverse_each`は新しい配列を作らないので、それが利点です。

    ```Ruby
    # 悪い例
    array.reverse.each { ... }

    # 良い例
    array.reverse_each { ... }
    ```

## コメント

> 良いコードは素晴らしいドキュメントを持っています。
> あなたがまさにコードにコメントを追加しようとしている時、
> 自問してほしい、"どのようにコードを改善すれば、このコメントが不要になるだろうか？"
> コードを改善してドキュメントをより明快にしましょう。
> -- Steve McConnell

* コードそのものがドキュメントになるような説明的なコードを書いて、このセクションの残りのパートは無視しましょう。本当に！
* コメントは英語で書きましょう。
* 最初の`#`とコメントの間にスペースを１つ入れましょう。
* １語より長いコメントを活用し、句読点を使いましょう。
  ピリオドの後に[one space](http://en.wikipedia.org/wiki/Sentence_spacing)を使いましょう。
* 余計なコメントは避けましょう。

    ```Ruby
    # 悪い例
    counter += 1 # Increments counter by one.
    ```

* コメントは最新に保ちましょう。
  古くなったコメントは、コメントがないより悪いです。

> 良いコードは良いジョークのようだ - なんの説明もいらない。<br/>
> -- Russ Olsen

* 悪いコードを説明するコメントは避けましょう。
  自己説明的なコードへのリファクタリングを行いましょう
  (やるかやらないか - "やってみる"はなしだ。 --Yoda)。

### 注釈

* 注釈は、通常関連するコードのすぐ上に書きましょう。
* 注釈のキーワードの後ろは`: `を続けましょう。
  その後ろに問題点を書きましょう。
* もし問題点の記述に複数行かかる場合は、
  後続の行は`#`の後ろにスペース２つでインデントしましょう。

    ```Ruby
    def bar
      # FIXME: This has crashed occasionally since v3.2.1. It may
      #   be related to the BarBazUtil upgrade.
      baz(:quux)
    end
    ```

* もし問題が明らかで、記述が冗長な場合は、
  問題のある行の末尾に、本文なしの注釈だけ付けましょう。
  この用法は例外であり、ルールではありません。

    ```Ruby
    def bar
      sleep 100 # OPTIMIZE
    end
    ```

* あとで追加されるべき、今はない機能や関数を書き留めるには`TODO`を使いましょう。
* 直す必要がある壊れたコードを書き留めるには`FIXME`を使いましょう。
* パフォーマンスに問題を及ぼすような、遅い、または非効率なコードを書き留めるには`OPTIMIZE`を使いましょう。
* 疑わしくリファクタリングで除去すべきコードの匂いを書き留めるには`HACK`を使いましょう。
* 意図したとおりに動くか確認する必要がある箇所を書き留めるには`REVIEW`を使いましょう。
  例: `REVIEW: Are we sure this is how the client does X currently?`
* 適切に感じるのであれば、他の独自のキーワードを用いても構いませんが、
  それらのキーワードは`README`やそれに類するものに書いておきましょう。

## クラス

* クラス定義は置いて一貫性のある構造にしましょう。

    ```Ruby
    class Person
      # extend や include を最初に行います
      extend SomeModule
      include AnotherModule

      # 定数定義はその次です
      SOME_CONSTANT = 20

      # その後ろはアトリビュートマクロです
      attr_reader :name

      # 他のマクロが続きます(もしあれば)
      validates :name

      # public class methods が次に来ます
      def self.some_method
      end

      # public instance methods が続きます
      def some_method
      end

      # protected and private methods は後ろの方にまとめます
      protected

      def some_protected_method
      end

      private

      def some_private_method
      end
    end
    ```

* クラスメソッドしかないクラスはモジュールであることが好まれます。
  クラスはインスタンスを生成することにのみ意味があります。

    ```Ruby
    # 悪い例
    class SomeClass
      def self.some_method
        # body omitted
      end

      def self.some_other_method
      end
    end

    # 良い例
    module SomeClass
      module_function

      def some_method
        # body omitted
      end

      def some_other_method
      end
    end
    ```

* モジュールのインスタンスメソッドをクラスメソッドにしたいときは、
  `extend self`よりも`module_function`が好まれます。

    ```Ruby
    # 悪い例
    module Utilities
      extend self

      def parse_something(string)
        # do stuff here
      end

      def other_utility_method(number, string)
        # do some more stuff
      end
    end

    # 良い例
    module Utilities
      module_function

      def parse_something(string)
        # do stuff here
      end

      def other_utility_method(number, string)
        # do some more stuff
      end
    end
    ```

* クラス階層の設計を行うときは、
  [リスコフの置換原則](http://ja.wikipedia.org/wiki/%E3%83%AA%E3%82%B9%E3%82%B3%E3%83%95%E3%81%AE%E7%BD%AE%E6%8F%9B%E5%8E%9F%E5%89%87).
  に従いましょう。
* あなたのクラスを可能な限り
  [SOLID](http://en.wikipedia.org/wiki/SOLID_(object-oriented_design\))
  に保ちましょう。
* クラスの領分を説明するため、常に`to_s`メソッドを提供しましょう。

    ```Ruby
    class Person
      attr_reader :first_name, :last_name

      def initialize(first_name, last_name)
        @first_name = first_name
        @last_name = last_name
      end

      def to_s
        "#{@first_name} #{@last_name}"
      end
    end
    ```

* 単純なアクセサやミューテータの定義には、`attr`群を用いましょう。

    ```Ruby
    # 悪い例
    class Person
      def initialize(first_name, last_name)
        @first_name = first_name
        @last_name = last_name
      end

      def first_name
        @first_name
      end

      def last_name
        @last_name
      end
    end

    # 良い例
    class Person
      attr_reader :first_name, :last_name

      def initialize(first_name, last_name)
        @first_name = first_name
        @last_name = last_name
      end
    end
    ```

* `attr`の使用は避けましょう。代わりに`attr_reader`や`attr_accessor`を使いましょう。

    ```Ruby
    # 悪い例 - １つのアクセサしか作れません(1.9で廃止されました)
    attr :something, true
    attr :one, :two, :three # attr_readerと同じです

    # 良い例
    attr_accessor :something
    attr_reader :one, :two, :three
    ```

* `Struct.new`の使用を考えましょう、
  それは、単純なアクセサ、コンストラクタや比較演算子を定義してくれます。

    ```Ruby
    # 良い例
    class Person
      attr_accessor :first_name, :last_name

      def initialize(first_name, last_name)
        @first_name = first_name
        @last_name = last_name
      end
    end

    # より良い例
    Person = Struct.new(:first_name, :last_name) do
    end
    ````

* `Struct.new`を拡張してはいけません - それは既に新しいクラスです。
  それは余分なクラスレベルをもたらし、
  複数回`require`された時に、奇妙なエラーの原因にもなります。

* あるクラスのインスタンス生成する追加の方法を提供したいときは、
  ファクトリメソッドの追加を検討しましょう。

    ```Ruby
    class Person
      def self.create(options_hash)
        # body omitted
      end
    end
    ```

* 継承より[ダック・タイピング](http://ja.wikipedia.org/wiki/%E3%83%80%E3%83%83%E3%82%AF%E3%83%BB%E3%82%BF%E3%82%A4%E3%83%94%E3%83%B3%E3%82%B0)が好まれます。

    ```Ruby
    # 悪い例
    class Animal
      # abstract method
      def speak
      end
    end

    # 継承
    class Duck < Animal
      def speak
        puts 'Quack! Quack'
      end
    end

    # 継承
    class Dog < Animal
      def speak
        puts 'Bau! Bau!'
      end
    end

    # 良い例
    class Duck
      def speak
        puts 'Quack! Quack'
      end
    end

    class Dog
      def speak
        puts 'Bau! Bau!'
      end
    end
    ```

* 継承での振る舞いが"扱いづらい"ので、クラス変数(`@@`)の使用は避けましょう。

    ```Ruby
    class Parent
      @@class_var = 'parent'

      def self.print_class_var
        puts @@class_var
      end
    end

    class Child < Parent
      @@class_var = 'child'
    end

    Parent.print_class_var # => will print "child"
    ```

    クラス階層内の全てのクラスを見ることができるように、
    実際にクラス変数を１つ共有してみましょう。
    クラスインスタンス変数はクラス変数より好まれます。

* 意図した使い方に沿って、可視性(`private`、`protected`)を設定しましょう。
  全てを`public`(デフォルトの設定)のままにしないようにしましょう。
  結局私達は今 *Ruby* を書いているのだから。 *Python* ではなく。
* `public`、`protected`、`private`は、適用するメソッド定義と同じインデントにしましょう。
  可視性を定義する識別子以降のメソッドに適用されることを強調するため、
  識別子の上下に空行を入れましょう。

    ```Ruby
    class SomeClass
      def public_method
        # ...
      end

      private

      def private_method
        # ...
      end

      def another_private_method
        # ...
      end
    end
    ```

* シングルトンメソッドを定義するときは`def self.method`を用いましょう。
  クラス名を繰り返さないので、簡単にリファクタリングできるようになります。

    ```Ruby
    class TestClass
      # 悪い例
      def TestClass.some_method
        # body omitted
      end

      # 良い例
      def self.some_other_method
        # body omitted
      end

      # たくさんのシングルトンメソッドを定義しなければならない時
      # この書き方も便利で、許容できます。
      class << self
        def first_method
          # body omitted
        end

        def second_method_etc
          # body omitted
        end
      end
    end
    ```

## 例外

* 例外発生には`fail`を用いましょう。
  `raise`は例外をキャッチして、再度発生させるときにのみ使いましょう
  (何故なら、ここでは落ちるのではなく、明示的に目的を持って例外を発生させているからです)。

    ```Ruby
    begin
      fail 'Oops'
    rescue => error
      raise if error.message != 'Oops'
    end
    ```

* ２引数の`fail/raise`では、`RuntimeError`を明示しないようにしましょう。

    ```Ruby
    # 悪い例
    fail RuntimeError, 'message'

    # 良い例 - デフォルトでRuntimeErrorが発生します
    fail 'message'
    ```

* 例外インスタンスの代わりに、
  例外クラスとメッセージが分かれている`fail/raise`が好まれます。

    ```Ruby
    # 悪い例
    fail SomeException.new('message')
    # `fail SomeException.new('message'), backtrace`とする書き方が存在しないことに注意しましょう。

    # 良い例
    fail SomeException, 'message'
    # `fail SomeException, 'message', backtrace`の用法と一貫性があります
    ```

* `ensure`ブロックから`return`してはいけません。
  もし`ensure`から明示的に値を返したい場合は、
  `return`はどの例外発生よりも前に書いておき、
  例外など発生していなかったかのように値を返しましょう。
  事実上、例外は静かに捨てられます。

    ```Ruby
    def foo
      begin
        fail
      ensure
        return 'very bad idea'
      end
    end
    ```

* 可能な場所では、 *暗黙のbeginブロック* を用いましょう。

    ```Ruby
    # 悪い例
    def foo
      begin
        # main logic goes here
      rescue
        # failure handling goes here
      end
    end

    # 良い例
    def foo
      # main logic goes here
    rescue
      # failure handling goes here
    end
    ```

* *不確実性のあるメソッド*(Avdi Grimmによって作られた言葉です)
  を用いて`begin`の蔓延を和らげましょう。

    ```Ruby
    # 悪い例
    begin
      something_that_might_fail
    rescue IOError
      # handle IOError
    end

    begin
      something_else_that_might_fail
    rescue IOError
      # handle IOError
    end

    # 良い例
    def with_io_error_handling
       yield
    rescue IOError
      # handle IOError
    end

    with_io_error_handling { something_that_might_fail }

    with_io_error_handling { something_else_that_might_fail }
    ```

* 例外をもみ消してはいけません。

    ```Ruby
    # 悪い例
    begin
      # an exception occurs here
    rescue SomeError
      # the rescue clause does absolutely nothing
    end

    # 悪い例
    do_something rescue nil
    ```

* `rescue`のガード節は避けましょう。

    ```Ruby
    # 悪い例 - StandardErrorとそれを継承した全てのクラスをキャッチしてしまします
    read_file rescue handle_error($!)

    # 良い例 - Errno::ENOENTとそれを継承したクラスのみをキャッチします
    def foo
      read_file
    rescue Errno::ENOENT => ex
      handle_error(ex)
    end
    ```


* 制御フローに例外を使っては行けません。

    ```Ruby
    # 悪い例
    begin
      n / d
    rescue ZeroDivisionError
      puts 'Cannot divide by 0!'
    end

    # 良い例
    if d.zero?
      puts 'Cannot divide by 0!'
    else
      n / d
    end
    ```

* `Exception`を`rescue`するのは避けましょう。
  これは`exit`のシグナルも捕捉するため、`kill -9`が必要になります。

    ```Ruby
    # 悪い例
    begin
      # calls to exit and kill signals will be caught (except kill -9)
      exit
    rescue Exception
      puts "you didn't really want to exit, right?"
      # exception handling
    end

    # 良い例
    begin
      # a blind rescue rescues from StandardError, not Exception as many
      # programmers assume.
    rescue => e
      # exception handling
    end

    # こちらも良い例
    begin
      # an exception occurs here

    rescue StandardError => e
      # exception handling
    end

    ```

* より詳細な例外を`rescue`チェーンの上に配置しましょう。
  そうでなければ、決して`rescue`されません。

    ```Ruby
    # 悪い例
    begin
      # some code
    rescue Exception => e
      # some handling
    rescue StandardError => e
      # some handling
    end

    # 良い例
    begin
      # some code
    rescue StandardError => e
      # some handling
    rescue Exception => e
      # some handling
    end
    ```

* 外部リソースの含まれるプログラムでは、`ensure`で開放しましょう

    ```Ruby
    f = File.open('testfile')
    begin
      # .. process
    rescue
      # .. handle error
    ensure
      f.close unless f.nil?
    end
    ```

* 新しい例外クラスを導入するより、基本ライブラリの例外クラスを用いることが好まれます。

## Collections

* 配列やハッシュのリテラルの方が好まれます。
  (コンストラクタに引数を渡す場合を除けば、ということですが)

    ```Ruby
    # 悪い例
    arr = Array.new
    hash = Hash.new

    # 良い例
    arr = []
    hash = {}
    ```

* (空文字列や、文字列内にスペースが入っていない)文字列の配列構文は、
  `%w`リテラルの方が好まれます。
  このルールは要素が２つ以上の配列に適用されます。

    ```Ruby
    # 悪い例
    STATES = ['draft', 'open', 'closed']

    # 良い例
    STATES = %w(draft open closed)
    ```

* シンボルの配列が必要なときは`%i`が好まれます
  (Ruby 1.9との互換性の維持が必要で無ければ)。
  このルールは要素が２つ以上の配列に適用されます。

    ```Ruby
    # 悪い例
    STATES = [:draft, :open, :closed]

    # 良い例
    STATES = %i(draft open closed)
    ```

* `Array`や`Hash`リテラルの最後の要素の後ろの`,`は避けましょう。
  複数行にわかれていない時は特に避けましょう。

    ```Ruby
    # 悪い例 - 簡単に要素を移動・追加・削除できますが、それでも好まれません。
    VALUES = [
               1001,
               2020,
               3333,
             ]

    # 悪い例
    VALUES = [1001, 2020, 3333, ]

    # 良い例
    VALUES = [1001, 2020, 3333]
    ```

* 配列に大きな隙間を作るのは避けましょう。

    ```Ruby
    arr = []
    arr[100] = 1 # now you have an array with lots of nils
    ```

* 配列の最初や最後にアクセスしたいときは、
  `[0]`や`[-1]`より`first`や`last`が好まれます。

* 要素が一意のものを扱うときは、`Array`の代わりに`Set`を用いましょう。
  `Set`は重複がない要素が順序を持たないように実装されています。
  これは`Array`の直感的な内部操作と、`Hash`の要素発見の速さが合わさっています。
* ハッシュのキーには文字列よりシンボルが好まれます。

    ```Ruby
    # 悪い例
    hash = { 'one' => 1, 'two' => 2, 'three' => 3 }

    # 良い例
    hash = { one: 1, two: 2, three: 3 }
    ```

* 変更のできるオブジェクトをハッシュのキーに使うのは避けましょう。

* キーがシンボルの時は、ハッシュリテラルの構文を用いましょう。

    ```Ruby
    # 悪い例
    hash = { :one => 1, :two => 2, :three => 3 }

    # 良い例
    hash = { one: 1, two: 2, three: 3 }
    ```

* `Hash#has_key?`より`Hash#key?`を、
  `Hash#has_value?`より`Hash#value?`を用いましょう。
    [ここ](http://blade.nagaokaut.ac.jp/cgi-bin/scat.rb/ruby/ruby-core/43765)
  でMatzが述べているように、長い記法は廃止が検討されています。

    ```Ruby
    # 悪い例
    hash.has_key?(:test)
    hash.has_value?(value)

    # 良い例
    hash.key?(:test)
    hash.value?(value)
    ```

* 存在すべきキーを扱う時は、`Hash#fetch`を用いましょう。

    ```Ruby
    heroes = { batman: 'Bruce Wayne', superman: 'Clark Kent' }
    # 悪い例 - もし誤りがあってもすぐに気づくことができないかもしれません
    heroes[:batman] # => "Bruce Wayne"
    heroes[:supermann] # => nil

    # 良い例 - fetchはKeyErrorを投げるので、問題が明らかになります
    heroes.fetch(:supermann)
    ```

* 独自のロジックを用いないようにするため、
  `Hash#fetch`経由でデフォルト値を導入しましょう。

   ```Ruby
   batman = { name: 'Bruce Wayne', is_evil: false }

   # 悪い例 - falseと判定される値が入っていた場合、望んだとお降りに動かないかもしれません
   batman[:is_evil] || true # => true

   # 良い例 - falseと判定される値が入っていても正しく動きます
   batman.fetch(:is_evil, true) # => false
   ```

* `Hash#fetch`では、デフォルト値の代わりにブロックを用いることが好まれます。

   ```Ruby
   batman = { name: 'Bruce Wayne' }

   # 悪い例 - デフォルト値が使われると、先に評価してしまいます
   # だから、もし複数回呼ばれると、プログラムが遅くなります
   batman.fetch(:powers, get_batman_powers) # get_batman_powers は高価な呼び出しです

   # 良い例 - ブロックは後から評価されます。だから、KeyErrorが評価の引き金になります
   batman.fetch(:powers) { get_batman_powers }
   ```

* Ruby 1.9現在ではハッシュは順序付けられるということを信頼しましょう。
* コレクションを走査している時に変更を加えてわいけません。

## 文字列

* 文字列連結の代わりに文字列挿入を好みます。

    ```Ruby
    # 悪い例
    email_with_name = user.name + ' <' + user.email + '>'

    # 良い例
    email_with_name = "#{user.name} <#{user.email}>"
    ```

* 文字列挿入時にはスペースを入れることを検討しましょう。
  文字列から分かれたコードがより明確になります。

    ```Ruby
    "#{ user.last_name }, #{ user.first_name }"
    ```

* 文字列挿入の必要がないときや、`\t`や`\n`｀’｀等の特別な文字がない場合は、
  シングルクォーテーションが好まれます。

    ```Ruby
    # 悪い例
    name = "Bozhidar"

    # 良い例
    name = 'Bozhidar'
    ```

* 文字リテラル構文`?x`を用いてはいけません。
  Ruby 1.9からは基本的には冗長です -
  `?x`は`'x'`(１文字の文字列)に変換されます

    ```Ruby
    # 悪い例
    char = ?c

    # 良い例
    char = 'c'
    ```

* 文字列の中の挿入されるインスタンス変数やグローバル変数の周りの
  `{}`は省略してはいけません。

    ```Ruby
    class Person
      attr_reader :first_name, :last_name

      def initialize(first_name, last_name)
        @first_name = first_name
        @last_name = last_name
      end

      # 悪い例 - 有効ですが不格好です
      def to_s
        "#@first_name #@last_name"
      end

      # 良い例
      def to_s
        "#{@first_name} #{@last_name}"
      end
    end

    $global = 0
    # 悪い例
    puts "$global = #$global"

    # 良い例
    puts "$global = #{$global}"
    ```

* 大きなデータの塊を作る必要があるときは、`String#+`の使用は避けましょう。
  代わりに、`String#<<`を使いましょう。
  連結`String#<<`は、文字列インスタンスを直接書き換えるため、
  `String#+`よりも常に速いです、
  `String#+`はたくさんの新しいオブジェクトを作ってしまします。

    ```Ruby
    # 良く、そして速い例
    html = ''
    html << '<h1>Page title</h1>'

    paragraphs.each do |paragraph|
      html << "<p>#{paragraph}</p>"
    end
    ```

* 複数行のヒアドキュメントを用いるときは、
  先頭のスペースも保持してしまうということを頭に入れておかなければなりません。
  過剰なスペースを取り除くためのマージンを採用するのを実用的です。

    ```Ruby
    code = <<-END.gsub(/^\s+\|/, '')
      |def test
      |  some_method
      |  other_method
      |end
    END
    #=> "def test\n  some_method\n  other_method\nend\n"
    ```

## 正規表現

> 問題に突き当たった時、"そうだ、正規表現を使おう"と考えます。
> そこには２つの問題があります。<br/>
> -- Jamie Zawinski

* 単にプレーンテキストを文字列中から探すだけの時は、
  正規表現を使ってはいけません: `string['text']`を使いましょう。
* 単純化のため、文字列の添字に直接正規表現を渡しましょう。

    ```Ruby
    match = string[/regexp/]             # get content of matched regexp
    first_group = string[/text(grp)/, 1] # get content of captured group
    string[/text (grp)/, 1] = 'replace'  # string => 'text replace'
    ```

* 捕捉した結果を使う必要のないとき、捕捉しないグループを用いましょう。

    ```Ruby
    /(first|second)/   # 悪い例
    /(?:first|second)/ # 良い例
    ```

* 最後に正規表現にマッチした値を示すPerlレガシーの暗号的な変数を用いてはいけません
  (`$1`、`$2`など)。
  代わりに`Regexp.last_match[n]`を用いましょう。

    ```Ruby
    /(regexp)/ =~ string
    ...

    # 悪い例
    process $1

    # 良い例
    process Regexp.last_match[1]
    ```


* どの値が入っているか追うのが困難になるので、
  順序付けられたグループを使うのは避けましょう。
  代わりに名付けられたグループを使いましょう。

    ```Ruby
    # 悪い例
    /(regexp)/ =~ string
    ...
    process Regexp.last_match[1]

    # 良い例
    /(?<meaningful_var>regexp)/ =~ string
    ...
    process meaningful_var
    ```

* 文字クラスの中では、特別な意味を持つ文字が少ないので注意が必要です:
  `^`、`-`、`\`、`]`のみが特別な意味を持つので、
  `.`を`[]`の中でエスケープしてはいけません。

* `^`や`$`は、文字列の先頭や末尾ではなく、
  行頭や行末にマッチするので注意が必要です。
  もし文字列全体の先頭末尾にマッチさせたいときは、
  `\A`、`\z`を使いましょう
  (`\n?\z`と等価である`\Z`と混同しないようにしましょう)。

    ```Ruby
    string = "some injection\nusername"
    string[/^username$/]   # matches
    string[/\Ausername\z/] # don't match
    ```

* 複雑な正規表現には`x`識別子を用いましょう。
  これを用いることで、より読みやすくなり、
  便利なコメントを使えるようになります。
  スペースが無視されることに注意しましょう。

    ```Ruby
    regexp = %r{
      start         # some text
      \s            # white space char
      (group)       # first group
      (?:alt1|alt2) # some alternation
      end
    }x
    ```

* `sub`/`gsub`での複雑な置換は、ブロックやハッシュを用いることで実現できます。

## パーセントリテラル

* 挿入と`"`双方が入る１行の文字列には、
  `%()`(`%Q()`の短縮形)を使いましょう。
  複数行の時はヒアドキュメントを好みます。

    ```Ruby
    # 悪い例 (挿入の必要がありません)
    %(<div class="text">Some text</div>)
    # should be '<div class="text">Some text</div>'

    # 悪い例 (ダブルクォートがありません)
    %(This is #{quality} style)
    # should be "This is #{quality} style"

    # 悪い例 (複数行です)
    %(<div>\n<span class="big">#{exclamation}</span>\n</div>)
    # should be a heredoc.

    # 良い例 (挿入が必要、ダブルクォートがある、そして１行です)
    %(<tr><td class="name">#{name}</td>)
    ```

* 文字列に`'`と`"`双方が含まれない限り、
  `%q`の使用は避けましょう。
  たくさんの文字列をエスケープしなくてもよいときは、
  通常の文字列リテラルのほうがより読みやすく、
  推奨されるべきです。

    ```Ruby
    # 悪い例
    name = %q(Bruce Wayne)
    time = %q(8 o'clock)
    question = %q("What did you say?")

    # 良い例
    name = 'Bruce Wayne'
    time = "8 o'clock"
    question = '"What did you say?"'
    ```

* '/'が１つ *より多い* 正規表現に限り、`%r`を使いましょう。

    ```Ruby
    # 悪い例
    %r(\s+)

    # こちらも悪い例
    %r(^/(.*)$)
    # should be /^\/(.*)$/

    # 良い例
    %r(^/blog/2011/(.*)$)
    ```

* 呼び出すコマンドにバッククォートが含まれる(かなり起こりえないが)ことがない限り、
  `%x`の使用は避けましょう。

    ```Ruby
    # 悪い例
    date = %x(date)

    # 良い例
    date = `date`
    echo = %x(echo `date`)
    ```

* `%s`の使用は避けましょう。
  Rubyコミュニティは、スペース含むシンボルをを作る時は
  `:"文字列"`がよいと決めたようです。

* パーセントリテラルの区切り文字は、`%r`を除いて`()`が好まれます。
  正規表現の中では、`()`は色々なシーンで使われるので、
  正規表現の内容によっては、より使われる機会の少ない`{`のほうが
  良い選択となることがあるかもしれません。

    ```Ruby
    # 悪い例
    %w[one two three]
    %q{"Test's king!", John said.}

    # 良い例
    %w(one two three)
    %q("Test's king!", John said.)
    ```

## メタプログラミング

* 不要なメタプログラミングは避けましょう。Avoid needless metaprogramming.

* ライブラリに書かれているコアなクラスを汚すのはやめましょう
  (モンキーパッチを当ててはいけません)。

* ブロック渡しの`class_eval`のほうが、文字列挿入型よりも好ましいです。
  - 文字列挿入型を使う時は、バックとレースが働くように、常に`__FILE__`と`__LINE__`を渡しましょう:

    ```ruby
    class_eval 'def use_relative_model_naming?; true; end', __FILE__, __LINE__
    ```

  - `define_method`の方が、`class_eval{ def ... }`よりも好まれます。

* 文字列挿入型の`class_eval`(または他の`eval`)を用いる時は、
  挿入されたときのコードをコメントに追加しましょう(Railsでは活用されています)。

    ```ruby
    # from activesupport/lib/active_support/core_ext/string/output_safety.rb
    UNSAFE_STRING_METHODS.each do |unsafe_method|
      if 'String'.respond_to?(unsafe_method)
        class_eval <<-EOT, __FILE__, __LINE__ + 1
          def #{unsafe_method}(*args, &block)       # def capitalize(*args, &block)
            to_str.#{unsafe_method}(*args, &block)  #   to_str.capitalize(*args, &block)
          end                                       # end

          def #{unsafe_method}!(*args)              # def capitalize!(*args)
            @dirty = true                           #   @dirty = true
            super                                   #   super
          end                                       # end
        EOT
      end
    end
    ```

* `method_missing`を用いたメタプログラミングは避けましょう。
  何故なら、バックとレースが面倒になり、
  `#methods`のリストの中に出てこず、
  ミススペルしたメソッド呼び出しも無言で動いてしまいます、
  例えば`nukes.launch_state = false`のようにです。
  代わりに、移譲、プロキシ、または`define_method`を使いましょう。
  もし`method_missing`を使わなければならない時は:

  - [`respond_to_missing?`](http://blog.marc-andre.ca/2010/11/methodmissing-politely.html)も実装されているか確かめましょう
  - 既知の接頭辞、`find_by_*`のようなものを捕捉しましょう -- 可能な限りアサートさせましょう
  - 最後に`super`を呼び出しましょう
  - アサートする、特別でないメソッドに移譲しましょう:

    ```ruby
    # 悪い例
    def method_missing?(meth, *args, &block)
      if /^find_by_(?<prop>.*)/ =~ meth
        # ... lots of code to do a find_by
      else
        super
      end
    end

    # 良い例
    def method_missing?(meth, *args, &block)
      if /^find_by_(?<prop>.*)/ =~ meth
        find_by(prop, *args, &block)
      else
        super
      end
    end

    # それでも最も良い選択は、発見できる全てのアトリビュートにdefine_methodすることです
    ```

## 雑則

* `ruby -w`で安全なコードを書きましょう。
* オプショナルな変数としてのハッシュの使用を避けましょう。やりすぎてはいませんか？(オブジェクトの初期化はこのルールの例外です)
* コードのある行が10行を超えるメソッドは避けましょう。
  理想を言えば、多くのメソッドは5行以内がよいです。
  空行は行数には含めません。
* ３つや４つ以上引数を設定するのは避けましょう。
* もし本当に"global"なメソッドが必要な場合は、
  Kernelに定義し、privateに設定しましょう。
* グローバル変数の代わりに、モジュールのインスタンス変数を使用しましょう。

    ```Ruby
    # 悪い例
    $foo_bar = 1

    # 良い例
    module Foo
      class << self
        attr_accessor :bar
      end
    end

    Foo.bar = 1
    ```

* `alias_method`が動く時は、`alias`は避けましょう。
* 複雑なコマンドラインオプションをパースするために`OptionParser`を使いましょう。
  また、些細なオプションには`ruby -s`を使いましょう。
* 現在のシステム時間を読み出すには、`Time.new`よりも`Time.now`を使いましょう。
* それで問題ない時は、破壊的処理を避け関数型の手法でコードを書きましょう。
* それがメソッドの目的でない限り、引数に破壊的変更をするのはやめましょう。
* ３段階を超えるネストは避けましょう。
* 一貫性を保ちましょう。理想を言えば、このガイドラインに沿いましょう。
* 常識を用いましょう。

## ツール

ここでは、このガイドに反するコードを自動的にチェックするのを支援するツールをいくつか紹介します。

### RuboCop

[RuboCop](https://github.com/bbatsov/rubocop)は、このガイドに基づいた
Rubyコードスタイルチェッカーです。
Rubocopはすでにこのガイドの重要な部分をカバーしており、
MRI 1.9, MRI 2.0 双方をサポートし、Emacs向けのよいプラグインがあります。

### RubyMine

[RubyMine](http://www.jetbrains.com/ruby/) のコードインスペクションは、このガイドに
[部分的に基づいています](http://confluence.jetbrains.com/display/RUBYDEV/RubyMine+Inspections)。

# Contributing

このガイドに書いてあることには変更不能なものはありません。
Rubyのコードスタイルに興味のある全ての人と共に取り組むことが私の望みなので、
究極的には、全てのRubyコミュニティにとって有益なリソースを作ることができればと思っています。

改善のために、遠慮せずチケットを立てたりプルリクエストを送ったりしてください。
あなたの手助けに予め感謝します！

## 貢献するには

簡単です！ [contribution guidelines](https://github.com/bbatsov/ruby-style-guide/blob/master/CONTRIBUTING.md)を読んでください！

# ライセンス

![Creative Commons License](http://i.creativecommons.org/l/by/3.0/88x31.png)
この著作物は、[Creative Commons Attribution 3.0 Unported License](http://creativecommons.org/licenses/by/3.0/deed.en_US)
に従います。

# 広めましょう

コミュニティ駆動のスタイルガイドは、これを知らないコミュニティにはほとんど役に立ちません。
このガイドについてつぶやいたり、友達や同僚にシェアしてください。
全てのコメント、提案、オプションがこのガイドを少しだけでも良くしていきます。
そして、考えうるベストのガイドが欲しいですよね？

ありがとう<br/>
[Bozhidar](https://twitter.com/bbatsov)
