# GraphQL React Todo App

GraphQL、React、Prismaを使用したモダンなTodoアプリケーションです。

## 📺 参考動画

このプロジェクトは[こちらのYouTube動画](https://www.youtube.com/watch?v=PzBsTUZo12s)を参考にして作成しました

## 📝 動画との差分

- **Tailwind CSS**: 3系 → 4系にアップグレード
- **Delete機能**: 動画にはない独自追加機能
  
  <img width="457" alt="スクリーンショット 2025-06-18 13 09 44" src="https://github.com/user-attachments/assets/ca276688-6908-4e2c-b01d-2984fb015586" />

## ✨ 機能

- ✅ タスクの追加
- ✅ タスクの完了/未完了の切り替え
- ✅ タスクの削除（独自追加機能）
- ✅ リアルタイムなUI更新
- ✅ レスポンシブデザイン
- ✅ アニメーション効果

## 🛠️ 技術スタック

### フロントエンド

- **React 18** - UIライブラリ
- **TypeScript** - 型安全性
- **Apollo Client** - GraphQLクライアント
- **Tailwind CSS 4系** - スタイリング（動画では3系でしたが4系にアップグレード）
- **Vite** - ビルドツール
- **Framer Motion** - アニメーション
- **Lucide React** - アイコン

### バックエンド

- **Node.js** - サーバーランタイム
- **TypeScript** - 型安全性
- **Apollo Server** - GraphQLサーバー
- **Prisma** - ORM
- **SQLite** - データベース

### 開発ツール

- **ESLint** - コード品質
- **PostCSS** - CSS処理
- **Nodemon** - サーバー自動再起動

## 🚀 セットアップ

### 前提条件

- Node.js (v16以上)
- npm または yarn

### インストール

1. リポジトリをクローン

```bash
git clone <repository-url>
cd graphql-react
```

2. 依存関係のインストール

**バックエンド:**

```bash
cd graphql-server
npm install
```

**フロントエンド:**

```bash
cd ../todo-client
npm install
```

3. データベースのセットアップ

```bash
cd ../graphql-server
npx prisma migrate dev
```

## 🏃‍♂️ 実行

### 開発環境での起動

**バックエンドサーバーの起動:**

```bash
cd graphql-server
npm run start
```

→ GraphQLサーバーが `http://localhost:4000` で起動

**フロントエンドの起動:**

```bash
cd todo-client
npm run dev
```

→ Reactアプリが `http://localhost:5173` で起動
