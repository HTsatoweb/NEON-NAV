NEON NAV v40 — 公開用パッケージ
=================================

■ 入っているもの
- index.html             アプリ本体（単一HTML）
- manifest.webmanifest   ホーム画面追加／PWA設定
- sw.js                  アプリ本体のシェルキャッシュ用Service Worker
- icon.svg / icon-192.png / icon-512.png  アプリアイコン

■ すぐ試す
1. index.html をFirefox / Chrome / Edgeで開く。
2. 地図・地名検索・道路データ取得にはインターネット接続が必要。
3. ブラウザの「内部自己診断」を実行して基本テストを確認する。

file:// での起動は可能ですが、現在地、共有リンク、PWAインストール、Service Workerは
ブラウザのセキュリティ制約によりHTTPSまたはlocalhostでの利用を推奨します。

■ インターネットに公開する（Cloudflare Pages：ZIPアップロード）
1. CloudflareアカウントにログインしてWorkers & Pagesを開く。
2. Pagesプロジェクトを新規作成し、Direct Uploadを選ぶ。
3. このZIPファイル、または展開した NEON_NAV_public_v40 フォルダーをアップロードする。
4. プロジェクト名を決めてDeployする。
5. 発行された https://＜プロジェクト名＞.pages.dev/ を開いて動作確認する。

公式手順：
https://developers.cloudflare.com/pages/get-started/direct-upload/

注意：Direct Uploadで作ったプロジェクトは、後からGit連携へ切替できません。
Gitによる自動更新も使いたい場合は最初からGit integrationを選んでください。

■ GitHub Pagesで公開する方法
1. GitHubで新しいリポジトリを作成する。
2. このパッケージ内のファイルをリポジトリの最上位にアップロードする。
3. リポジトリの Settings → Pages を開く。
4. Build and deploymentで Deploy from a branch を選び、main / /(root) を指定して保存する。
5. 発行された https://＜ユーザー名＞.github.io/＜リポジトリ名＞/ を開く。

公式ガイド：https://docs.github.com/en/pages/quickstart

■ 公開前に必ず知っておくこと
- このパッケージは静的サイトです。アプリをWeb上に公開するファイル一式を用意しますが、
  あなたのCloudflare/GitHubアカウントへこちらからログインして公開操作を完了することはできません。
- 地図画像はOpenStreetMapタイル、地名検索はNominatim、道路グラフはOverpass APIを利用します。
  これらは無料の無制限サービスではなく、混雑・利用制限・停止があり得ます。
- OpenStreetMap標準タイルは、表示中の地図に必要な範囲だけ取得してください。広域の先読み・
  一括ダウンロードは禁止され、帰属表示を地図上に残す必要があります。
  https://operations.osmfoundation.org/policies/tiles/
- Nominatim公開サーバーは最大1リクエスト/秒などの条件があります。
  https://operations.osmfoundation.org/policies/nominatim/
- Overpass公開サーバーは小規模利用向けです。アプリ／サイト全利用者のアクセス量が集計されます。
  多数の一般利用者へ公開する場合は、専用または商用の道路データサービス、あるいは自前のOverpass環境と
  適切な地図タイル提供元へ切り替えてください。
  https://wiki.openstreetmap.org/wiki/Overpass_API
- キャッシュ対象はアプリのHTML等だけです。地図タイルやOverpass/Nominatimの応答をService Workerで
  先読み・保存しません。地図データ・検索・ルート計算には基本的にオンライン接続が必要です。
- 共有リンクには出発地・目的地の緯度経度が含まれます。共有ボタンを押すと確認が出ます。
- 所要時間は道路属性に基づく推定です。ライブ交通、リアルタイム通行止め、公共交通、運行時刻表、
  駐車場情報などを完全に反映するGoogle Maps相当のサービスではありません。

■ v40の主な変更
- ルート本数の25本固定上限を撤廃。正の安全な整数の範囲で必要数を指定できます。
- 「＋10本」で追加計算。実在する異なる道路経路のみを列挙します。
- ルート一覧を60件ずつ展開して、大量のDOM描画による負荷を抑制。
- 代替ルート用の道路取得コリドーを4段階固定から段階的拡張へ変更。
- タッチ操作、スマホ用レイアウト、地図全画面、共有URLからの地点復元。
- HTTPSホスト時のPWA manifest / Service Worker対応。
