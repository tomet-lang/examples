# Tomet Vault & Project Structure Examples

Tomet を導入する際、**「ディレクトリ構造をどう設計すべきか？」** をユーザーが悩まなくても済むように、代表的な2つのベストプラクティスをまとめたサンプル集です。

用途に合わせて、該当するディレクトリをそのままテンプレートとしてコピー＆ペーストして使用できます。

---

## 2つの推奨構成

| 用途 | ディレクトリ | スキーマ・設定の置き場所 | 特徴 |
| :--- | :--- | :--- | :--- |
| **個人知識管理 (PKM / メモ帳)** | [`pkm/`](./pkm) | `.tomet/`（隠しフォルダ） | ルート全体がノート空間。システム定義を隠して執筆に集中 |
| **アプリ開発・仕様書・チームWiki** | [`app-dev/`](./app-dev) | `tmtroot/schema/`（可視フォルダ） | ドキュメントを `tmtroot/` に集約。語彙やBlueprintを可視化して共同管理 |

---

## 1. 個人知識管理（PKM / メモ帳）: [`pkm/`](./pkm)

Obsidian のように「リポジトリ全体を思考のノート空間として使いたい」場合です。

```
pkm/
├── default.config.tmt      # Vault境界・基本設定
├── .tomet/                 # システム設定（普段は隠れています）
│   ├── blueprints/         # 日報・ノートの雛形
│   └── vocabularies/       # カスタム語彙
├── 00-Inbox/               # 一時メモ
├── 10-Daily/               # 日記・日報
├── 20-Projects/            # 進行中プロジェクト
└── 30-Notes/               # 永続ノート・ナレッジ
```

- **なぜこの構成か？**:
  日々の執筆において、ファイルツリーの最上位にシステムフォルダが並んでいるとノイズになります。`.tomet/` に隠蔽することで、快適にメモ書きへ没入できます。

---

## 2. アプリ開発・仕様書・チームWiki: [`app-dev/`](./app-dev)

Rust, Go, TypeScript などのコードリポジトリや、チームで仕様書・Wikiを管理する場合です。

```
app-dev/
├── default.config.tmt      # プロジェクト設定（schema/ 配下を指定）
├── src/                    # アプリケーションのコード
└── tmtroot/                # ドキュメント空間のルート
    ├── shelf.toml        # tomet-shelf（Webサイト生成）設定
    ├── .index.tmt          # トップページ・索引
    ├── docs/               # ユーザー向け仕様・ガイド
    ├── dev/                # 開発者専用メモ・ロードマップ
    └── schema/             # プロジェクト共通の語彙・Blueprint
        ├── blueprints/     # RFCや設計書の雛形
        └── vocabularies/   # ドメイン固有の語彙定義
```

- **なぜこの構成か？**:
  アプリ開発では、語彙（`vocabulary`）や設計書雛形（`blueprint`）もチーム全員で育てていく大事な仕様です。隠さず `tmtroot/schema/` に堂々と配置し、`tomet-shelf` でそのままAPI仕様書・語彙リファレンスとしてWebサイト化できます。

---

## クイックコマンド

### 新規ノート・文書の作成
```bash
# PKM: 今日のデイリーノートを作成
tomet new pkm/10-Daily/$(date +%Y-%m-%d).tmt --blueprint daily

# App-dev: RFC（設計書）を作成
tomet new app-dev/tmtroot/dev/rfc-001.tmt --blueprint rfc
```

### 構文・リンク・語彙の健全性チェック
```bash
# 各ディレクトリで実行
cd pkm && tomet check .
cd app-dev && tomet check .
```

### ドキュメントサイトのビルド（app-dev）
```bash
cd app-dev && tomet-shelf build tmtroot/
# プレビューサーバー起動
cd app-dev && tomet-shelf serve tmtroot/
```
