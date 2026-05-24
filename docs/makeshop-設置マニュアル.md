# makeshop への設置マニュアル

Render にデプロイされた診断ツールを、makeshop の **plushpuppyjapan.com** に埋め込む手順です。

---

## 前提

- ✅ GitHub にこのリポジトリが push 済み
- ✅ Render で初回デプロイが完了
- ✅ Render の URL を取得済み（例: `https://plush-puppy-coat-clinic.onrender.com`）

まだの方は **`../README.md`** の「初回セットアップ」をご参照ください。

---

## 📋 ステップ 1: Render URL の確認

1. [Render ダッシュボード](https://dashboard.render.com) を開く
2. `plush-puppy-coat-clinic` サービスをクリック
3. ページ上部に表示されるURL（例: `https://plush-puppy-coat-clinic.onrender.com`）をコピー

---

## 📋 ステップ 2: iframe 埋め込みコードを準備

以下のコードをコピーし、テキストエディタで開いてください:

```html
<!--
========================================================
  プラッシュパピー 被毛診断 (Render埋め込み版)
========================================================
-->

<div style="max-width:1100px; margin:0 auto; padding:0 16px;">
  <iframe
    id="ppCoatClinicFrame"
    src="https://plush-puppy-coat-clinic.onrender.com/index.html"
    style="width:100%; min-height:1200px; border:0; display:block;"
    title="プラッシュパピー 被毛診断"
    loading="lazy"
    scrolling="no"
    allowfullscreen></iframe>
</div>

<script>
(function () {
  var frame = document.getElementById('ppCoatClinicFrame');
  if (!frame) return;
  window.addEventListener('message', function (e) {
    // セキュリティ: Render のオリジンのみ受け入れる
    if (e.origin !== 'https://plush-puppy-coat-clinic.onrender.com') return;
    if (e.data && e.data.type === 'plushpuppy-coat-clinic-height') {
      var h = parseInt(e.data.height, 10);
      if (h && h > 0) {
        frame.style.height = (h + 20) + 'px';
      }
    }
  }, false);
})();
</script>
```

### ⚠️ 重要: URL を書き換える

上のコードの **2箇所** にある `https://plush-puppy-coat-clinic.onrender.com` を、**実際にRenderが発行したURL**に書き換えてください:

1. `iframe` の `src="..."` 部分
2. JavaScript内の `e.origin !== ...` 部分（セキュリティチェック）

たとえばRenderから `https://plush-puppy-diagnosis-abc123.onrender.com` を発行された場合、両方をそれに書き換えます。

---

## 📋 ステップ 3: makeshop にフリーページを作成

1. **makeshop管理画面** にログイン
2. 左メニュー → **「ショップデザイン」**
3. **「テンプレート選択・編集」** → **「フリーページ管理」**
4. **「ページ追加」** ボタンをクリック
5. 以下を入力:

   | 項目 | 値 |
   |------|----|
   | **ページURL** | `coat-diagnosis` （任意の半角英数字） |
   | **ページ名** | `被毛診断` |
   | **ページタイトル** | `被毛診断 \| Plush Puppy Japan` |

6. **本文入力欄** に、ステップ2で準備したコードを貼り付け
7. **「保存」** をクリック

---

## 📋 ステップ 4: 公開URL の確認

保存すると以下のURLで公開されます:

```
https://www.plushpuppyjapan.com/view/page/coat-diagnosis
```

このURLにアクセスし、診断ツールが表示されることを確認してください。

---

## 📋 ステップ 5: トップページからの導線を作成

お客様が診断ページに辿り着けるよう、トップページにバナーやメニューリンクを追加します。

### バナー設置例

makeshop のトップページに以下のような HTML を追加:

```html
<a href="/view/page/coat-diagnosis"
   style="display:inline-block; background:#43569f; color:white;
          padding:16px 40px; border-radius:28px; text-decoration:none;
          font-weight:700; letter-spacing:0.1em;">
  🐩 愛犬の被毛診断はこちら
</a>
```

### グローバルメニュー追加

makeshop 管理画面 → **「ショップデザイン」** → **「メニュー設定」** で以下を追加:

| 項目 | 値 |
|------|----|
| メニュー名 | 被毛診断 |
| リンク先 | `/view/page/coat-diagnosis` |

---

## ✅ 動作確認チェックリスト

設置後、以下を確認:

- [ ] PCのChrome で `https://www.plushpuppyjapan.com/view/page/coat-diagnosis` を開く
- [ ] 「Coat Diagnosis」「被毛診断」というタイトルが表示される
- [ ] フォームに入力できる
- [ ] 「この内容で診断する」ボタンを押すと診断結果が表示される
- [ ] 推奨製品の画像（プラッシュパピーのボトル）が表示される
- [ ] 「商品ページを見る」リンクが正しい商品ページに飛ぶ
- [ ] iframe の高さが自動調整されている（縦スクロールバーが二重に出ない）
- [ ] スマホ（iPhone Safari）でも正しく表示される

---

## 🔧 トラブルシューティング

### Q1: ページに何も表示されない

**A**:
- ブラウザの開発者ツール（F12）→ Console を見る
- 「Failed to load resource」とあれば Render URL が間違っている可能性
- ステップ2で URL を正しく書き換えたか再確認

### Q2: iframe の中身は表示されるが高さがおかしい

**A**:
- `e.origin !== ...` の部分の URL が正しいか確認
- 不一致だと postMessage が無視され、自動高さ調整が効かない

### Q3: スマホで横スクロールが発生する

**A**:
- iframe の `width` が `100%` になっているか確認
- 親要素の `max-width:1100px` が効いているか確認

### Q4: 「Render の URL を開くと数秒待たされる」

**A**:
- Render 無料プランは15分間アクセスがないとスリープします
- 初回アクセス時のみ2〜3秒の遅延が発生
- 商用本格運用時は Starter プラン($7/月) へのアップグレードを推奨

### Q5: makeshop でコードを貼ったら表示が崩れた

**A**:
- makeshop の HTML エディタが「自動整形」している可能性
- **HTML編集モード**で貼り付けたか確認
- ビジュアルエディタモードでは貼り付け不可

---

## 🔒 セキュリティについて

このセットアップは以下のセキュリティ対策を施しています:

| 対策 | 内容 |
|------|------|
| **Origin チェック** | postMessage を Render の URL からのみ受信 |
| **X-Frame-Options** | `ALLOWALL` で makeshop からの埋め込みを許可（Renderヘッダーで設定） |
| **rel="noopener"** | iframe 内のリンクは新規タブで開く設定 |
| **HTTPS 強制** | Render は自動で SSL 証明書を発行 |

---

## 📞 サポート

不明点があれば、開発元（Resolution Engine Inc.）までご連絡ください。
