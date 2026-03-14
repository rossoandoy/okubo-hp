# 実装状況記録：CV 頁廃止・ナビ整合・デプロイ

親リポジトリ（okubo）に残す記録。実施日・対象・変更内容・デプロイ結果をまとめる。

---

## 概要

- **対象リポジトリ**: `professor-s-keio-portal`（大久保教授 Keio ポータル）
- **実施内容**: CV ページ廃止、グローバルナビをトップページ構成と一致、サイトマップ追加、GitHub Pages へのデプロイ
- **参照計画**: `.cursor/plans/cv頁廃止・ナビ整合・codexデザインレビュー_8ebcaa30.plan.md`（修正版。PDF ダウンロードは不要とする前提）

---

## 実施した変更（professor-s-keio-portal）

### 1. ナビの整合

- **変更前**: Research | Publications（Selected, By topic）| **CV** (/cv) | Contact
- **変更後**: **Research**（/#research）| **Publications**（Selected /#publications, By topic /by-topic）| **Career**（/#career）| **Contact**（/#contact）
- トップページの構成（Hero → Research → Publications → Career → Contact）とナビの項目・並びを一致させた。
- 変更ファイル: `src/components/Navigation.tsx`（mainNavItems およびモバイルメニュー）

### 2. CV ページの廃止

- `/cv` ルートおよび `CvPage.tsx` を削除。
- 経歴・学歴・委員等は従来どおりトップの **Career セクション**（`CareerSection.tsx`）で `src/data/cvContent.ts` を参照して表示。CV 用データは残置。
- 変更ファイル: `src/App.tsx`（/cv ルート・CvPage の import 削除）、`src/pages/CvPage.tsx`（削除）

### 3. 論文検索の導線

- Publications セクションの「Search all (CV)」を「Search all」にし、リンク先を `/cv` から **/by-topic** に変更。
- 変更ファイル: `src/components/PublicationsSection.tsx`

### 4. サイトマップ

- サイトマップページ（`/sitemap`）を追加。フッターに「Site map」/「サイトマップ」リンクを追加。
- 変更ファイル: `src/pages/SitemapPage.tsx` 新規、`src/App.tsx` にルート追加、`src/components/Footer.tsx` にリンク追加。Sitemap 上では CV は廃止し Career は Home 内アンカーとして記載。

### 5. データ・ドキュメント

- `src/data/cvContent.ts`: CareerSection 用に維持（コメントを「Used by CareerSection」に更新）。
- `docs/DESIGN_REVIEW.md`: デザインレビュー（手動チェックリスト）の結果を記録。
- `docs/CV_REVIEW.md`: 既存の CV 関連レビュー記録（存在する場合）。

---

## デプロイ

- **方式**: GitHub Actions（`.github/workflows/deploy-pages.yml`）。`main` への push でビルドし、GitHub Pages にデプロイ。
- **実施**: 上記変更をコミットし、`professor-s-keio-portal` の `origin main` に push 済み（コミット: `CV頁廃止・ナビ整合: Research/Publications/Career/Contact、Search all→/by-topic、サイトマップ追加`）。
- **確認**:  
  - ワークフロー: https://github.com/rossoandoy/professor-s-keio-portal/actions  
  - 公開 URL: リポジトリの Settings → Pages に記載（例: `https://rossoandoy.github.io/professor-s-keio-portal/`）。

---

## 補足

- CV 用 PDF のダウンロードは計画どおり設けていない（`public/cv.pdf` の配置・リンクは行っていない）。
- 計画ファイル（.cursor/plans/ 内）は編集していない。
- By Topic ページ（/by-topic）は従来どおり。全論文検索はここに集約。
