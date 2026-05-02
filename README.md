# HF Agents Course Lab

Hugging Face Agents Course を学習しながら、最終的に調査・検索・計算・回答整形ができるエージェントを作るためのリポジトリです。

最終成果物は、GAIA 形式のタスクに対応できる調査エージェントです。

## 目的

このリポジトリでは、次の内容を実装・記録します。

- エージェントの基本構造の理解
- 道具を使うエージェントの実装
- `smolagents`、LlamaIndex、LangGraph の比較
- 検索拡張生成を使うエージェントの実装
- 評価データによる性能確認
- 失敗分析と改善
- Hugging Face Spaces での公開

## 最終目標

次の機能を持つエージェントを作成します。

- 入力された質問を分析する
- 必要な手順を計画する
- 検索、文書確認、計算などの道具を選択する
- 取得した根拠を整理する
- 最終回答を短く整形する
- 評価結果と失敗原因を記録する

## リポジトリ構成

```text
hf-agents-course-lab/
├── README.md
├── pyproject.toml
├── uv.lock
├── .python-version
├── .env.example
├── notes/
│   ├── unit1_agents_fundamentals.md
│   ├── unit2_framework_comparison.md
│   ├── unit3_agentic_rag.md
│   └── unit4_final_report.md
├── agents/
│   ├── simple_tool_agent/
│   ├── smolagents_agent/
│   ├── llamaindex_agent/
│   ├── langgraph_agent/
│   └── gaia_agent/
├── tools/
│   ├── web_search.py
│   ├── calculator.py
│   ├── document_reader.py
│   ├── image_reader.py
│   └── answer_normalizer.py
├── rag/
│   ├── retriever.py
│   ├── index_builder.py
│   └── sample_data/
├── eval/
│   ├── test_cases.jsonl
│   ├── run_eval.py
│   ├── results.csv
│   └── error_analysis.md
├── app/
│   ├── app.py
│   └── requirements.txt
└── experiments/
    ├── prompts/
    ├── traces/
    └── ablations/
```

## 学習計画

|  週 | 学習範囲                        | 成果物                 |
| -: | --------------------------- | ------------------- |
|  0 | 環境構築、Hugging Face Spaces 確認 | リポジトリ、README、学習ログ   |
|  1 | エージェントの基礎                   | `simple_tool_agent` |
|  2 | `smolagents`                | `smolagents_agent`  |
|  3 | LlamaIndex、LangGraph        | フレームワーク比較表、小実装      |
|  4 | エージェント型検索拡張生成               | `rag/`             |
|  5 | 評価基盤                        | `eval/`             |
|  6 | 最終エージェント初版                  | `gaia_agent`        |
|  7 | GAIA 対応と提出準備                | Spaces 公開版、評価結果     |
|  8 | 改善と最終レポート                   | 最終レポート、失敗分析         |

## セットアップ

このリポジトリでは、Python 環境と依存関係の管理に `uv` を使います。

### 1. リポジトリを複製

```bash
git clone https://github.com/YOUR_NAME/hf-agents-course-lab.git
cd hf-agents-course-lab
```

### 2. `uv` をインストール

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Windows の場合：

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

インストール済みか確認します。

```bash
uv --version
```

### 3. Python と依存関係を同期

```bash
uv sync
```

`.venv` は `uv sync` により自動作成されます。通常は手動で `source .venv/bin/activate` する必要はありません。

### 4. 環境変数を設定

`.env` を作成します。

```bash
cp .env.example .env
```

例：

```env
HF_TOKEN=your_huggingface_token
OPENAI_API_KEY=your_openai_api_key
SERPAPI_API_KEY=your_serpapi_key
```

使用するモデルや検索手段に応じて、必要なものだけ設定します。

## 実行方法

### 最小エージェント

```bash
uv run python agents/simple_tool_agent/main.py
```

### `smolagents` エージェント

```bash
uv run python agents/smolagents_agent/main.py
```

### 検索拡張生成エージェント

```bash
uv run python rag/retriever.py
```

### GAIA 向けエージェント

```bash
uv run python agents/gaia_agent/main.py
```

### Hugging Face Spaces 用アプリ

```bash
uv run python app/app.py
```

## 成果物

### 1. 学習ノート

`notes/` に、各ユニットの学習内容を記録します。

記録形式：

```markdown
# Unit X メモ

## 学んだ概念

## 実装したもの

## つまずいた点

## 自分のプロジェクトに使うなら

## 次に試すこと
```

### 2. エージェント実装

`agents/` に、段階ごとの実装を保存します。

| ディレクトリ               | 内容                         |
| -------------------- | -------------------------- |
| `simple_tool_agent/` | 最小構成の道具利用エージェント            |
| `smolagents_agent/`  | `smolagents` を使った実装        |
| `llamaindex_agent/`  | LlamaIndex を使った検索エージェント    |
| `langgraph_agent/`   | LangGraph を使った状態管理つきエージェント |
| `gaia_agent/`        | 最終課題向けエージェント               |

### 3. 道具

`tools/` に、エージェントから呼び出す道具を実装します。

| ファイル                   | 役割      |
| ---------------------- | ------- |
| `web_search.py`        | ウェブ検索   |
| `calculator.py`        | 数値計算    |
| `document_reader.py`   | 文書読み取り  |
| `image_reader.py`      | 画像確認    |
| `answer_normalizer.py` | 回答形式の整形 |

### 4. 評価

`eval/` に、評価データと結果を保存します。

```text
eval/
├── test_cases.jsonl
├── run_eval.py
├── results.csv
└── error_analysis.md
```

評価データの形式：

```json
{"id":"q001","question":"...","expected_answer":"...","category":"retrieval"}
{"id":"q002","question":"...","expected_answer":"...","category":"calculation"}
{"id":"q003","question":"...","expected_answer":"...","category":"multi-hop"}
```

評価実行：

```bash
uv run python eval/run_eval.py
```

## 評価観点

エージェントは、次の観点で評価します。

| 観点   | 内容                    |
| ---- | --------------------- |
| 正答率  | 期待回答と一致しているか          |
| 道具選択 | 必要な道具を選べているか          |
| 根拠確認 | 回答の前に必要な情報を確認しているか    |
| 回答形式 | 余計な説明を含まず、指定形式で答えているか |
| 再現性  | 同じ入力に対して安定した結果を返せるか   |

## 失敗分類

失敗した問題は、次の分類で記録します。

| 分類     | 内容             | 改善方針        |
| ------ | -------------- | ----------- |
| 検索失敗   | 必要な情報を取得できない   | 検索語の生成を改善する |
| 読解失敗   | 取得した情報を誤って解釈する | 根拠抽出を明示する   |
| 計算失敗   | 数値処理を誤る        | 計算道具を必ず使う   |
| 道具選択失敗 | 不要または不適切な道具を使う | タスク分類を改善する  |
| 回答形式失敗 | 余計な説明や表記ゆれがある  | 回答正規化を強化する  |

## 最終エージェントの処理フロー

```text
質問入力
  ↓
タスク分類
  ↓
計画生成
  ↓
道具選択
  ↓
検索・文書確認・計算
  ↓
根拠整理
  ↓
回答生成
  ↓
回答正規化
  ↓
最終回答
```

## 最終レポート

`notes/unit4_final_report.md` に、次の内容をまとめます。

```markdown
# 最終レポート

## 作ったもの

## 採用した構成

## 使用した道具

## 評価結果

## 成功した問題の傾向

## 失敗した問題の傾向

## 改善した点

## 今後の改善案
```

## 完了条件

このリポジトリの完了条件は、次のとおりです。

* Hugging Face Agents Course の主要ユニットを完了している
* 最小エージェントを実装している
* `smolagents` を使ったエージェントを実装している
* 検索拡張生成を使ったエージェントを実装している
* 評価用データで性能を確認している
* Hugging Face Spaces で公開している
* 評価結果と失敗分析を記録している

## 公開物

最終的に、次のものを公開します。

* Hugging Face Space
* 実装コード
* README
* 評価結果
* 失敗分析
* 最終レポート

## ライセンス

このリポジトリのコードは MIT License とします。

教材、モデル、外部データの利用条件は、それぞれの提供元のライセンスに従います。
