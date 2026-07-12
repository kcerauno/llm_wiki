# llm_wiki — 汎用LLM Wiki

どのプロジェクトにも配置できる、LLM(Claude Code 等)が管理するプロジェクト内 Wiki の
テンプレートと運用規約を開発するプロジェクト。

## 要件(3点)

1. どのプロジェクトにも配置可能(ディレクトリ一式のコピーで導入完了)
2. LLM は Wiki 用ディレクトリ(`ai_wiki/`)配下のみを更新する
3. 人間が指示したときに、プロジェクトの実状態をチェックして Wiki を更新する(手動トリガー)

## ドキュメント

- [docs/design_llm_wiki.md](docs/design_llm_wiki.md) — 検討ドキュメント(設計方針・方式比較・未決事項)

## 導入方法

1. `template/ai_wiki/` を対象プロジェクトのルートへコピー:
   `cp -r template/ai_wiki /path/to/project/`
2. 対象プロジェクトの CLAUDE.md(または同等のエージェント指示ファイル)に1行追記:
   `ai_wiki/ は LLM 管理の Wiki。運用規約は ai_wiki/WIKI_RULES.md を参照。`
3. 最初の指示: 「プロジェクトの状態をチェックして Wiki を初期化して(スコープ: README と主要設定)」

運用の詳細は [template/ai_wiki/WIKI_RULES.md](template/ai_wiki/WIKI_RULES.md) を参照。

## 参考

- https://zenn.dev/tsurubee/articles/llm-wiki-connecting-knowledge (Karpathy 型 LLM Wiki)
- https://qiita.com/usayamadausako/items/c8b5cca97554f6f64782 (手動トリガー型 ai_wiki)

## 状態

テンプレート初版実装済み。次: 実プロジェクト1つに配置して Sync → Record → Synthesize → Promote を一巡試行。
