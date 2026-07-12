# optional/ — 厳格運用向けの設定サンプル(Claude Code 専用)

WIKI_RULES.md の書き込み境界(2章)は規約であり、LLM の遵守に依存する。
Claude Code で境界をハーネス側から強制したい場合は、本ディレクトリの設定サンプルを使う。

## claude-settings-strict.json の使い方

**Wiki 操作専用のセッション**で使うことを想定している(本体開発と併用すると
本体側の編集がすべてブロック・確認対象になり開発を阻害するため)。

1. 内容をプロジェクトの `.claude/settings.local.json` にマージする
   (Wiki 操作するときだけ有効化し、終わったら外す運用でもよい)
2. `deny` のパス一覧(`src/**`, `docs/**` など)は**プロジェクトの実構成に合わせて書き換える**。
   サンプルは一般的な構成の例にすぎない

## 挙動の説明

- `allow`: `ai_wiki/**` への Edit/Write は確認なしで許可、読み取りは全域許可
- `deny`: 列挙したプロジェクト本体パスへの Edit/Write を強制ブロック
  (Claude Code では deny が allow より優先される)
- allow にも deny にも該当しない書き込み(列挙漏れのパス)は、
  既定の permission モードでは実行前にユーザー確認が入る。deny の列挙が
  完全でなくても、確認プロンプトが最後の防壁になる

## 注意

- この設定は Claude Code 専用。他のエージェントには WIKI_RULES.md の規約のみが境界となる
- Bash 経由の書き込み(`echo > file` 等)はこの Edit/Write ルールでは防げない。
  厳格運用セッションでは Bash の許可設定も絞ることを推奨する
