# App Development Tomet Example

アプリケーション開発リポジトリやチームWiki、仕様書管理に特化した、Tomet の推奨構成テンプレートです。

## ディレクトリ構造

```
app-dev/
├── default.config.tmt          # プロジェクト全体のTomet設定
├── src/                        # アプリケーションのソースコード
│   └── main.rs
├── Cargo.toml                  # （例：Rustの場合）
└── tmtroot/                    # ドキュメント・仕様書のルート
    ├── tmtbook.toml            # tmtbook（静的サイト生成）設定
    ├── .index.tmt              # トップページ・目次
    ├── docs/                   # ユーザー向け・仕様ドキュメント
    │   ├── spec/api.tmt
    │   └── guide/getting-started.tmt
    ├── dev/                    # 開発者専用メモ・ロードマップ
    │   └── roadmap.tmt
    └── schema/                 # 語彙・Blueprint（可視化して共同管理）
        ├── blueprints/rfc.blueprint.tmt
        └── vocabularies/api.vocabulary.tmt
```

## なぜ `tmtroot/schema/` にまとめるのか？

アプリ開発やチーム開発において、語彙（`vocabulary`）やテンプレート（`blueprint`）は**「チーム全員で共有・拡張していくプロジェクトの共通仕様」**です。

- **可視化**: 隠しフォルダではなく `schema/` に堂々と置くことで、新しいAPI定義要素やドキュメント雛形を追加しやすくします。
- **`tmtbook` との統合**: `tmtroot/` 直下に置くことで、`tmtbook build` を実行した際に「API語彙一覧」や「RFCテンプレート仕様」がそのままドキュメントサイトに自動レンダリングされます。

## 使い方

### 1. ドキュメントの整合性をチェックする
```bash
tomet check .
```

### 2. RFCテンプレートから新しい設計書を起こす
```bash
tomet new tmtroot/dev/rfc-001.tmt --blueprint rfc
```

### 3. ドキュメントサイトをビルドする（tmtbook）
```bash
tmtbook build tmtroot/
# またはローカルサーバー起動
tmtbook serve tmtroot/
```
