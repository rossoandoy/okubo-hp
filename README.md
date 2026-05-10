# Okubo Lab — プロジェクト管理リポジトリ

大久保敏弘教授（慶應義塾大学 経済学部）のウェブサイトプロジェクトの親リポジトリ。
企画・仕様ドキュメントと、サイト本体のサブモジュールを管理する。

---

## サイト本体

| リポジトリ | 用途 | 技術スタック |
|---|---|---|
| **[professor-s-keio-portal](https://github.com/rossoandoy/professor-s-keio-portal)** | 慶應ポータル（正規サイト） | React + Vite + Tailwind + shadcn/ui |
| [okubo-personal-page](https://github.com/rossoandoy/okubo-personal-page) | 個人ページ（別プロジェクト） | React + Express |

**正規サイトは `professor-s-keio-portal`** です。開発・コンテンツ更新はそちらで行ってください。

## コンテンツ管理 (CMS)

教授がブラウザからコンテンツを更新できます:

1. [Pages CMS](https://pagescms.org) にアクセス
2. GitHub アカウントでログイン
3. `professor-s-keio-portal` を選択
4. Publications / News / Hero / Contact 等を編集・保存

詳細: [professor-s-keio-portal/docs/CMS_GUIDE.md](https://github.com/rossoandoy/professor-s-keio-portal/blob/main/docs/CMS_GUIDE.md)

## ドキュメント（このリポジトリ）

| ファイル | 内容 |
|---|---|
| `1_ドキュメント一覧とgitリポジトリ構成.md` | 成果物一覧・リポジトリ構成 |
| `2_システム構成・技術アーキテクチャ仕様書.md` | 全体アーキテクチャ・構成図 |
| `3_環境構築手順書.md` | 開発環境セットアップ手順 |
| `a_企画・要件定義書一式（大久保教授hp）.md` | 企画・KPI・ペルソナ・要件 |

## クローン方法

```bash
# サブモジュールも含めて取得
git clone --recurse-submodules https://github.com/rossoandoy/okubo-hp.git

# サブモジュールが空の場合
cd okubo-hp
git submodule update --init --recursive
```

## デプロイ

- **GitHub Pages**: `professor-s-keio-portal` の main に push すると自動デプロイ
- **慶應サーバー**: `npm run build:keio` → ZIP を Cyberduck で `public_html` に配置
