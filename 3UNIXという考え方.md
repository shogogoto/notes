# UNIXという考え方

  お粗末なUNIX=crappy UNIXes: UNIXの方法論から離れた自称UNIX

  UNIXの考え方はコマンドなどの細部に埋もれがち

## イントロ
  OSは創造者の哲学を身にまとって現れる
    e.g. Mac
      高度に視覚に訴えるオブジェクト指向のUI
      「ほら、あなたのすぐ目の前に」というキャッチフレーズ
    e.g. MS-DOS
      メインフレームの香り
    e.g. DECのOpenVMS
      ユーザーはPCを恐れていると見なした
      ユーザーに与える選択肢は少なくて強力
    e.g. UNIX
      ユーザーは自信が何をしているのか解っているという前提
      「何をしているか分からないのなら、ここにいるべきでない」という不親切さ
        -> 初期のUNIXは支持を得ることに失敗

  UNIXの変遷
    初期
      大学やハッカーのおもちゃ
      ビジネス目的では使えないと思われた
    1980~
      どのOSよりも柔軟で移植性に富み、性能の高く格安のOSがあると噂
      しかし、ビジネス界がUNIXの進出を阻止した
      大学で若い世代が先入観なしにUNIXに親しんだ
      そして、ビジネスや学問の世界でUNIXが受け入れられるようになった

  オープンソース: UNIXが商標登録された故の代わりの呼称

## 1. UNIXの考え方: たくさんの登場人物たち

  タイムシェアリング=時分割方式: 極短時間に動作を切り替えることで\
    同時並列に多数のジョブを実行しているように見せる方式
    <-> バッチモード=一括処理方式: ジョブを蓄えておいて順次実行する方式


  ! :? でいろんな種類のデータを定義できるようにしたい
  !   e.g. :P = Person

  スペース・トラベル: MITが開発したMulticsシステム上でのゲーム
  最初のUNIX: {スペース・トラベル}の動作環境
    アセンブリ言語で書かれた
    P1 |Multicsから{タイムシェアリング}などの特徴を盗んだ
    by. ケン・トンプソン
      UNIXの発明者
    when. 1969
    where. AT&T研究所
    移植性のあるB言語で書き直し
      when. 1972

  B言語の拡張としてC言語が作られた
    by. デニス・リッチー
    when. 1973

  よいプログラマは素晴らしいソフトウェアを書く。偉大なプログラマは、\
    その素晴らしいソフトウェアを盗む
    e.g. `P1`

  偉大なプログラムは追い詰められた人間が書く
    実用的なものが要求されている
    どうやればできるか知っているエキスパートが周りにいない
    「正しく」やる時間がない

## 2. 人類にとっての小さな一歩
  VW: フォルクスワーゲン社

  UNIXの定理1=スモール・イズ・ビューティフル: プログラムは小さく始めて小さくシンプルに保つ
    「これからは小型車の時代」という{VW}のキャンペーンでもある
      アメリカでは大型車が持て囃されていた
      原油の価格高騰を契機に燃費の良いVWの小さな車が注目された
      小型車の燃費以外のメリットが発見された
        狭い駐車場に楽に駐車できる軽い乗り回し、応用力
        構造がシンプルでメンテしやすい

    <-> 巨大なアメリカンプログラム
      e.g. ファイルコピーのプログラム
        手順10以外は蛇足
        1. コピー元ファイル名を尋ねる
        2. そのファイルの存在チェック
        3. なければ通知
        4. コピー先ファイル名を尋ねる
        5. そのファイルの存在チェック
        6. あれば上書きするか尋ねる
        7. 元ファイルを開く
        8. 元ファイルが空だったら中止
        9. コピー先を開く
        10. コピーする
        11. 元ファイルを閉じる
        12. 先ファイルを閉じる

  問題の理解不足のために巨大な解決策を実装しようとしてしまう
  SFの90%はクズである。ただし、あらゆることの90%はクズである。

  {UNIXの定理1}のメリット
    理解しやすい
    保守しやすい
    メモリ消費量が少ない、軽い
    他のツールと組み合わせやすい
      <-> いろんなデータ形式に対応しようとする
        -> サポートされない形式が将来できて時代遅れになる
        <-> 未来を予測することを最初から諦める
          逆に時代遅れになることを避けられる

  UNIXの定理2=１つのプログラムには１つのことをうまくやらせる:
    <- 最良のプログラムは生涯で１つのことをうまくやる
    <- しのびよる多機能主義:
      プログラマの創造性が単一目的外の機能を付加しようとしてしまう
        ユーザーとの対話はホントに必要か？\
          ファイルかCLIからパラメータ入力するだけではいけないのか
        特殊フォーマットである必要があるのか？
    <- 車輪の再発明: すでに世の中にある車輪のようなものを再発明する無駄な作業
        既に似た機能をもつ他のプログラムがあるのではないか？
    <-> lsコマンド
      {UNIXの定理2}に反して、使われもしない膨大なオプションが追加されている
      表示を変換する別の機能と分離すべき

## 3. 楽しみと実益をかねた早めの試作

  UNIXの定理3=できるだけ早く試作を作成する:
    <- アイデアが成功するかどうかは現実的な場面でテストするまで分からない
    -> リリースが早まり、誤った前提のまま労力を無駄にするリスクが減る
    -> ユーザーのフィードバック

    <-> 正しい設計作法: 設計を完全にしてからコーディング
      こうすればうまく行くはずだ、という憶測でしかない
      まず、機能仕様書を書かなくちゃ
      e.g. リリース直前になって不意打ちを食らう







