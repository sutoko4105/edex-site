# EDEX Kendama 公式サイト：作業する人・AIへの約束

PLAKEN（3Dプリントのけん玉）のブランド EDEX Kendama の公式サイト。ドメインは edexkendama.com。
名刺のQRから海外の人も来るので、日本語と英語の両方を同じ質で保つこと。

## 作り

- ビルドなしの静的サイト。フレームワークもパッケージも使わない。
- `index.html`：トップ。写真 → スクロール版（最新モデルV2の分解）→ 開発ログ → Tap Lab → 購入先 → フォロー。
- `v1.html`：開発ログから開く、V1のスクロール版（アーカイブ）。
- `tap-lab.html`：Tap Lab（Tapを縮尺どおりの図で分解するウェブアプリ）。単体で動く。
- `img/`：ロゴと実物写真。`og.jpg` はSNSで共有したときの画像。
- `frames/v2/f000.webp`〜`f161.webp`、`frames/v1/f000.webp`〜`f161.webp`：スクロール版のコマ（162枚ずつ）。
- `404.html`：存在しないURLのときに出るページ。どの階層のURLでも表示されるので、中の画像やリンクは `/` から始まる書き方にしている。
- `favicon.ico`・`apple-touch-icon.png`・`icon-192.png`：ブラウザのタブとスマホのホーム画面のアイコン（EDEXのマーク）。
- `sitemap.xml`・`robots.txt`：検索エンジン向け。ページを足したら `sitemap.xml` にも足す。
- `CNAME`：独自ドメイン edexkendama.com の設定。GitHub が管理しているので消さない。

## 言語

- 同じHTMLに日本語（`.l-ja`）と英語（`.l-en`）を並べて書き、`html[data-lang]` で片方を隠す。
- 決め方：URLの `#ja` / `#en` → 保存した選択（localStorage `edex-lang`）→ 端末の言語（日本語なら日本語、それ以外は英語）。
- 文言を変えるときは、必ず両方の言語を直す。

## スクロール版

- `<canvas>` に、スクロール位置に合わせてコマを描く。コマはスクロール版に近づいてから読み込む。
- スクリプトの `N`（コマ数）、コマのフォルダ、キャプションの範囲（`<section class="cap" data-from data-to data-step>`）、ステップ数（`/ 07`）、スキップを消す位置（`LAST` または `f >= 150`）は連動している。コマ数を変えたら全部合わせる。
- コマの画像は編集・圧縮・差し替えをしない。3Dモデルから別の場所で描いている。

## 絶対にしないこと

- 3Dモデルのファイル（`.3mf`、`.stl`、`model-data.json`、`model.json`、`scroll-config.json` など）をこのサイトやリポジトリに入れない。形が抜き出せてしまう。
  描画の道具とモデルは、オーナーの Google ドライブ「EDEX Kendama｜3Dモデル」に置いてあり、そこで描いたコマだけをここに入れる。
- 断面図や内部構造（インフィル）を見せない。
- ルナホールの形について書かない（形はモデルごとに違う）。重さの公差は載せない。
- 「どのけん玉にもない」と言い切らない。使ってよい言い方は「現行の実用的なけん玉では、ほかに見ない形」。
- アクセス解析は GoatCounter（クッキーなし・個人情報なし）だけを使う。ほかの解析タグや広告タグは足さない。

## 購入リンク

- 日本語：STORES のショップトップ `https://edex-kendama.stores.jp/`
- 英語：FANKEN の EDEX 一覧 `https://fanken.jp/en/collections/edex-kendama-%E6%97%A5%E6%9C%AC`
- 日本語ページの「海外の方は FANKEN へ」：`https://fanken.jp/collections/edex-kendama-%E6%97%A5%E6%9C%AC`
- 個別の商品ページには直接リンクしない（在庫や型が変わってもリンクを直さずに済むように）。
- V2 は H型・V型の区別をしない。

## 新しいモデルが出たとき

1. 新しいモデルのコマを `frames/<モデル>/` に入れる（コマはドライブ側で描く）。
2. トップ（`index.html`）のスクロール版を新しいモデルに切り替え、キャプションを新しいモデルに合わせる。
3. それまでの最新モデルは `v1.html` と同じ形のアーカイブページ（例：`v2.html`）にして、開発ログのカードから「構造を見る（アーカイブ）」でつなぐ。
4. 開発ログに新しいカードを一番上に足し、`LATEST` を付け替える。

## 確認すること

- スマホ幅 360px・390px で横にはみ出さない。
- JP/EN の切り替え、`#ja` / `#en` 付きのURL。
- コンソールに 404 やエラーがない（コマが全部読める）。
- スクロールでキャプションが 01〜07 の順に切り替わり、最後に購入ボタンが出る。

## アクセス解析（GoatCounter）

- 各ページ（`index.html`・`v1.html`・`tap-lab.html`）の `var CODE = 'edexkendama'` が GoatCounter のサイトコード（edexkendama.goatcounter.com）。空にすると止まる。edexkendama.com 以外（プレビューや手元）では数えない。
- GoatCounter 公式の `<script data-goatcounter=...>` タグは貼らない（二重に数える。読み込みはこの `CODE` の仕組みで済んでいる）。
- 自分の端末を数えないようにするには、その端末で `https://edexkendama.com/#toggle-goatcounter` を一度開く（もう一度開くと元に戻る）。
- ページの表示は自動で数える。名刺のQRは `https://edexkendama.com/?campaign=card` にしてあり、GoatCounter の Campaigns に「card」として出る。
- クリックはイベントとして数える。名前は `click/<何>/<場所>/<言語>`。
  - 何：`buy-stores`・`buy-fanken`・`follow-instagram`・`follow-x`・`note`・`contact`・`open-taplab`・`open-v1`
  - 場所：`structure`（スクロール版）・`log`（開発ログ）・`buy`（購入先）・`follow`・`hero`・`header` など
- スクロール版を最後まで見た人は `scroll/v2-end/<言語>`（V1ページは `scroll/v1-end/<言語>`）。
- 新しいリンクの種類を足したら、ページ内の `kinds` の一覧にも足す。

