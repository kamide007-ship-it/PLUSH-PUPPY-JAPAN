# 🚀 QUICK START - 5ステップでデプロイ

このプロジェクトを **GitHub → Render → makeshop** の流れで公開する最速手順です。

所要時間: 約15〜30分

---

## ✅ 必要なもの

事前に以下を準備してください:

- [ ] [GitHubアカウント](https://github.com)（無料）
- [ ] [Render.comアカウント](https://render.com)（無料、GitHubで連携可）
- [ ] makeshop管理画面へのログイン情報
- [ ] このプロジェクトのZIP（既にお手元にあるはず）

---

## STEP 1: GitHub にリポジトリを作成（5分）

1. [https://github.com/new](https://github.com/new) を開く
2. 以下を入力:
   - Repository name: **`plush-puppy-coat-clinic`**
   - Description: `Plush Puppy 被毛診断ツール`
   - **Public** を選択（PrivateでもOKだがPublicが楽）
   - **「Add a README file」 のチェックは外す** ⚠️
3. **「Create repository」**

→ 空っぽのリポジトリが作成されます。URLをコピーしておく:
```
https://github.com/YOUR-USERNAME/plush-puppy-coat-clinic
```

---

## STEP 2: ローカルから GitHub に Push（5分）

ターミナル（Windows: PowerShell / Mac: ターミナル.app）を開いて、このフォルダ内で実行:

```bash
# フォルダに移動
cd plush-puppy-coat-clinic-render

# Git 初期化
git init
git add .
git commit -m "Initial commit"

# GitHub と接続（YOUR-USERNAMEを書き換え）
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/plush-puppy-coat-clinic.git
git push -u origin main
```

**注意**: 初回push時、GitHubのユーザー名とパスワード（または Personal Access Token）を聞かれます。

→ GitHubのリポジトリページをリロードすると、ファイルが表示されます。

---

## STEP 3: Render でデプロイ（5分）

### 3-A. Render にサインアップ

1. [https://render.com](https://render.com) → **「Get Started for Free」**
2. **「GitHub」** で連携サインアップ（最も簡単）

### 3-B. 静的サイトを作成

1. Renderダッシュボード → **「New +」** ボタン → **「Static Site」**
2. **「Connect a repository」** で `plush-puppy-coat-clinic` を選択
3. 以下を確認・入力:

   | 項目 | 値 |
   |------|----|
   | Name | `plush-puppy-coat-clinic` |
   | Branch | `main` |
   | Root Directory | (空欄) |
   | Build Command | (空欄) |
   | Publish Directory | `.` |

4. **「Create Static Site」** をクリック

### 3-C. デプロイを待つ

「Deploy in progress...」と出るので2〜3分待つ。

→ 完了すると以下のような URL が発行されます:
```
https://plush-puppy-coat-clinic.onrender.com
```

**このURLをコピーしておく** ⭐

---

## STEP 4: makeshop に埋め込みコードを貼る（10分）

### 4-A. embed-snippet.html を編集

このフォルダ内の `embed-snippet.html` を **テキストエディタで開く**:

ファイル内の **2箇所** にある `YOUR-RENDER-URL.onrender.com` を、ステップ3で取得した実際のURLに**書き換える**:

```html
<!-- 修正前 -->
src="https://YOUR-RENDER-URL.onrender.com/index.html"
...
if (e.origin !== 'https://YOUR-RENDER-URL.onrender.com') return;

<!-- 修正後（例） -->
src="https://plush-puppy-coat-clinic.onrender.com/index.html"
...
if (e.origin !== 'https://plush-puppy-coat-clinic.onrender.com') return;
```

書き換えたら全選択（Ctrl+A → Ctrl+C）してコピー。

### 4-B. makeshop でフリーページ作成

1. makeshop管理画面 → **「ショップデザイン」** → **「テンプレート選択・編集」** → **「フリーページ管理」**
2. **「ページ追加」**
3. 以下を入力:

   | 項目 | 値 |
   |------|----|
   | ページURL | `coat-diagnosis` |
   | ページ名 | `被毛診断` |
   | ページタイトル | `被毛診断 \| Plush Puppy Japan` |

4. **本文入力欄** に、ステップ4-Aでコピーしたコードを貼り付け
5. **「保存」** をクリック

---

## STEP 5: 動作確認（5分）

### 5-A. 公開URLにアクセス

ブラウザで以下を開く:

```
https://www.plushpuppyjapan.com/view/page/coat-diagnosis
```

### 5-B. 確認項目

- [ ] 「Coat Diagnosis 被毛診断」のタイトルが表示される
- [ ] フォームが表示される
- [ ] 「この内容で診断する」を押すと結果が出る
- [ ] 推奨商品の画像が表示される
- [ ] スマホでも崩れずに表示される

---

## 🎉 公開完了！

これで愛犬の被毛診断ツールが公開されました。

---

## 📌 次のステップ

### バナー・メニューから誘導

makeshopのトップページに「愛犬の被毛診断」へのバナーを設置:

```html
<a href="/view/page/coat-diagnosis"
   style="display:inline-block; background:#43569f; color:white;
          padding:16px 40px; border-radius:28px; text-decoration:none;
          font-weight:700; letter-spacing:0.1em;">
  🐩 愛犬の被毛診断はこちら
</a>
```

### 商品情報を更新する

価格変更や新商品追加は GitHub から行います。
詳細は **`docs/更新方法.md`** をご参照ください。

### カスタムドメイン

`diagnosis.plushpuppyjapan.com` のような独自ドメインを使いたい場合は、
Render のダッシュボード → Settings → Custom Domain から設定できます。

---

## 🆘 困ったとき

| 症状 | 対処 |
|------|------|
| ページが真っ白 | `docs/トラブルシューティング.md` 参照 |
| 画像が出ない | `docs/トラブルシューティング.md` 参照 |
| 何度Pushしても更新されない | Renderダッシュボード → Events で状態確認 |
| ヘルプが必要 | 開発元（Resolution Engine Inc.）へ |

---

## 📚 詳しいマニュアル

- `README.md` … プロジェクト概要
- `docs/makeshop-設置マニュアル.md` … 設置の詳細
- `docs/更新方法.md` … 商品情報の更新方法
- `docs/トラブルシューティング.md` … 困った時に
- `docs/商品更新の詳しい手順.md` … 製品マスタの書き換え方
- `docs/design-tokens.md` … デザイン仕様
