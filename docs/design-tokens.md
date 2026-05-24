# デザイン仕様書 (Design Tokens)

将来の改修・新ページ作成時に、デザインの一貫性を保つための仕様書です。

---

## カラーパレット

すべて `plushpuppyjapan.com` から実測抽出した確定値です。

### プライマリ

| 役割 | カラーコード | 用途 |
|------|-------------|------|
| Plush Puppy Navy | `#43569f` | メインカラー、ボタン、見出し、リンク |
| Navy Dark (hover) | `#3a4889` | ホバー時の濃色 |
| Navy Soft | `#e8eaf3` | 背景の薄ニュアンス |

### アクセント

| 役割 | カラーコード | 用途 |
|------|-------------|------|
| Plush Puppy Orange | `#ef9a11` | アクセント、強調、CTAボタン |
| Orange Dark (hover) | `#d68607` | ホバー時の濃色 |
| Orange Soft | `#fff8eb` | 注意書きの背景 |

### テキスト

| 役割 | カラーコード | 用途 |
|------|-------------|------|
| Text Main | `#333333` | 本文 |
| Text Light | `#666666` | サブテキスト |
| Text Muted | `#999999` | キャプション・補足 |

### 背景・線

| 役割 | カラーコード | 用途 |
|------|-------------|------|
| White | `#ffffff` | カード背景 |
| BG Soft | `#f7f8fa` | パネル背景 |
| Border | `#e5e7eb` | 線 |
| Border Light | `#f0f1f4` | 薄い線 |

---

## タイポグラフィ

### フォントファミリー

| 用途 | フォント | 読み込み元 |
|------|---------|-----------|
| 日本語本文・見出し | Noto Sans JP | Google Fonts |
| 英語見出し | Source Sans Pro | Google Fonts |

Weights:
- Noto Sans JP: 300, 400, 500, 700
- Source Sans Pro: 400, 600, 700

### 見出しサイズ

| 用途 | サイズ | 例 |
|------|--------|----|
| ページタイトル | 32px | "Coat Diagnosis" |
| セクションタイトル | 24px | "Recommended Products" |
| サブセクション見出し | 18px | "愛犬のプロフィール" |
| 本文 | 16px | (デフォルト) |
| キャプション | 13-14px | 補足説明 |
| 小文字（英字ラベル） | 10-11px | "BASIC PROFILE" |

### 文字間隔

英字見出しには `letter-spacing: 0.1em〜0.2em` を付与してエレガンスを演出。

---

## 間隔・余白

### コンポーネント間

| 用途 | 値 |
|------|----|
| セクション間 | 40px |
| パネル内padding | 32px |
| カード間gap | 16px |
| ボタンpadding | 13px 48px |

### グリッド

| 用途 | 値 |
|------|----|
| 最大コンテンツ幅 | 1100px |
| グリッドgap | 16px |
| カード最小幅 (auto-fill) | 180px〜220px |

---

## ボタン

### Primary（紺）

```css
background: #43569f;
color: white;
padding: 13px 48px;
border-radius: 28px;  /* ピル型 */
box-shadow: 0 4px 12px rgba(67, 86, 159, 0.2);
```

### Ghost（透明背景）

```css
background: transparent;
color: #43569f;
border: 2px solid #43569f;
padding: 13px 48px;
border-radius: 28px;
```

### Large (診断ボタン用)

```css
padding: 18px 64px;
font-size: 16px;
font-weight: 700;
letter-spacing: 0.1em;
```

---

## カード・パネル

### 標準カード

```css
background: white;
border-radius: 12px;
box-shadow: 0 2px 8px rgba(0, 0, 0, 0.06);
padding: 32px;
```

### ホバー時

```css
box-shadow: 0 8px 24px rgba(0, 0, 0, 0.08);
transform: translateY(-2px);
```

---

## アニメーション

| 用途 | デュレーション | イージング |
|------|--------------|-----------|
| ホバー | 200ms | ease |
| ページ遷移 | 300ms | ease |
| チャート描画 | 800ms | Chart.js default |

---

## レスポンシブ

### ブレイクポイント

| サイズ | 範囲 | 主な変更 |
|--------|------|---------|
| Mobile | 〜640px | グリッド1列、フォント縮小、padding削減 |
| Tablet | 641px〜1024px | グリッド2列 |
| Desktop | 1025px〜 | グリッド3-4列、全機能展開 |

### iPhone対応

- viewport-fit=cover（ノッチ対応）
- env(safe-area-inset-*) で左右の余白確保
- input/select の font-size を 16px 固定（自動ズーム防止）

---

## アクセシビリティ

- すべての画像に `alt` 属性
- 外部リンクは `target="_blank" rel="noopener"`
- フォーカス時のアウトライン保持
- ボタンの min-height: 44px（タップしやすさ）
- カラーコントラスト比 4.5:1 以上

---

## 将来の拡張時の注意

新セクションを追加する際は:

1. **CSSクラス名は `.pp-` プレフィックス必須**（衝突防止）
2. **カラーは CSS変数（`var(--pp-navy)` 等）を使う**（一貫性）
3. **フォントは `var(--font-jp)` / `var(--font-en)` を使う**
4. **見出しは英→日の順**（"Coat Diagnosis" + "被毛診断"）
5. **オレンジ線アクセント** を要所に（plushpuppyjapan.com 流儀）

---

## 参考URL

- 本家デザインリファレンス: [plushpuppyjapan.com](https://www.plushpuppyjapan.com)
- カラー抽出元: 同上のトップページ・カテゴリページ
- フォント: [Google Fonts - Noto Sans JP](https://fonts.google.com/specimen/Noto+Sans+JP)
