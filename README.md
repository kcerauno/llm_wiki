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

## 推奨の指示方法

指示は自然言語だが、最も曖昧さがないのは**操作名そのものをキーワードとして使う**形:
`ai_wiki の <操作名> をして`。「ai_wiki」の語が規約(WIKI_RULES.md)の参照を誘発し、
操作名が規約の節見出しと一対一対応するため、解釈の揺れが生じにくい。

| 操作 | 意味 | 指示例 |
|---|---|---|
| **Sync** | プロジェクト実体と Wiki の突き合わせ・更新(実体が正) | `ai_wiki の Sync をして` |
| **Record** | いまの調査・作業の結果を investigations/ に新規記録 | `ai_wiki に Record して:ここまでの調査結果` |
| **Promote** | 整理。調査メモの concepts/ への昇格・archive への退避・承認済み関連リンクの反映 | `ai_wiki の Promote をして` |
| **Lint** | Wiki 内部の健全性チェック(リンク切れ・重複・矛盾など)。報告のみで修正しない | `ai_wiki の Lint をして` |
| **Synthesize** | 全知見を横断して共通パターン・矛盾・ギャップ・新仮説を 99-Insights.md に抽出 | `ai_wiki の Synthesize をして` |

### 追加指定のやり方

操作名の後ろに括弧や「:」で条件を付ける。よく使う指定:

- **スコープを絞る**(Sync / Synthesize):
  `ai_wiki の Sync をして(スコープ: src/auth/ 配下のみ)`
  `ai_wiki の Synthesize をして(対象: 最近1ヶ月に更新されたページのみ)`
- **記録する内容を指定する**(Record):
  `ai_wiki に Record して:キャッシュ有効期限の調査結果。結論と根拠を中心に`
- **対象ページを指定する**(Promote / Lint):
  `ai_wiki の Promote をして(investigations/session_timeout.md を concepts へ昇格できるか評価)`
- **複数操作の連続実行**:
  `ai_wiki の Sync と Lint をして`(規約の定める順序 Sync → Record → Promote → Lint → Synthesize で実行される)

## 参考

- https://zenn.dev/tsurubee/articles/llm-wiki-connecting-knowledge (Karpathy 型 LLM Wiki)
- https://qiita.com/usayamadausako/items/c8b5cca97554f6f64782 (手動トリガー型 ai_wiki)

## 状態

テンプレート初版実装済み。次: 実プロジェクト1つに配置して Sync → Record → Synthesize → Promote を一巡試行。
