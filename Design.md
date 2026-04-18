# Portfolio Design Specification
**阿部 若奈 — 図解デザイナー**

---

## コンセプト

「情報を図にする人」が自分自身を図で語るポートフォリオ。
vonix.co のようなプロダクトデザイン的な清潔感と、Low-Tech Magazine の軽量哲学を組み合わせる。
外部リソースなし（フォント・画像・JSライブラリ不使用）。全グラフィックはインラインSVG。

---

## カラーパレット

| 変数 | 値 | 用途 |
|---|---|---|
| `--bg` | `#fafaf8` | ページ背景 |
| `--ink` | `#0d0d0d` | テキスト・線 |
| `--mid` | `#888888` | サブテキスト・アイコン |
| `--line` | `#e4e0db` | グリッド線・ボーダー |
| `--surface` | `#f4f1ec` | カード背景・タグ |
| `--invert` | `#0d0d0d` | 黒背景ブロック |
| `--invert-text` | `#fafaf8` | 黒背景上のテキスト |

アクセントカラーなし。モノクロのみ。

---

## タイポグラフィ

```
見出し (h1, h2):    system-ui, sans-serif / font-weight: 700 / letter-spacing: -0.03em
イタリック装飾:      Georgia, serif / font-style: italic / font-weight: 400
本文・UI:           system-ui, sans-serif / font-weight: 400
ラベル・キャプション: system-ui / font-size: 0.68rem / letter-spacing: 0.12em / text-transform: uppercase
```

**スケール:**
- h1: 3.2rem
- h2: 2rem  
- h3: 1rem / font-weight: 600
- body: 0.88rem
- label: 0.68rem

**イタリック使用箇所:** h1・h2の2行目（例: `デザイナー` の前後）

---

## レイアウト・グリッド

- 最大幅: `1100px`、中央寄せ
- 左右に `1px solid var(--line)` のボーダー（ページ全体を囲む縦線）
- セクション区切り: `1px solid var(--line)` の横線
- グリッド交差点に `6px` の黒い丸ドット（`::before` 疑似要素）
- カラム: 1・2・3カラムのグリッドを混在

```
Hero:        2カラム (テキスト 1fr | SVGイラスト 1fr)
スキル:      3カラム
ワーク種別:  3カラム (各セルにSVGアイコン)
職歴:        1カラム (年 + 内容の2カラム内部グリッド)
学歴・スキル: 2カラム
```

---

## コンポーネント

### セル（.cell）
```
padding: 2rem 2.5rem
border-right: 1px solid var(--line)
border-bottom: 1px solid var(--line)
::before { 左上角に黒丸ドット }
```

### タグ（.tag）
```
background: var(--surface)
font-size: 0.68rem
padding: 0.1rem 0.5rem
color: var(--mid)
```

### スキルドット
```
filled: ● (color: var(--ink))
empty:  ○ (color: var(--line))
letter-spacing: 0.2em
```

### 黒塗りブロック
ヘッダーバーと一部カード見出しに使用。
```
background: var(--invert)
color: var(--invert-text)
padding: 0.45rem 1rem
```

### リンクホバー
```
default: underline / color: var(--ink)
hover:   background: var(--ink) / color: var(--bg) / text-decoration: none
```

---

## SVGグラフィック仕様

**スタイル:** モノクロ線画。stroke のみ（fill は white または なし）。
stroke-width: 1〜1.5px。角丸 rx=4〜8。

### ① ヒーローイラスト（480×360）

vonix.co のようなプロダクトUI風。**図解制作プロセス**を表現：

```
要素:
- 背景: 同心円2つ（stroke-dasharray でダッシュ線、薄いグレー）
- ドットグリッド: 左側に 3×8 の点群
- メインカード: 白い角丸矩形 + 上部グレーバー（ブラウザ風）
  - バー内: 黒丸・グレー丸・薄丸（ウィンドウドット）
- カード内フローチャート（横並び3ステップ）:
    [情報収集] →（矢印）→ [整理・分類]（黒塗り）→（矢印）→ [図解化]
    下段: 3つの小カード（データカード風）
    最下段: 黒丸3つ + 空白丸4つ（進捗ドット）
- フローティング要素:
    右上: 角丸ピル型チップ「図解 ✓」
    左下: 黒背景バッジ
```

### ② ワーク種別アイコン（48×48）

各アイコンは `viewBox="0 0 48 48"` の正方形SVG。stroke-width=1.5、fill=none。

- **図解・資料**: 四角3つ→矢印で繋がるフロー図
- **DTP・印刷**: 4本の横線（段組レイアウト）+ 左に縦の太線
- **3DCG・映像**: 等角投影の立方体（3辺のみ）

---

## ページ構成とコンテンツ

### トップバー（黒）
```
⬡  外部リソースなし  ·  システムフォントのみ  ·  ~12KB
```

### ヒーローセクション
```
左:
  ラベル: "Portfolio · 2026"
  h1: 阿部 若奈
      <em>図解デザイナー</em>
  サブ: 複雑な情報をわかりやすいビジュアルへ。
       DTP・資料・3DCG・映像を横断するデザイナー。
  連絡先:
    WEB  実務ポートフォリオ ↗ (https://sites.google.com/view/wakanaabe/home)
    WEB  個人制作 — Behance ↗ (https://www.behance.net/114f2d32)
    MAIL wcn.aby@gmail.com
    TEL  080-6390-0765

右: ヒーローSVGイラスト
```

### ワーク種別グリッド（3セル）
```
[SVGアイコン]
h3: 図解・資料制作
p:  複雑な情報をクリアに整理するインフォグラフィック・プレゼン資料

[SVGアイコン]
h3: DTP・印刷物
p:  ポスター・冊子・広報誌などの印刷デザイン

[SVGアイコン]
h3: 3DCG・映像
p:  Cinema4Dによる3DCGモデリングと文化財動画制作
```

### スキルグリッド（3セル）
```
Adobe Suite:       Illustrator ●●●●○ / InDesign ●●●●○ / Photoshop ●●●○○
制作ツール:         Canva ●●●●● / Figma ●●○○○ / Cinema4D ●●○○○
ビジネスツール:     Google Workspace ●●●●● / Microsoft Office ●●●●●
```

### 職歴タイムライン
```
2026 –   資料作成デザイナー・3DCGモデラー        #3dcg #資料デザイン
〜       スタートアップ 一人デザイナー            #UI #WEB #LINE api
〜       文化財動画制作                          #動画
2020–21  デンマーク留学 Nordfyns Højskole
〜       長岡市国際交流センター 広報デザイン担当   #ポスター #冊子
〜       アルバイト・時々デザイン
2016     DTPオペレーター                         #DTP
```

### 学歴（2カラム）
```
左:
  2020  Nordfyns Højskole（デンマーク）
  2014  長岡造形大学 建築・環境デザイン学科 インテリアデザインコース 修了
  2010  長岡明徳高校 卒業

右: スキルドット表（上記スキルグリッドと同内容）
```

### フッター
```
左: © 2026 阿部 若奈
右: 外部リソースなし · システムフォントのみ · ~12KB
```

---

## 実装制約

- HTML/CSS のみ（JavaScriptなし）
- 外部リソース読み込みなし（`<link>`・`<script src>`・`url()` 禁止）
- 全グラフィック: インラインSVG
- 推定ページサイズ: 12〜16KB以内
- レスポンシブ: 600px以下でカラム数を1に折りたたむ
