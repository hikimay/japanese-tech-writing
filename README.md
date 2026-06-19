# japanese-tech-writing

生成 AI に日本語の技術文書（書籍の章、技術記事、解説文）を書かせる／推敲させるときに、文章の質を制御する [Claude Code](https://claude.com/claude-code) スキルです。
論理が通っているように見えて中身のない「AI 特有の言い回し」を抑え、論証の筋が通った技術文章を生成します。

## 由来と先行スキル

このスキルは、二つの先行する取り組みに基づいています。

- 文章規範の本体は、k16shikano 氏の「日本語技術文書の文章規範」に基づきます（[gist](https://gist.github.com/k16shikano/fd287c3133457c4fd8f5601d34aa817d)）。観点 1〜8 の骨格はこの規範を技術文書向けに整理したものです。
- AI 臭の語彙リスト（[reference/ng-vocab.md](reference/ng-vocab.md)）は、iKora128 / Daichi Nagashima 氏の「[stop-ai-slop-jp](https://github.com/iKora128/stop-ai-slop-jp)」（MIT License）の語彙を、技術文書向けに取捨選択・改変したものです。

本スキルは、これらを Claude Code のスキル形式にまとめ、生成・推敲・採点の手順を加えたものです。

## 制御する観点

1. 整形（一文一改行、和欧文間スペースなど）
2. 段落と論証の構成
3. 論証の厳密さ（最優先）
4. 読み手の負荷の管理
5. 視点と語り
6. 演出の抑制
7. LLM っぽい表現の禁止
8. 冗長の排除

規範本体は [SKILL.md](SKILL.md) にあります。詳細な規範は [reference/rules.md](reference/rules.md)、点検項目と採点表は [reference/checklist.md](reference/checklist.md)、避けるべき語彙は [reference/ng-vocab.md](reference/ng-vocab.md) に分けて置いています。

## インストール

すべてのプロジェクトから使う個人用なら、`~/.claude/skills/` に置きます。

```bash
git clone https://github.com/hikimay/japanese-tech-writing.git \
  ~/.claude/skills/japanese-tech-writing
```

特定のプロジェクトだけで使うなら、そのプロジェクトの `.claude/skills/` に置きます。

```bash
git clone https://github.com/hikimay/japanese-tech-writing.git \
  .claude/skills/japanese-tech-writing
```

## 使い方

技術文書を書く・直す作業でこのスキルが規範を適用します。用途は次の 3 つです。

- 生成：「日本語技術文書のルールに従って、〇〇の解説を書いて」
- 推敲：「/japanese-tech-writing この下書きを規範に沿って推敲して」。下書きはファイルパスを渡しても、本文を貼り付けても校正できます。
- 公開前チェック：「/japanese-tech-writing この文章を採点して」（6 軸×10 点、合格ライン 42/60）

## 位置づけ

技術文書に特化し、論証の厳密さ（正確な因果・定義、必要な不確実性の保持）を最優先します。随筆やブログなど一般的な日本語文にも、ここでの規範をそのまま適用できます。

## ライセンス

MIT License。詳細は [LICENSE](LICENSE) を参照してください。
