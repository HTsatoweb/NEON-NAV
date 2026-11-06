# NEON NAV v41 — 第三者ソフトウェア・データのライセンス一覧

このファイルは、公開パッケージから利用する主な外部ソフトウェア、データおよびAPIをまとめたものです。個別の利用条件が変更される場合があるため、公開・運用時には各公式ページを再確認してください。

## 1. NEON NAV独自部分

- **対象**: NEON NAV独自のHTML/JavaScript、UI、デザイン、探索ロジック、PWA設定、同梱アイコン等
- **表示**: `© 2026 NEON NAV Project. All rights reserved.`
- **条件**: 詳細は同梱の `LICENSE-NEON-NAV.txt` を参照してください。
- この権利表示は第三者ライブラリ・地図データ・API応答には適用されません。
- 実際の公開権利者が個人名・団体名を使用する場合、公開前に `NEON NAV Project` をその正式名称へ置き換えてください。

## 2. ソフトウェア／ライブラリ

| 名称・バージョン | 用途 | ライセンス | 読み込み方法・公式情報 |
|---|---|---|---|
| Leaflet 1.9.4 | インタラクティブ地図表示 | BSD 2-Clause | CDNから実行時に取得。jsDelivrを優先し、unpkgをフォールバックに使用。 [公式ライセンス](https://github.com/Leaflet/Leaflet/blob/v1.9.4/LICENSE) |
| Osmix 0.4.1 | 利用者が `.osm.pbf` を手動読込した場合の解析 | MIT（上流プロジェクトの公開ライセンス） | PBF機能を使う時だけ動的import。jsDelivr / esm.sh / unpkg / Skypackを順に試行。 [上流リポジトリ・ライセンス](https://github.com/conveyal/osmix) |
| Web標準API | Canvas、Web Worker、IndexedDB、Service Worker、Geolocation、Web Share、Fullscreen等 | ブラウザ実装に従う | 外部ライブラリではありません。 |

LeafletはこのZIPにライブラリ本体を同梱せず、ブラウザからCDN経由で読み込みます。地図上のLeaflet名とBSD-2-Clauseライセンスへのリンクを残しています。Osmixも通常の自動道路取得では使わず、任意PBFの手動読込機能でのみ読み込みます。

### Leaflet — BSD 2-Clause License

Copyright (c) 2010-2023, Volodymyr Agafonkin  
Copyright (c) 2010-2011, CloudMade  
All rights reserved.

Redistribution and use in source and binary forms, with or without modification, are permitted provided that the following conditions are met:

1. Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.
2. Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

### Osmix — MIT License

Copyright (c) 2025 Conveyal

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

## 3. 地図・地理データ

### OpenStreetMap

- **帰属表示**: `© OpenStreetMap contributors`（リンク先: https://www.openstreetmap.org/copyright）
- **データライセンス**: Open Data Commons Open Database License 1.0（ODbL 1.0）
- **利用箇所**: 標準地図タイル、道路・フェリー航路データ、地名検索結果、任意PBFデータ
- **注意**: OSMデータを改変・派生してデータベースとして配布する場合などは、ODbLの帰属・共有継承条件を確認してください。
- 公式: https://www.openstreetmap.org/copyright

### HOT Humanitarian map style

- **帰属表示**: `Tiles style by Humanitarian OpenStreetMap Team hosted by OpenStreetMap France`
- **スタイル**: HDM-CartoCSSのスタイルシート・Nori icons・Maki iconsは上流プロジェクトでCC0として公開されています。
- **サーバー**: `tile.openstreetmap.fr/hot` のタイル提供はOpenStreetMap Franceがホストします。
- **注意**: HOTタイルの提供元利用ポリシーでは、公開・非営利・適度なトラフィック等の条件が示されています。商用・高トラフィック用途に自動で適合するとは限りません。該当する場合は別の適切なタイル提供元へ切り替えてください。
- 公式情報: https://github.com/hotosm/hdm-cartocss · https://www.openstreetmap.fr/usage/

### Geofabrik

- **用途**: 画面から案内する任意の地域別 `.osm.pbf` データ取得元
- **データライセンス**: OpenStreetMap由来データはODbL 1.0
- **注意**: PBFファイル自体はこのZIPには含めていません。ダウンロードしたデータにも出典・ODbLの条件が適用されます。
- 公式: https://www.geofabrik.de/data/download.html

## 4. 外部API・サービス（ソフトウェアライセンスとは別の利用ポリシー）

| サービス | 用途 | データのライセンス／条件 | 公式ポリシー |
|---|---|---|---|
| OpenStreetMap Standard Tile Server | 標準地図画像 | OSM由来データのODbL帰属表示が必要。タイルサーバーは共有資源で、可用性保証なし。大量取得・先読みは禁止。 | https://operations.osmfoundation.org/policies/tiles/ |
| OpenStreetMap France HOT Tile Server | HOTスタイル地図画像（標準タイル失敗時の代替） | OSMデータODbL + HOTスタイルCC0。提供元独自の公開・非営利・中程度トラフィック条件あり。 | https://www.openstreetmap.fr/usage/ |
| Nominatim | 利用者操作による地名検索 | OSM由来データはODbL。公開サーバーは最大1リクエスト/秒、明確なアプリ識別、帰属表示等が必要。オートコンプリート・大量検索用途に使用しない。 | https://operations.osmfoundation.org/policies/nominatim/ |
| Overpass API (`overpass-api.de`, `overpass.private.coffee`) | 道路way・フェリー航路・ノードの読み取り | 応答に含まれるOSMデータはODbL。公開インスタンスは共有資源で、負荷・混雑・利用制限により応答しない場合がある。 | https://wiki.openstreetmap.org/wiki/Overpass_API |
| Geofabrik Download | 任意PBFデータへの案内 | OSM由来の配布データはODbL 1.0。 | https://www.geofabrik.de/data/download.html |

APIの稼働率・速度・利用可能性は保証されません。一般公開後に利用者が増える場合、共有公開APIをそのまま大規模サービスのバックエンドとして使い続けず、各提供元の条件に合った専用・商用サービスまたは自前環境を検討してください。

## 5. CDN

Leaflet / Osmixの配布にjsDelivr、unpkg、esm.sh、Skypackを参照します。これらはファイル配信先であり、配信されるライブラリのライセンスを置き換えません。

## 6. 公開時チェック

- [ ] 地図の隅にOSM帰属表示が常時見えること。
- [ ] OSM表記からODbLを説明する公式著作権ページへリンクできること。
- [ ] HOTタイル表示時にHOTとOpenStreetMap Franceの帰属が見えること。
- [ ] Leaflet / BSD-2-Clause表示が地図上に残っていること。
- [ ] Nominatim・Overpass・タイルの各利用ポリシーに沿ったトラフィックで運用すること。
- [ ] `LICENSE-NEON-NAV.txt` の権利者表記が公開者の意図に合っていること。

この一覧は法的助言ではありません。用途、アクセス規模、加工データの配布形態に応じて、各ライセンス本文と提供元の最新ポリシーを確認してください。
