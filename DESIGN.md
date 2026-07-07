# pebble ホームページ 設計メモ

2026-07-06 初版 ／ 2026-07-07 更新（ロゴシステム刷新まで反映）／ 制作: Fable

## 店舗情報（調査ソース）

- 店名: pebble（ペブル）— 「小石」の意
- 業態: ワインバーとして 2024年7月17日 開業 → 2025年7月 シェフ・夏川氏を迎えレストランへリニューアル
- 場所: 〒530-0043 大阪府大阪市北区天満 3-1-2 TSビル 5F（安藤忠雄設計・故 堺屋太一氏の旧邸宅）
- 眺望: 大川（旧淀川）
- アクセス: 天満橋駅から約 240m（徒歩約3分）
- 席数: 10席（カウンター6 ＋ 個室テーブル4／最大4名）
- 料金: ランチ ¥8,800〜 ／ ディナー ¥10,800〜¥19,800（税込・サービス料 7% 別）
- 営業: 月・火・木・土・祝 12:00–14:30 / 18:00–22:00、水・金 18:00–22:00、日曜定休
- 電話: 06-6356-0141 ／ 予約: TableCheck https://www.tablecheck.com/ja/pebble
- Instagram: https://www.instagram.com/pebble_wine_osaka/
- Google Maps: https://maps.app.goo.gl/BENYgtLQY3g4eQJY9
- ミシュランガイド掲載ページあり（guide.michelin.com）※サイト本文には未記載。掲載を謳う場合は店側で確認のこと

情報ソース: TableCheck 店舗ページ、食べログ(en)、MICHELIN Guide 検索結果。
**営業時間・価格は食べログ/TableCheck 由来のため、公開前に店舗で最終確認を推奨。**

## Instagram とホームページの役割分担（本設計の核）

| | Instagram（動く情報） | ホームページ（変わらない情報） |
|---|---|---|
| 役割 | 日々の発信・ファンとの接点 | 公式の受け皿・予約への導線 |
| 内容 | 本日の一皿、入荷ワイン、臨時休業、空席案内、季節の告知 | コンセプト、コース料金、営業時間、アクセス、予約窓口 |
| 更新頻度 | 高（店側が日々運用） | 低（変更時のみ） |
| 導線 | プロフィールリンク → HP（予約へ） | 各所から IG へ送客 |

設計上の反映:
1. **ヒーロー直下**に「日々の更新は Instagram で」の常設リンク（最初の1画面で役割を宣言）
2. **専用セクション「日々のことは、Instagramで。」**で役割分担を2カラムで明示 — 訪問者が「どちらを見ればいいか」で迷わない
3. コース料金の注記に「最新のコースは Instagram にて」— 価格改定のたびに HP を触らなくても矛盾が生きにくい構造
4. HP 側は予約 CTA（TableCheck ＋ 電話）を終着点に置き、IG プロフィールのリンク先として機能する

運用の推奨: Instagram プロフィールのリンクをこの HP（または予約セクション #reserve への直リンク）に設定する。

## デザイン（2026-07-07 現行）

- モチーフ: 店名 pebble（小石）× 大川 → 「水面に落ちた小石の波紋」。canvas アニメーション、発生点は右上にオフセット（アシンメトリー）。prefers-reduced-motion では静止画
- 配色（ブランド素材準拠）: 生コンクリート #D8D5D0 地＋SVGノイズの打ちっぱなしテクスチャ ／ 墨 #24221D ／ 錆（店頭コールテン鋼看板由来）#6E4832。ダークは夜のコンクリート #1B1A18 ＋ 錆 #C68E6B
- タイポ: 本文は明朝（Hiragino Mincho / Yu Mincho）、ラベルはゴシック。縦書き章ラベル
- 予約導線: ヒーロー通過後に追従バー（ご予約ボタン→モーダル）＋予約セクションに TableCheck（主）/食べログ/一休.com 並列＋電話。IG は予約経路に挟まない
- 単一ページ構成: Hero → Concept → Cuisine → Wine → Space → Instagram → Information → Reservation → Footer
- ライト/ダーク両テーマ対応（CSS変数 4ブロック: `:root`／`prefers-color-scheme`／`data-theme` 両値）、レスポンシブ（620px でモバイルレイアウト）
- 角丸なし（round=0）で確定（2026-07-07 比較検討・round study）: 円=水と石・動くもの（波紋・小石ロゴ）、直角=建築・静的な構造（枠・ボタン・モーダル・写真）という役割分担。丸みは料理・接客が担い、サイトの構造は建築に忠実に（yamano: 「建物の角と料理・ソムリエ接客の丸」）

## ロゴシステム（2026-07-07 確定）

- **絶対ルール: 公式ロゴ準拠**。ヒーローとフッターは共通の `.lockup` コンポーネントを使う。比率は原画 `assets/logo-pebble-full.png` からの実測値で固定 — **石の幅=店名幅の 67.9%、石と店名の間隔=店名幅の 13.6%**（=店名高さの 0.565 倍）。配置ごとに変えてよいのは全体幅のみ（ヒーロー `clamp(220px, 38vw, 380px)`／フッター 96px）
- ロックアップは `transform: scale(0.9)` で 10% 縮小（レイアウト枠は不変＝周囲の要素位置に影響しない・余白として還元）
- **色: 白抜きが本番**（wm study で白/墨を比較し白を採用）。石 `logo-pebbles.png`・店名 `pebble-wordmark-white.png` とも両テーマ共通で白。追従バーの小石も白
- 素材はすべて公式アセットからの切り出し（自作SVGは廃止）:
  - 石: `assets/icon-pebble.jpg` → 輝度しきい値でアルファ化 → `assets/img/logo-pebbles.png`（白）
  - 店名: `assets/logo-pebble-full.png` の文字帯 → `assets/img/pebble-wordmark-white.png` ほか色違い
  - 透過PNG生成の注意: **透明画素の色は形と同色で焼く**（黒透明だと縮小時に灰色のフリンジ=縁取りが出る）
- ワードマークの書体: 市販フォントに一致なし（比率・極細モノラインは ITC Avant Garde Gothic Extra Light が最も近いが、e の横棒が円からはみ出す特徴はカスタム作字）。よって文字もアセット画像を使用し、HTML には SEO/読み上げ用の不可視テキスト `pebble` を残す
- 墨色トークン `--stones`／`--wm`（ライト=墨・ダーク=紙色の焼き分けPNGを切替）は wm-ink 習作のために温存

## 実装メモ（実機で踏んだ罠）

- `dialog::backdrop` に backdrop-filter を掛けない — iOS Safari で backdrop がダイアログ本体より上に合成され、モーダルが見えなくなる
- `<dialog>` は `position: fixed; inset: 0; margin: auto; height: fit-content` で明示的にビューポートへ固定 — iOS Safari は文書先頭基準で配置することがある
- モーダルを閉じたら開いた時点の `scrollY` を `close` イベントで復元 — フォーカス復帰でページ先頭へ飛ぶ
- ヒーローの高さは `svh`（vh はモバイルの URL バー収納で「最大ビューポート」基準になり、スクロール中に余白が伸びて見える）
- 日本語見出し・ラベルの折り返しは `.nb`（inline-block）で文節単位に制御
- claude.ai の Artifact プレビューは sandboxed iframe のため `<dialog>` のトップレイヤーが機能しない — スタディ版のみオーバーレイ方式に差し替え済み。実機確認は GitHub Pages のサブパスデプロイ（docs/<slug>/）が確実

## ファイル構成

- `index.html` — 最新版（`assets/` を相対参照）／ `docs/` — GitHub Pages 配信用コピー（**手動 cp 同期。二重管理は既知の課題**）
- `assets/logo-pebble-full.png`・`assets/icon-pebble.jpg` — 公式ロゴ原画（yamano 提供）
- `assets/img/_src/` — 元写真（yamano 提供）／ `assets/img/` — web 最適化コピー＋ロゴ切り出しPNG群
- `versions/vN/index.html` — 各バージョンの自己完結スナップショット（画像 base64 埋め込み・単体で開ける）
- `versions/round-a, round-b` — 角丸スタディ(不採用)／ `versions/wm-ink` — 墨色ロックアップ習作（https://kazuyamano.github.io/pebble-fable/wm-ink/ に配信）
- `VERSIONS.md` — バージョン履歴・スタディの採否記録

## 今後の課題

- docs/ 二重管理の解消（Actions のデプロイ対象をルートに変更すれば docs/ 複製を廃止できる）
- JSON-LD 構造化データ（Restaurant スキーマ: 住所・電話・営業時間・価格帯）— 検索・マップでの見え方に効く
- ドメイン取得と `og:image` 等の OGP 整備＋favicon（ヒーロー画像なし構成のため og:image は space-interior 推奨）
- Instagram 公式埋め込み（oEmbed / Meta の embed.js）の追加はホスティング先が決まってから
- 営業時間・価格の店舗最終確認（食べログ/TableCheck 調べのまま公開中）
- リリース前の実機スモークチェックの習慣化（iPhone 実機＋狭幅 375px でヒーロー・モーダル・追従バー）

（解決済み: 一休.com 店舗直リンク → v4 で反映）
