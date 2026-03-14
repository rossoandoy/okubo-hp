# 1. ドキュメント一覧およびGitリポジトリ構成

## 1-1. ドキュメント一覧（成果物リスト）

### A. 企画・要件（上流）
1. プロジェクト概要書（背景／目的／スコープ／体制／前提）
2. 目的・KGI/KPI定義書（成功指標／GA4で測る指標）
3. ペルソナ・主要導線設計書（想定閲覧者別の導線）
4. サイトマップ／IA（URL設計・ナビ構成）
5. コンテンツ要件定義書（掲載範囲・素材一覧・提供形式）
6. 業績（Publications）要件定義書（カテゴリ・表示ルール・入力項目）
7. 非機能要件定義書（レスポンシブ／性能／アクセシビリティ／対応ブラウザ）
8. 運用要件定義書（教授編集→レビュー→公開反映／役割分担）

### B. 技術・アーキテクチャ
9. 技術仕様書（採用技術スタック詳細：バージョン方針・理由・制約）
10. システム構成・技術アーキテクチャ仕様書（構成図・環境・データ所在）
11. リポジトリ仕様書（構成、命名規則、ブランチ戦略、権限）
12. セキュリティ仕様書（2FA、Branch protection、Secrets、依存脆弱性対策）

### C. UI/UX・デザイン
13. ワイヤーフレーム（Top／Research／Publications／Join us／Contact／News）
14. デザインガイドライン（トーン、タイポ、余白、アクセシビリティ）
15. コンポーネント設計書（ヘッダ・フッタ・カード・業績リスト等）

### D. CMS（ブラウザ編集）
16. CMS運用設計書（教授向け：編集〜PR作成〜確認の流れ）
17. コンテンツモデル定義書（Pages／News／Publicationsのフィールド定義）
18. CMS設定設計書（Decap CMS config設計、メディア管理）
19. 入力ガイド（教授向け：例・注意点・よくあるミス）

### E. 計測・監視・品質
20. GA4実装設計書（イベント定義、命名規則、検証手順）
21. Sentry実装設計書（PII方針、通知、サンプリング）
22. CI品質ゲート仕様書（ビルド、リンク、Lighthouse、全角検知、画像上限）
23. テスト計画書（表示、計測、回帰、受入観点）

### F. リリース・デプロイ・復旧
24. ビルド＆リリース手順書（タグ、リリースノート、成果物ZIP生成）
25. デプロイ手順書（方式A: ZIP+Cyberduck／方式B: CI自動反映※後日決定）
26. ロールバック手順書（直前成果物の復旧、判断基準）

### G. 運用・ガバナンス
27. 運用ルール（ハンドブック：PRルール、公開反映、緊急対応）
28. 権限・アカウント管理台帳（GitHub、2FA、引継ぎ）
29. コンテンツポリシー（著作権・個人情報・公開可否判断フロー）
30. バックアップ／アーカイブ方針（repo、成果物、公開状態）

### H. AI支援（提案→人が採用）
31. AI支援機能設計書（PR要約、表記ゆれ指摘、週次サマリ）
32. AIガードレール設計（自動改変禁止、PII/著作権検知、通知）
33. 改善バックログ運用（KPI変動・異常検知→Issue化）

---

## 1-2. Gitリポジトリ構成（推奨）

> 想定：静的サイト（Astro/Next static等） + Decap CMS + CI（GitHub Actions） + GA4/Sentry

### ルート構成（例）
- README.md
- docs/
  - 00_overview.md
  - 01_kpi.md
  - 02_ia_sitemap.md
  - 03_content_requirements.md
  - 04_publications_requirements.md
  - 10_tech_spec.md
  - 11_architecture.md
  - 12_repo_security.md
  - 20_ga4_spec.md
  - 21_sentry_spec.md
  - 22_ci_quality_gate.md
  - 24_release.md
  - 25_deploy.md
  - 26_rollback.md
  - 27_ops_handbook.md
  - templates/
  - **実装制御文書**: PLAN.md, SPEC.md, TODO.md, KNOWLEDGE.md（リポジトリ内 docs/ を参照）
- src/
  - pages/
  - components/
  - layouts/
  - styles/
- public/
  - assets/
  - images/
- content/
  - pages/
  - news/
  - publications/
- admin/
  - index.html
  - config.yml
- scripts/
  - check-filenames.js
  - check-links.js
- .github/
  - workflows/
    - pr-check.yml
    - build-release.yml
- package.json
- pnpm-lock.yaml（or package-lock.json）
- .editorconfig
- .gitignore

### 運用上の重要ルール（repoに明記）
- 全角ファイル名禁止（CIで検知）
- main直push禁止（PR必須）
- PRでビルド成功＋品質ゲート通過が必須
- 成果物ZIPはReleaseまたはArtifactsに必ず残す（ロールバック用）

---

## 1-3. ブランチ/レビュー運用（要点だけ）
- 教授：CMSで更新（ブランチ or PR作成）
- あなた：PRレビュー（見た目/内容/著作権/リンク）→マージ
- CI：成果物生成（ZIP）
- あなた：公開反映（慶應サーバへアップ）

