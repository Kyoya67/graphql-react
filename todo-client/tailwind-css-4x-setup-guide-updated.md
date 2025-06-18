# 【2025年版】Tailwind CSS 4.x で「npx tailwindcss init -p」が動かない理由と解決方法

## はじめに

Tailwind CSS をプロジェクトに導入しようとして、お馴染みの
`npx tailwindcss init -p` コマンドを実行したら...

```bash
npm error could not determine executable to run
```

「**意味わからん。何で？**」

そんな経験をした方、多いのではないでしょうか？実は、Tailwind CSS 4.x
では従来の設定方法が大幅に変更されています。この記事では、その理由と正しい解決方法を解説します。

## 何が変わったのか？

### 従来（Tailwind CSS 3.x まで）

```bash
# これが普通に動いていた
npx tailwindcss init -p
```

### 現在（Tailwind CSS 4.x 以降）

```bash
# これがエラーになる！
npx tailwindcss init -p
# → npm error could not determine executable to run
```

## 原因：アーキテクチャの大幅変更

Tailwind CSS 4.x では以下の変更が行われました：

1. **CLI コマンドの廃止**: `npx tailwindcss init` コマンドが使用不可に
2. **PostCSS プラグインの分離**: PostCSS プラグインが別パッケージ
   `@tailwindcss/postcss` に移動
3. **手動設定が必要**: 設定ファイルを手動で作成する必要がある
4. **CSS インポート方法の変更**: 新しい `@import` 記法が推奨

## 解決方法

### ステップ 1: 必要なパッケージをインストール

```bash
# Tailwind CSS 本体とPostCSSプラグインをインストール
npm install -D tailwindcss@latest postcss@latest autoprefixer@latest @tailwindcss/postcss
```

### ステップ 2: 設定ファイルを手動で作成

#### `tailwind.config.js`

```javascript
/** @type {import('tailwindcss').Config} */
export default {
    content: [
        "./index.html",
        "./src/**/*.{js,ts,jsx,tsx}",
    ],
    theme: {
        extend: {},
    },
    plugins: [],
};
```

#### `postcss.config.js`

```javascript
export default {
    plugins: {
        "@tailwindcss/postcss": {},
        autoprefixer: {},
    },
};
```

### ステップ 3: CSS ファイルの設定（2つの方法）

#### 方法1: 新しい `@import` 記法（推奨）

`src/index.css`（またはメインのCSSファイル）で：

```css
@import "tailwindcss";

/* 既存のスタイル */
```

#### 方法2: 従来の `@tailwind` ディレクティブ

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

/* 既存のスタイル */
```

:::message **どちらを選ぶべき？**

- **新規プロジェクト**: `@import "tailwindcss";` を推奨
- **既存プロジェクト**: 従来の方法でも動作します :::

## よくあるエラーと対処法

### エラー 1: PostCSS プラグインエラー

```
[postcss] It looks like you're trying to use `tailwindcss` directly as a PostCSS plugin. 
The PostCSS plugin has moved to a separate package...
```

**解決方法**: `@tailwindcss/postcss`
パッケージをインストールして、`postcss.config.js` を正しく設定する。

### エラー 2: 実行ファイルが見つからない

```
npm error could not determine executable to run
```

**解決方法**: CLI コマンドは廃止されているので、手動で設定ファイルを作成する。

### エラー 3: スタイルが適用されない

**解決方法**: CSS ファイルで `@import "tailwindcss";` または `@tailwind`
ディレクティブが正しく記述されているか確認する。

## 動作確認

設定が完了したら、コンポーネントでTailwindクラスをテストしてみましょう：

```tsx
// App.tsx
function App() {
    return (
        <div className="min-h-screen bg-gray-100 flex items-center justify-center">
            <div className="bg-white p-8 rounded-lg shadow-md">
                <h1 className="text-3xl font-bold text-blue-600 mb-4">
                    Tailwind CSS 4.x セットアップ完了！
                </h1>
                <button className="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
                    ボタンテスト
                </button>
            </div>
        </div>
    );
}
```

## まとめ

Tailwind CSS 4.x での変更点：

- ❌ `npx tailwindcss init -p` コマンドは廃止
- ✅ 設定ファイルを手動で作成する
- ✅ `@tailwindcss/postcss` パッケージが必要
- ✅ `@import "tailwindcss";` の新記法が推奨
- ✅ 従来の `@tailwind` ディレクティブも使用可能

最初は「意味わからん」と思うかもしれませんが、一度設定してしまえば従来通り快適に使用できます。

## 参考リンク

- [Tailwind CSS 公式ドキュメント](https://tailwindcss.com/docs/installation)
- [Tailwind CSS GitHub リポジトリ](https://github.com/tailwindlabs/tailwindcss)
- [PostCSS 公式サイト](https://postcss.org/)

---

この記事が同じ問題で困っている方の助けになれば幸いです！質問やフィードバックがあれば、コメントでお気軽にどうぞ。
