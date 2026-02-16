![PM-Quill Logo](images/pm-quill-logo.png)

# PM-Quill — AI 駆動のプロダクト意思決定ツール

[English](README.md) | [中文](README.zh.md)

> コードを書く前に、何を作るか考えよう。

コーディング AI ツールの**上流**。Cursor / Claude Code はコードを書く。PM-Quill は**何のコードを書くか**を決める手助けをします。

## なぜ PM-Quill が必要か

AI はコーディングのハードルを限りなく下げました。しかし「何を作るか」「なぜ作るか」という意思決定は、まだ勘に頼っています。

個人開発者のよくあるサイクル：

```
アイデアが浮かぶ → すぐコードを書く → 途中で方向が間違いだと気づく → やり直し
```

PM-Quill はこのサイクルを断ち切ります：

```
アイデアが浮かぶ → /spec で整理 → /feasibility で評価 → /plan でタスク分解 → AI にコードを任せる
```

## コアコマンド

| コマンド | 機能 | 出力 |
|---------|------|------|
| `/spec` | 曖昧なアイデアを構造化されたプロダクト仕様に変換 | `specs/{project}/spec.md` |
| `/feasibility` | 技術アプローチ、工数、リスクを評価 | `specs/{project}/feasibility.md` |
| `/plan` | 実行可能なタスクリストに分解 | `specs/{project}/plan.md` |
| `/review` | プロジェクトの振り返り、学びの抽出 | `specs/{project}/review.md` |

## クイックスタート

### 前提条件

- [Claude Code](https://code.claude.com/) をインストール
- [OpenCode](https://opencode.ai/) をインストール

### 使い方

1. リポジトリをクローン：

```bash
git clone https://github.com/lukeliu95/PM-Quill.git
```

2. PM-Quill ディレクトリで Claude Code / OpenCode を起動：

```bash
cd PM-Quill
claude
```

3. 使い始める：

```
/spec AI API のコストを追跡するダッシュボードを作りたい
```

PM-Quill がいくつかの重要な質問をした後、完全なプロダクト仕様を生成します。次に `/feasibility` でアプローチを評価し、`/plan` でタスクに分解すれば、OpenCode や Claude Code にコーディングを任せられます。

## ワークフロー例

```
あなた：/spec ブックマークを素早く保存・整理できる Chrome 拡張機能を作りたい

PM-Quill：[1-2 個の重要な質問]
PM-Quill：[specs/bookmark-manager/spec.md を生成]

あなた：/feasibility

PM-Quill：[2-3 個の技術アプローチを評価、工数を見積もり]
PM-Quill：[specs/bookmark-manager/feasibility.md を生成]

あなた：/plan

PM-Quill：[日単位のタスクに分解、各タスクに AI 用プロンプト付き]
PM-Quill：[specs/bookmark-manager/plan.md を生成]

あなた：Task 1.1 のプロンプトを Cursor にコピーして、コーディング開始
```

## プロジェクト構成

```
PM-Quill/
├── CLAUDE.md              # プロダクトの魂ファイル
├── context/               # プロダクトとユーザーのコンテキスト
│   ├── product.md         # PM-Quill のプロダクト定義
│   └── user.md            # ターゲットユーザーペルソナ
├── specs/                 # 全プロジェクトの Spec 出力
│   └── {project-name}/    # プロジェクトごとのサブディレクトリ
├── templates/             # Spec テンプレート
├── archive/               # 完了プロジェクトのアーカイブ
└── .claude/
    ├── agents/            # 専門エージェント定義
    ├── skills/            # スラッシュコマンド定義
    └── rules/             # ライティング規約
```

## 設計原則

1. **Spec がすべてを駆動する** — Spec なしにアクションなし
2. **ファイルがデータベース** — すべての成果物は Markdown：可読、検索可能、バージョン管理可能
3. **段階的開示** — まず 80% のソリューションを提供し、不確実な点はあなたの判断に委ねる
4. **シンプル優先** — 3 行の繰り返しコードは、早すぎる抽象化に勝る

## やらないこと

- コードは書かない（Cursor / Claude Code に任せる）
- プロジェクト管理はしない（Linear / Notion に任せる）
- デザインはしない（Figma / Gemini に任せる）
- 市場調査はしない（専門のリサーチツールに任せる）

## 作者

- [Luke Liu](https://x.com/lukeliu95)

## License

MIT
