# 犬種追加用テンプレート

新しい犬種を追加する場合、`index.html` の2箇所を編集します。

---

## 編集箇所1: 犬種セレクトのHTML

`<select id="breed">` の中の `<optgroup>` から該当するコートタイプを探して、`<option>` を追加します。

### 例: ベルジアンシェパード（ダブルコート）を追加

```html
<optgroup label="ダブルコート">
  <option value="pomeranian">ポメラニアン</option>
  <option value="shiba">柴犬</option>
  ...
  <option value="belgian_shepherd">ベルジアンシェパード</option>  ← この行を追加
</optgroup>
```

---

## 編集箇所2: BREED_TO_COAT マッピング

`const BREED_TO_COAT = {` の中に、犬種のコート分類を追加します。

```javascript
const BREED_TO_COAT = {
  ...
  // ダブル
  pomeranian:'double', shiba:'double', ...
  belgian_shepherd:'double',   // ← この行を追加
  ...
};
```

---

## サイズバリエーション追加の例

例: 「ベルニーズマウンテンドッグ」と「ポーチュギーズシープドッグ」を追加する場合

### 編集1: HTMLに optgroup を追加

```html
<optgroup label="大型ダブルコート">
  <option value="bernese">ベルニーズマウンテンドッグ</option>
  <option value="great_pyrenees">グレートピレニーズ</option>
</optgroup>
```

### 編集2: BREED_TO_COAT に追加

```javascript
bernese:'double',
great_pyrenees:'double',
```

---

## 親コート（COAT_PARENT）について

サイズ別のサブカテゴリを新設する場合（例: 新たに `large_double` というサブタイプを作る場合）:

1. **PRODUCTS の coats 配列** にも `'large_double'` を追加する商品マスタ更新が必要
2. **COAT_PARENT** マップに親コートを定義:
   ```javascript
   const COAT_PARENT = {
     ...
     large_double:'double',
   };
   ```

これにより、`large_double` 専用製品がなくても、`double` 用製品にフォールバックします。

---

## value 名前付けの規則

- 半角英数字とアンダースコアのみ
- 全て小文字
- 国際的に通じる英名を使う（日本語ローマ字でも可）
- サイズ別は接尾辞 `_toy`, `_mini`, `_med`, `_std`, `_giant`
- タイプ別は接尾辞 `_smooth`, `_long`, `_wire`, `_rough`

### 良い例

```
poodle_toy
schnauzer_giant
collie_rough
```

### 悪い例

```
プードルトイ           ← 日本語不可
PoodleToy             ← 大文字は使わない
poodle-toy            ← ハイフン不可、アンダースコアで
poodle toy            ← スペース不可
```

---

## 動作確認

編集後、ブラウザで `index.html` を開いて:

1. 犬種セレクトに新しい犬種が表示されるか
2. その犬種を選んで診断したとき、適切な製品が推奨されるか

---

## サポート

複雑な編集（例: 新コートタイプの新設、推奨ロジックの大幅変更）は、
開発元（Resolution Engine Inc.）までご相談ください。
