# NEON NAV v41 — 公開用パッケージ

スマートフォン対応のNEON NAV静的サイト一式です。v40のルート探索・複数ルート比較・モバイルUI・PWA機能を維持し、地図上の帰属表示と著作権・ライセンス案内を強化しました。

## ファイル

- `index.html` — アプリ本体
- `manifest.webmanifest` — PWA設定
- `sw.js` — アプリシェルのキャッシュ（v41）
- `icon.svg` / `icon-192.png` / `icon-512.png` — アイコン
- `LICENSE-NEON-NAV.txt` — NEON NAV独自コード・デザインの著作権表示
- `THIRD_PARTY_NOTICES.md` — 第三者ソフトウェア・外部データ・APIのライセンスと利用条件

## すぐ試す

1. `index.html` をFirefox / Chrome / Edgeで開きます。
2. 地図・地名検索・道路データ取得にはインターネット接続が必要です。
3. ブラウザの「内部自己診断」を実行して基本テストを確認します。

`file://` での起動は可能ですが、現在地、共有リンク、PWAインストール、Service WorkerはHTTPSまたはlocalhostでの利用を推奨します。

## インターネットに公開する

### Cloudflare Pages（ZIPアップロード）

1. CloudflareのWorkers & Pagesを開きます。
2. Pagesプロジェクトを新規作成し、Direct Uploadを選びます。
3. このZIPファイル、または展開した `NEON_NAV_public_v41` フォルダーをアップロードします。
4. Deployして発行URLを確認します。

公式手順: https://developers.cloudflare.com/pages/get-started/direct-upload/

### GitHub Pages

1. GitHubで新しいリポジトリを作ります。
2. ZIP内のファイルをリポジトリ最上位へアップロードします。
3. Settings → Pages → Deploy from a branch を選び、`main` / `/(root)` を指定します。
4. 発行URLを開いて動作確認します。

公式手順: https://docs.github.com/en/pages/quickstart

## 地図・APIの公開運用で必ず確認すること

- **OpenStreetMap**: `© OpenStreetMap contributors` 表示とODbLへのリンクを地図上に残してください。標準タイルサーバーは共有資源で、タイルの大量ダウンロードや先読みは禁止されています。 https://operations.osmfoundation.org/policies/tiles/
- **HOT地図**: HOTの帰属表示に加え、配信元OpenStreetMap Franceの利用条件があります。公開・非営利・適度なトラフィック等の条件が示されているため、商用や高トラフィックの公開先として安易に使わないでください。 https://www.openstreetmap.fr/usage/
- **Nominatim**: 公開サーバーは最大1リクエスト/秒などの条件があります。オートコンプリートや大量検索に使わず、利用者が明示的に検索したときだけ呼び出すなど、利用ポリシーを守ってください。 https://operations.osmfoundation.org/policies/nominatim/
- **Overpass API**: 公開インスタンスは共有資源であり、混雑・制限・停止があり得ます。大規模な一般公開サービスでは、専用・商用サービスまたは自前環境を検討してください。 https://wiki.openstreetmap.org/wiki/Overpass_API
- **Geofabrik**: 任意PBFデータはこのZIPに含まれません。取得データはODbL 1.0です。 https://www.geofabrik.de/data/download.html
- キャッシュ対象はアプリシェルだけです。地図タイル・Nominatim・Overpassの応答をこのService Workerが先読み・保存することはありません。
- 共有リンクには出発地・目的地の緯度経度が含まれます。
- 所要時間は道路属性等に基づく推定であり、ライブ交通・最新通行止めを完全には反映しません。

## 著作権・ライセンス

地図の右下にOpenStreetMap / HOT / Leafletの帰属表示があり、アプリ最下部の「著作権・ライセンス」から主要ライセンスを確認できます。完全な一覧は `THIRD_PARTY_NOTICES.md`、NEON NAV独自コードの表示は `LICENSE-NEON-NAV.txt` を参照してください。

`NEON NAV Project` はこのパッケージのプロジェクト名として記載しています。公開者が正式な個人名・組織名で権利表示したい場合は、`LICENSE-NEON-NAV.txt` と `THIRD_PARTY_NOTICES.md` を公開前に調整してください。

## v41で変更した点

- 標準OSMタイルのクレジットにODbLへのリンクを明記。
- HOTタイルにHumanitarian OpenStreetMap TeamとOpenStreetMap Franceへの正式リンクを追加。
- Leaflet 1.9.4 / BSD-2-Clauseのリンクを地図上の帰属欄へ追加。
- アプリ最下部に開閉式のライセンス案内を追加。
- `LICENSE-NEON-NAV.txt` と `THIRD_PARTY_NOTICES.md` を同梱。
- Service Workerのキャッシュ名をv41へ更新し、古いv40シェルを更新対象にしました。
