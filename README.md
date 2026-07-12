# wk_llm_wiki — 汎用LLM Wiki

どのプロジェクトにも配置できる、LLM(Claude Code 等)が管理するプロジェクト内 Wiki の
テンプレートと運用規約を開発するプロジェクト。

## 要件(3点)

1. どのプロジェクトにも配置可能(ディレクトリ一式のコピーで導入完了)
2. LLM は Wiki 用ディレクトリ(`ai_wiki/`)配下のみを更新する
3. 人間が指示したときに、プロジェクトの実状態をチェックして Wiki を更新する(手動トリガー)

## ドキュメント

- [docs/design_llm_wiki.md](docs/design_llm_wiki.md) — 検討ドキュメント(設計方針・方式比較・未決事項)

## 参考

- https://zenn.dev/tsurubee/articles/llm-wiki-connecting-knowledge (Karpathy 型 LLM Wiki)
- https://qiita.com/usayamadausako/items/c8b5cca97554f6f64782 (手動トリガー型 ai_wiki)

## 状態

検討フェーズ。テンプレート(`template/ai_wiki/`)は未実装。
