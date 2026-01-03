<!--
GENERATED FILE — DO NOT EDIT.
SSOT: /Spec.md
Run: powershell -ExecutionPolicy Bypass -File scripts/sync-spec.ps1
-->
# Miserba - ポートフォリオ自動生成アプリ 要件定義書（SSOT）

> **Single Source of Truth (SSOT)**
> このドキュメントは Miserba プロジェクトの唯一の真実の情報源です。
> 全ての開発判断はこのドキュメントに基づいて行います。

## 📋 プロジェクト概要

| 項目 | 内容 |
|------|------|
| プロダクト名 | **Miserba**（ミセルバ） |
| コンセプト | 生成AIを活用したポートフォリオ自動生成SaaS |
| ターゲット | @Makhmeto_AI のフォロワー（副業志望の20代、生成AI活用に興味がある層） |
| 開発手法 | SDD（Specification-Driven Development） |
| 開発ツール | Cursor |
| 対応プラットフォーム | Web（レスポンシブ対応）、PWA対応（スマホアプリライク） |

---

## 🎯 ターゲットユーザー分析

### メインターゲット
- **20代の副業志望者**
- プログラミング初心者〜中級者
- 生成AIに興味があるが、ポートフォリオ作成に時間をかけたくない人
- フリーランスや転職を目指している人
- SNS発信を通じて仕事を獲得したい人

### ユーザーペルソナ
```
名前: 田中さん（26歳・男性）
職業: 会社員（営業職）
副業: 生成AIを使ったWeb制作を学習中
課題: 
  - ポートフォリオを作りたいけど、デザインセンスがない
  - 時間がない（帰宅後2-3時間しかない）
  - どんな情報を載せればいいかわからない
  - 自分でコード書くのは大変
ニーズ:
  - 5分でポートフォリオを完成させたい
  - AIが自動で見栄えの良いデザインにしてほしい
  - スマホからも更新したい
  - 費用はできるだけ抑えたい（月1,000円以下）
```

---

## 💡 コア機能要件

### 1. AIポートフォリオ自動生成
**ユーザーの声: 「質問に答えるだけで、5分でポートフォリオが完成したら嬉しい」**

| 機能 | 詳細 |
|------|------|
| AIヒアリング | チャット形式で5-10個の質問に回答 |
| プロフィール自動生成 | 経歴・スキル・自己PRをAIが作成 |
| 実績セクション自動構成 | プロジェクト説明文をAIが最適化 |
| デザインテーマ自動選択 | ユーザーの業種・雰囲気に合わせて提案 |
| 多言語対応 | 日本語 / 英語 / ロシア語 / カザフ語 |

### 2. ノーコードエディター
**ユーザーの声: 「AIが作った後、自分で微調整もしたい」**

| 機能 | 詳細 |
|------|------|
| ドラッグ&ドロップ編集 | セクションの並び替え |
| リアルタイムプレビュー | 編集しながら即座に反映確認 |
| テキスト直接編集 | クリックして文章修正 |
| 画像アップロード | プロジェクト画像・プロフィール写真 |
| カラーテーマ変更 | ワンクリックで配色変更 |

### 3. 外部連携・インポート
**ユーザーの声: 「GitHubやQiitaの内容を自動で取り込んでほしい」**

| 連携先 | 取得情報 |
|--------|----------|
| GitHub | リポジトリ一覧、コントリビューション、使用言語 |
| Qiita | 記事一覧、いいね数、タグ |
| Zenn | 記事一覧、Book |
| Note | 記事タイトル・概要 |
| X (Twitter) | プロフィール情報（任意） |
| LinkedIn | 職歴（OAuth連携） |

### 4. 公開・共有機能
**ユーザーの声: 「URLをSNSでシェアして、すぐ見てもらいたい」**

| 機能 | 詳細 |
|------|------|
| カスタムURL | `miserba.com/username` 形式 |
| 独自ドメイン接続 | 有料プランで対応 |
| OGP自動生成 | SNSシェア時のサムネイル自動作成 |
| QRコード生成 | 名刺やイベントで使用 |
| PDFエクスポート | 履歴書形式での出力 |

### 5. アナリティクス
**ユーザーの声: 「誰がいつ見てくれたか知りたい」**

| 指標 | 詳細 |
|------|------|
| 閲覧数 | 日別・週別・月別 |
| 流入元 | SNS別、検索エンジン別 |
| 滞在時間 | セクション別の閲覧時間 |
| クリック率 | CTAボタン、リンクのクリック数 |

---

## 💳 課金機能（Stripe必須）

### プラン設計

| プラン | 月額 | 年額（20%OFF） | 機能 |
|--------|------|----------------|------|
| **Free** | ¥0 | - | 1ポートフォリオ、基本テンプレート3種、miserba.comサブドメイン、透かし表示 |
| **Pro** | ¥980 | ¥9,408 | 無制限ポートフォリオ、全テンプレート、カスタムURL、透かし非表示、アナリティクス |
| **Business** | ¥2,980 | ¥28,608 | Pro全機能 + 独自ドメイン、チーム機能（5名）、優先サポート、API連携 |

### Stripe実装要件

```yaml
必須機能:
  - サブスクリプション管理（月額/年額切替）
  - クレジットカード決済
  - 請求書自動発行
  - プラン変更（アップグレード/ダウングレード）
  - 解約処理
  - Webhook処理（支払い成功/失敗/解約）
  - 無料トライアル（14日間）
  - クーポンコード対応

セキュリティ:
  - PCI DSS準拠（Stripe側で対応）
  - カード情報は一切保持しない
  - Stripe Checkout または Elements 使用
```

---

## 🏗️ 技術スタック（確定事項）

### バックエンド
```yaml
Framework: FastAPI 0.115+
Language: Python 3.12+
ORM: SQLAlchemy 2.0 + Alembic（マイグレーション）
Database: PostgreSQL 16
Cache: Redis 7
Task Queue: Celery + Redis
認証: JWT + OAuth 2.0（Google, GitHub）
API仕様: OpenAPI 3.1（Swagger UI自動生成）
```

### フロントエンド
```yaml
Framework: React 18+ (Vite)
Language: TypeScript 5.x
State: Zustand（軽量状態管理）
Styling: Tailwind CSS 3.x + shadcn/ui
Form: React Hook Form + Zod
HTTP Client: TanStack Query (React Query) v5
Router: React Router v6
```

### インフラ
```yaml
Container: Docker + Docker Compose
Hosting:
  - Backend: Railway / Render / AWS ECS
  - Frontend: Vercel / Cloudflare Pages
  - Database: Supabase / Railway PostgreSQL
Storage: Cloudflare R2 / AWS S3（画像保存）
CDN: Cloudflare
CI/CD: GitHub Actions
Monitoring: Sentry（エラー監視）
```

### 外部サービス
```yaml
決済: Stripe
認証: Supabase Auth または 自前JWT + Google/GitHub OAuth
メール: Resend / SendGrid
AI: OpenAI GPT-4o-mini / Claude 3.5 Sonnet API
画像処理: Sharp（Node.js）/ Pillow（Python）
OGP生成: @vercel/og または Puppeteer
```

---

## 📁 ディレクトリ構成（推奨）

```
miserba/
├── backend/
│   ├── app/
│   │   ├── api/
│   │   │   ├── v1/
│   │   │   │   ├── auth.py
│   │   │   │   ├── users.py
│   │   │   │   ├── portfolios.py
│   │   │   │   ├── subscriptions.py
│   │   │   │   └── webhooks.py
│   │   │   └── deps.py
│   │   ├── core/
│   │   │   ├── config.py
│   │   │   ├── security.py
│   │   │   └── stripe.py
│   │   ├── models/
│   │   │   ├── user.py
│   │   │   ├── portfolio.py
│   │   │   └── subscription.py
│   │   ├── schemas/
│   │   ├── services/
│   │   │   ├── ai_generator.py
│   │   │   └── github_import.py
│   │   └── main.py
│   ├── alembic/
│   ├── tests/
│   ├── Dockerfile
│   └── requirements.txt
│
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   │   ├── ui/              # shadcn/ui components
│   │   │   ├── portfolio/
│   │   │   └── editor/
│   │   ├── features/
│   │   │   ├── auth/
│   │   │   ├── dashboard/
│   │   │   ├── editor/
│   │   │   └── billing/
│   │   ├── hooks/
│   │   ├── lib/
│   │   │   ├── api.ts
│   │   │   └── stripe.ts
│   │   ├── stores/
│   │   └── App.tsx
│   ├── public/
│   ├── Dockerfile
│   └── package.json
│
├── docker-compose.yml
├── .github/
│   └── workflows/
│       ├── ci.yml
│       └── deploy.yml
└── README.md
```

---

## 🗄️ データベース設計

### ER図（主要テーブル）

```
┌─────────────┐     ┌─────────────────┐     ┌──────────────┐
│   users     │────<│   portfolios    │     │subscriptions │
├─────────────┤     ├─────────────────┤     ├──────────────┤
│ id (PK)     │     │ id (PK)         │     │ id (PK)      │
│ email       │     │ user_id (FK)    │     │ user_id (FK) │
│ name        │     │ title           │     │ stripe_sub_id│
│ avatar_url  │     │ slug            │     │ plan         │
│ provider    │     │ template        │     │ status       │
│ provider_id │     │ content (JSON)  │     │ current_end  │
│ created_at  │     │ is_published    │     │ created_at   │
│ updated_at  │     │ views_count     │     │ updated_at   │
└─────────────┘     │ created_at      │     └──────────────┘
                    │ updated_at      │
                    └─────────────────┘
                           │
                           │
                    ┌──────────────────┐
                    │ portfolio_views  │
                    ├──────────────────┤
                    │ id (PK)          │
                    │ portfolio_id(FK) │
                    │ visitor_ip       │
                    │ user_agent       │
                    │ referrer         │
                    │ viewed_at        │
                    └──────────────────┘
```

### 主要テーブル定義

```sql
-- users テーブル
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    email VARCHAR(255) UNIQUE NOT NULL,
    name VARCHAR(100),
    avatar_url TEXT,
    provider VARCHAR(20), -- 'google', 'github', 'email'
    provider_id VARCHAR(255),
    stripe_customer_id VARCHAR(255),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- portfolios テーブル
CREATE TABLE portfolios (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID REFERENCES users(id) ON DELETE CASCADE,
    title VARCHAR(100) NOT NULL,
    slug VARCHAR(50) UNIQUE NOT NULL,
    template VARCHAR(50) DEFAULT 'default',
    content JSONB NOT NULL DEFAULT '{}',
    settings JSONB DEFAULT '{}',
    is_published BOOLEAN DEFAULT FALSE,
    views_count INTEGER DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- subscriptions テーブル
CREATE TABLE subscriptions (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID REFERENCES users(id) ON DELETE CASCADE,
    stripe_subscription_id VARCHAR(255) UNIQUE,
    stripe_price_id VARCHAR(255),
    plan VARCHAR(20) NOT NULL, -- 'free', 'pro', 'business'
    status VARCHAR(20) NOT NULL, -- 'active', 'canceled', 'past_due'
    current_period_start TIMESTAMP,
    current_period_end TIMESTAMP,
    cancel_at_period_end BOOLEAN DEFAULT FALSE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

---

## 🔐 API エンドポイント設計

### 認証 API
```
POST   /api/v1/auth/signup          # メール登録
POST   /api/v1/auth/login           # ログイン
POST   /api/v1/auth/logout          # ログアウト
POST   /api/v1/auth/refresh         # トークン更新
GET    /api/v1/auth/google          # Google OAuth
GET    /api/v1/auth/github          # GitHub OAuth
POST   /api/v1/auth/forgot-password # パスワードリセット
```

### ユーザー API
```
GET    /api/v1/users/me             # 自分の情報取得
PATCH  /api/v1/users/me             # プロフィール更新
DELETE /api/v1/users/me             # アカウント削除
```

### ポートフォリオ API
```
GET    /api/v1/portfolios           # 一覧取得
POST   /api/v1/portfolios           # 新規作成
GET    /api/v1/portfolios/{id}      # 詳細取得
PATCH  /api/v1/portfolios/{id}      # 更新
DELETE /api/v1/portfolios/{id}      # 削除
POST   /api/v1/portfolios/{id}/publish    # 公開
POST   /api/v1/portfolios/{id}/unpublish  # 非公開
GET    /api/v1/portfolios/{id}/analytics  # 分析データ
```

### AI生成 API
```
POST   /api/v1/ai/generate          # ポートフォリオ生成
POST   /api/v1/ai/improve           # 文章改善
POST   /api/v1/ai/translate         # 翻訳
```

### 外部連携 API
```
GET    /api/v1/import/github        # GitHub連携
GET    /api/v1/import/qiita         # Qiita連携
POST   /api/v1/import/qiita/sync    # Qiita同期
```

### 課金 API（Stripe）
```
GET    /api/v1/billing/plans        # プラン一覧
POST   /api/v1/billing/checkout     # Checkout Session作成
POST   /api/v1/billing/portal       # カスタマーポータル
GET    /api/v1/billing/subscription # サブスク状態取得
POST   /api/v1/webhooks/stripe      # Stripe Webhook
```

### 公開ページ API
```
GET    /p/{slug}                    # 公開ポートフォリオ表示
```

---

## 🎨 UI/UX 要件

### デザイン原則
1. **シンプル・ミニマル**: 余計な装飾を排除
2. **モバイルファースト**: スマホでの操作を最優先
3. **即座のフィードバック**: 操作結果を即時反映
4. **アクセシビリティ**: WCAG 2.1 AA準拠

### 画面一覧

| 画面名 | パス | 説明 |
|--------|------|------|
| LP | `/` | サービス紹介・料金プラン |
| ログイン | `/login` | メール/Google/GitHub |
| 新規登録 | `/signup` | アカウント作成 |
| ダッシュボード | `/dashboard` | ポートフォリオ一覧 |
| 新規作成（AI） | `/create` | AI質問フロー |
| エディター | `/edit/{id}` | ポートフォリオ編集 |
| プレビュー | `/preview/{id}` | プレビュー表示 |
| 設定 | `/settings` | アカウント設定 |
| 課金 | `/billing` | プラン管理 |
| 公開ページ | `/p/{slug}` | 公開ポートフォリオ |

### レスポンシブブレークポイント
```css
/* Tailwind CSS デフォルト */
sm: 640px   /* スマホ横向き */
md: 768px   /* タブレット */
lg: 1024px  /* 小型PC */
xl: 1280px  /* デスクトップ */
```

---

## 🔒 セキュリティ要件

### 認証・認可
- JWT有効期限: アクセストークン15分、リフレッシュトークン7日
- HTTPOnly Cookie でトークン管理
- CORS設定を本番ドメインのみ許可
- Rate Limiting: API 100req/min/IP

### データ保護
- パスワードハッシュ: bcrypt（コスト12）
- 通信: HTTPS必須（TLS 1.3）
- 機密情報: 環境変数管理（.env）
- SQLインジェクション: SQLAlchemy ORM使用

### Stripe セキュリティ
- Webhook署名検証必須
- カード情報はStripe側で管理（PCI DSS準拠）
- テスト環境と本番環境の完全分離

---

## 🚀 MVP（最小実行可能プロダクト）スコープ

### Phase 1: MVP（4週間）
- [x] ユーザー認証（メール + Google OAuth）
- [x] ポートフォリオ作成（手動入力）
- [x] 基本テンプレート 3種類
- [x] 公開URL生成
- [x] Stripe課金（Free/Pro）

### Phase 2: AI強化（+2週間）
- [ ] AI質問フロー
- [ ] プロフィール自動生成
- [ ] 文章改善機能

### Phase 3: 連携機能（+2週間）
- [ ] GitHub連携
- [ ] Qiita/Zenn連携
- [ ] OGP自動生成

### Phase 4: 成長機能（+2週間）
- [ ] アナリティクス
- [ ] PDFエクスポート
- [ ] 独自ドメイン対応

---

## 📊 KPI・成功指標

| 指標 | 目標（3ヶ月後） |
|------|-----------------|
| 登録ユーザー数 | 1,000人 |
| 有料転換率 | 5%（50人） |
| MRR | ¥49,000（50人 × ¥980） |
| ポートフォリオ作成数 | 1,500件 |
| DAU/MAU | 20% |

---

## 📝 開発ルール

### Git運用
- ブランチ戦略: GitHub Flow
- コミットメッセージ: Conventional Commits
- PRテンプレート必須
- mainマージは自動デプロイ

### コード品質
- Linter: ESLint + Prettier（Frontend）, Ruff + Black（Backend）
- 型チェック: TypeScript strict mode, mypy
- テストカバレッジ: 80%以上
- コードレビュー必須

### ドキュメント
- APIドキュメント: OpenAPI自動生成
- README.md更新必須
- 変更履歴: CHANGELOG.md

---

## 🤝 参考・競合サービス

| サービス | 特徴 | 価格帯 |
|----------|------|--------|
| Canva Portfolio | ノーコード、テンプレート豊富 | 無料〜¥1,500/月 |
| Notion Sites | Notionから簡単公開 | 無料〜 |
| Pixpa | クリエイター向け | $8〜/月 |
| Format | 写真家向け | $8〜/月 |

### Miserbaの差別化ポイント
1. **AI自動生成に特化**: 質問に答えるだけで完成
2. **日本市場特化**: Qiita/Zenn連携、日本語最適化
3. **圧倒的低価格**: ¥980/月（競合の半額以下）
4. **副業者向け**: 生成AI活用層にリーチ

---

## 📞 サポート方針

- **Free**: ヘルプセンター（FAQ）のみ
- **Pro**: メールサポート（48時間以内返信）
- **Business**: 優先サポート（24時間以内返信）、Slackサポート

---

## 📅 マイルストーン

| マイルストーン | 期日 | 内容 |
|----------------|------|------|
| 設計完了 | Week 1 | DB設計、API設計、UI設計 |
| MVP開発 | Week 4 | 基本機能実装完了 |
| α版リリース | Week 5 | 内部テスト開始 |
| β版リリース | Week 6 | 限定ユーザーテスト |
| 正式リリース | Week 8 | 一般公開 |

---

> **最終更新日**: 2025年1月4日
> **バージョン**: 1.0.0
> **作成者**: @Makhmeto_AI

---

## 変更履歴

| 日付 | バージョン | 変更内容 |
|------|-----------|----------|
| 2025-01-04 | 1.0.0 | 初版作成 |

