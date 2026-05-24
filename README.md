# 🐩 Plush Puppy Coat Diagnosis

愛犬の被毛状態から最適なPlush Puppy製品を推奨するWeb診断ツール

[![Deploy to Render](https://render.com/images/deploy-to-render-button.svg)](https://render.com/deploy)

---

## 📋 概要

| 項目 | 内容 |
|------|------|
| 公開URL | （デプロイ後にRenderから発行されます） |
| ホスティング | [Render.com](https://render.com) (静的サイト・無料プラン) |
| ソース管理 | GitHub |
| 更新方法 | GitHub にコミット → Renderが自動再デプロイ |

---

## 🚀 初回セットアップ（GitHub → Render）

### ステップ 1: GitHub にリポジトリを作成

1. [GitHub](https://github.com) にログイン
2. 右上の **「+」** → **「New repository」**
3. 以下を入力:
   - Repository name: `plush-puppy-coat-clinic`
   - Description: `Plush Puppy 被毛診断ツール`
   - **Public** または **Private** を選択（PrivateでもRenderから接続可能）
   - **READMEは追加しない**（このプロジェクトに既にあるため）
4. 「Create repository」をクリック

### ステップ 2: ローカルからGitHubへPush

ターミナル（コマンドプロンプト）で以下を実行:

```bash
# このフォルダで開始
cd path/to/plush-puppy-coat-clinic-render

# Git初期化（既に初期化済みなら不要）
git init
git add .
git commit -m "Initial commit"

# GitHubと接続（YOUR-USERNAMEを実際のユーザー名に書き換え）
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/plush-puppy-coat-clinic.git
git push -u origin main
```

### ステップ 3: Render にサインアップ

1. [https://render.com](https://render.com) を開く
2. **「Get Started」** → GitHub アカウントでサインアップ
3. メールアドレス確認

### ステップ 4: Render から GitHub リポジトリをデプロイ

1. Renderダッシュボード → **「New +」**ボタン → **「Static Site」**
2. 「Connect a repository」で GitHub アカウントを連携
3. リポジトリ一覧から **`plush-puppy-coat-clinic`** を選択
4. 以下を確認・入力:

   | 項目 | 値 |
   |------|----|
   | **Name** | `plush-puppy-coat-clinic` （URL に使われます） |
   | **Branch** | `main` |
   | **Root Directory** | （空欄のまま） |
   | **Build Command** | （空欄のまま） |
   | **Publish Directory** | `.` （ピリオド1個、ルート直下） |

5. **「Create Static Site」**をクリック

→ 2〜3分で初回デプロイが完了し、以下のような URL が発行されます:

```
https://plush-puppy-coat-clinic.onrender.com
```

これが**永続的なURL**です。makeshopのiframeに指定するのもこのURLになります。

### ステップ 5: makeshop のフリーページに iframe を貼る

Render の URL を `embed-snippet.html` に書き込み、makeshop のフリーページに貼り付けます。

詳細は同梱の **`docs/makeshop-設置マニュアル.md`** をご参照ください。

---

## 🔄 更新方法（運用フロー）

商品情報の変更・新製品追加などを行う場合:

### 方法 A: ローカル → push（推奨）

```bash
# 1. ファイルを編集
# (例: index.html の PRODUCTS 配列を編集)

# 2. GitHub にプッシュ
git add .
git commit -m "feat: 新商品「サマー シャンプー」を追加"
git push

# 3. 完了
# Render が自動的に検知して 1〜2分で再デプロイ
# makeshop 側は何もしなくてOK（同じURLで配信）
```

### 方法 B: GitHub の Web UIから直接編集

1. GitHub のリポジトリページを開く
2. `index.html` をクリック
3. 右上の **鉛筆アイコン**（Edit）をクリック
4. ブラウザ上で編集
5. ページ下部の **「Commit changes」**ボタンをクリック
6. → 自動でRenderが再デプロイ

軽微な編集（価格変更1箇所など）には方法Bが便利です。

---

## 🛠 動作確認手順

デプロイ後、以下を確認してください:

1. Render が発行したURL（例 `https://plush-puppy-coat-clinic.onrender.com`）にブラウザでアクセス
2. 「Coat Diagnosis」というページが表示される
3. 何も入力せず「この内容で診断する」を押す
4. 4つの製品が推奨される + レーダーチャートが表示される
5. 商品画像（プラッシュパピーのボトル）が表示される
6. 「商品ページを見る」をクリックすると plushpuppyjapan.com の個別商品ページが開く

---

## 📂 ファイル構成

```
plush-puppy-coat-clinic/
├── README.md                  ← このファイル
├── index.html                 ← 診断ツール本体
├── assets/                    ← 静的アセット
│   ├── products.json          ← 商品マスタ（バックアップ）
│   ├── supplements.json       ← サプリ情報
│   └── vendor/
│       └── chart.umd.min.js   ← Chart.js ローカルコピー
│
├── render.yaml                ← Render自動構成設定
├── _headers                   ← HTTPヘッダー設定
├── .gitignore                 ← Git除外ファイル
│
└── docs/                      ← マニュアル
    ├── makeshop-設置マニュアル.md
    ├── 更新方法.md
    ├── トラブルシューティング.md
    └── design-tokens.md
```

---

## 🔒 Render プラン情報

| プラン | 価格 | 帯域幅 | 月間ビルド時間 | おすすめ |
|--------|------|--------|----------------|----------|
| **Free** | $0 | 100GB/月 | 500分/月 | ✅ このアプリには十分 |
| Starter | $7/月 | 100GB/月 | 500分/月 | 商用本格運用時 |

無料プランで以下も可能:
- ✅ カスタムドメイン (例 `diagnosis.plushpuppyjapan.com`)
- ✅ 自動SSL証明書
- ✅ Pull Request プレビュー

無料プランの制限:
- ⚠️ 15分間アクセスがないと**スリープ**する（次回アクセス時に2〜3秒遅延）
- → 商用利用時は **Starter プラン($7/月)** へのアップグレードを推奨

---

## 🆘 サポート・連絡先

| 項目 | 内容 |
|------|------|
| 開発元 | Resolution Engine Inc. |
| 監修 | 上手 健太郎 獣医師 |
| 連携サプリ | [CanineVet](https://www.caninevet.jp) |
| 製品提供 | [Plush Puppy Japan](https://www.plushpuppyjapan.com) |

技術的な質問は開発元までお問い合わせください。
