# interpret-paper

論文の URL またはローカルの PDF を渡すと、日本語の詳細な解説 HTML を生成するツールです。
[Claude Code](https://claude.ai/code) のスラッシュコマンド `/interpret` として動作します。

数式・定理・証明・アルゴリズムを含む論文を対象とし、最適化や機械学習を学ぶ大学院生が読む想定で解説を書きます。

## 必要なもの

- [Claude Code](https://claude.ai/code)（Claude へのアクセス権が必要）
- [uv](https://docs.astral.sh/uv/)（Python のパッケージ管理）

## セットアップ

```bash
git clone https://github.com/<your-username>/interpret-paper.git
cd interpret-paper
uv sync
```

Claude Code でこのディレクトリを開くと、`.claude/commands/` 以下を読み取って `/interpret` コマンドが登録されます。追加の設定はいりません。

## 使い方

Claude Code の入力欄で `/interpret` に続けて論文を指定します。

```
/interpret https://arxiv.org/abs/1706.03762
/interpret papers/adam.pdf
/interpret --select
```

`--select` は `papers/` にある PDF を一覧から選びます。
解説の粒度は `--detail` で指定できます（`low` / `medium` / `high`、既定は `medium`）。

自然言語でも同じく動作します。

```
この論文を解説して: https://arxiv.org/abs/1706.03762
```

arXiv の URL は abs ページ（`arxiv.org/abs/XXXX`）を指定してください。
ツールは ar5iv の HTML 版、arXiv 公式の HTML 版、PDF の順に取得を試み、最初に取得できたものを使います。

## 出力

解説は `output/` に HTML ファイルとして書き出されます。
ブラウザで開くと数式がレンダリングされます。数式の描画に MathJax を使うため、表示にはインターネット接続が必要です。

## スラッシュコマンドの仕組み

`/interpret` の実体は `.claude/commands/interpret.md` です。
Claude Code はプロジェクト内の `.claude/commands/*.md` をスラッシュコマンドとして登録します。このため、ファイルを置く以外の設定作業はいりません。

## ディレクトリ構成

```
interpret-paper/
├── CLAUDE.md                      # Claude への指示（対象読者・スタイル）
├── pyproject.toml                 # uv の依存関係
├── .claude/
│   ├── commands/
│   │   └── interpret.md           # /interpret スラッシュコマンド
│   └── skills/
│       └── interpret.md           # スキル定義（詳細な手順）
├── templates/document.html        # HTML テンプレート
├── src/pdf_extract.py             # ローカル PDF の構造抽出（PyMuPDF）
├── papers/                        # PDF を置く場所
└── output/                        # 生成した HTML の出力先
```
