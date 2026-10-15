# Tomet Vault Example (PKM / Note-taking Starter)

個人知識管理（Personal Knowledge Management, PKM）やノート術（Daily notes、Zettelkasten、PARA等）に特化した、Tomet Vault の推奨構成テンプレートです。

## ディレクトリ構造

```
vault-example/
├── default.config.tmt      # Vault境界・設定（Blueprint・語彙の登録）
├── .tomet/                 # システム用（雛形・語彙）。普段は隠れています
│   ├── blueprints/         # ノートのテンプレート定義
│   │   ├── daily.blueprint.tmt
│   │   └── note.blueprint.tmt
│   └── vocabularies/       # Vault専用のカスタム語彙
│       └── vault.vocabulary.tmt
├── 00-Inbox/               # 一時的なメモや着信ノート
├── 10-Daily/               # 日記・日報
│   └── 2026-10-15.tmt
├── 20-Projects/            # 進行中プロジェクト
└── 30-Notes/               # 永続ノート・ナレッジ
    └── welcome.tmt
```

## なぜ `.tomet/` にまとめるのか？

ノートを書く日常において、最も重要なのは**「思考に集中すること」**です。
- ファイルツリーの最上位に `schema/` や `config.tmt` が並んでいると、日々のノートを探す際の認知的ノイズになります。
- Obsidian の `.obsidian/` と同様に、システムに関わる設定やテンプレートを `.tomet/` にしまっておくことで、ルート階層全体を自分のノート空間として快適に保てます。

## 使い方

### 1. 新しいデイリーノートを作成する
```bash
tomet new 10-Daily/$(date +%Y-%m-%d).tmt --blueprint daily
```

### 2. 一般ノートを作成する
```bash
tomet new 30-Notes/my-idea.tmt --blueprint note
```

### 3. Vault全体の健全性をチェックする
```bash
tomet check .
```
