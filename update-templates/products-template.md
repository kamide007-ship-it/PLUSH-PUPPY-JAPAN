# 新商品追加用テンプレート

`index.html` の `const PRODUCTS = [` から `];` の間に、下のテンプレートをコピペして必要箇所を書き換えてください。

---

## シャンプー用テンプレート

```javascript
  { id:'pp_XXXXX', cat:'shampoo', name:'商品名（日本語）', en:'Product Name (English)',
    price:0000, size:'500ml',
    url: ITEM_BASE + '000000000XXX',
    image: IMG_BASE + '000000000XXX_HASHHASH.jpg',
    matches:['daily'], coats:['all'],
    desc:'商品の特徴を1〜2文で。' },
```

## コンディショナー用テンプレート

```javascript
  { id:'pp_XXXXX', cat:'conditioner', name:'商品名', en:'Product Name',
    price:0000, size:'250ml',
    url: ITEM_BASE + '000000000XXX',
    image: IMG_BASE + '000000000XXX_HASHHASH.jpg',
    matches:['low_moisture','daily'], coats:['all'],
    desc:'商品の特徴を1〜2文で。' },
```

## フィニッシング用テンプレート

```javascript
  { id:'pp_XXXXX', cat:'finishing', name:'商品名', en:'Product Name',
    price:0000, size:'225g',
    url: ITEM_BASE + '000000000XXX',
    image: IMG_BASE + '000000000XXX_HASHHASH.jpg',
    matches:['show_prep'], coats:['all'],
    desc:'商品の特徴を1〜2文で。' },
```

## ブラシ用テンプレート

```javascript
  { id:'pp_XXXXX', cat:'brush', name:'商品名', en:'Brush Name',
    price:0000, size:'',
    url: ITEM_BASE + '000000000XXX',
    image: IMG_BASE + '000000000XXX_HASHHASH.jpg',
    matches:['daily','matting'], coats:['all'],
    desc:'ブラシの特徴を1〜2文で。' },
```

---

## 書き換える項目

| 書き換え対象 | 内容 |
|------------|------|
| `pp_XXXXX` | 内部ID（他と被らない名前。`pp_` で始める） |
| `商品名` | 日本語商品名 |
| `Product Name` | 英語商品名 |
| `0000` (price) | 価格（カンマなしの数字。税込価格） |
| `500ml` (size) | 容量・サイズ |
| `000000000XXX` (url) | plushpuppyjapan.com の商品ID（12桁） |
| `000000000XXX_HASHHASH.jpg` (image) | 画像ファイル名（商品ID＋ハッシュ） |
| `matches` | 適合する症状（複数可） |
| `coats` | 適合するコートタイプ |
| `desc` | 商品説明（1〜2文） |

---

## 商品IDと画像URLの調べ方

### 1. 商品IDの調べ方

plushpuppyjapan.com の該当商品ページを開き、URLを確認:

```
https://www.plushpuppyjapan.com/view/item/000000000200?...
                                           ↑
                                  この12桁が商品ID
```

### 2. 画像URLの調べ方

同じ商品ページで:

1. 商品画像を**右クリック**
2. 「画像URLをコピー」を選択
3. URLが以下の形式になっているはず:
   ```
   https://makeshop-multi-images.akamaized.net/PlushPuppyJP/itemimages/000000000200_AbCdEfG.jpg
                                                                       ↑
                                                          この部分（商品ID＋ハッシュ.jpg）
   ```
4. `/itemimages/` 以降の `000000000200_AbCdEfG.jpg` の部分だけをコピー

---

## 入力例（実在の商品）

```javascript
  { id:'pp_lets_face_it', cat:'shampoo', name:'洗顔シャンプー レッツ フェイス イット', en:"Let's Face It",
    price:3740, size:'250ml',
    url: ITEM_BASE + '000000000034',
    image: IMG_BASE + '000000000034_c8ceaIG.jpg',
    matches:['sensitive_skin','daily'], coats:['all'],
    desc:'目元・顔専用の低刺激処方。涙やけや目周りの汚れを優しくケア。' },
```

---

## matches に指定できる値の一覧

| 値 | 意味 |
|----|------|
| `'low_shine'` | 艶不足 |
| `'low_moisture'` | 乾燥 |
| `'oily'` | 油分過多 |
| `'breakage'` | 毛切れ |
| `'matting'` | 毛玉 |
| `'low_volume'` | ボリューム不足 |
| `'static'` | 静電気 |
| `'yellowing'` | 白毛のくすみ |
| `'sensitive_skin'` | 敏感肌 |
| `'shedding'` | 換毛期 |
| `'soft_coat'` | コートが柔らかすぎ |
| `'all_good'` | 良好（維持ケア） |
| `'daily'` | 日常ケア |
| `'show_prep'` | ショー準備 |
| `'white'` | 白毛向け |

## coats に指定できる値の一覧

→ `update-products.md` を参照
