# 第3回 解答

## 演習

- 第1回（素のLLM）とエージェントの回答の違い：　講座独自の内容を検索してうまく答えられた。
- `--trace` で見えたツール呼び出し（ツール名と引数）：　[make_quiz]、引数: {"lecture": {"type": "integer"}}
- 1つの質問での LLM 呼び出し回数（`requests`）：　requests=2
- 追加したツールと、docstring に書いた説明：　[make_quiz]
  指定した回の用語から1つ選び、確認問題と答えを返す。
  「第2回の確認問題を出して」のように、講座内容の復習問題を求められたときに使う。

## 宿題

- 取り組んだレベル：発展
- やったこと：CodespaceでPiを動かし、Piのシステムプロンプトと自分のINSTRUCTIONを比較した。
- 結果：
自分のINSTRUCTIONは以下のとおり

INSTRUCTIONS = """\
あなたはAIエンジニアリング講座（AIE2026）の学習支援エージェントです。
- 用語や講座に固有のことを答える前に、必ず search_glossary で用語集を確認する。
- 回の内容を聞かれたら get_lecture_summary を使う。
- 確認問題やクイズを求められたら make_quiz を使う。
- 用語集に見つからないことは、推測で断定せず「用語集にはない」と伝える。
- 回答の最後に、関係する回（第N回）を示す。
- 宿題の答えそのものは書かず、考え方のヒントで導く。
"""

Piの方は例えば抜粋すると以下のような指示がある。
promptSections.preamble =
			"You are a coding assistant running inside pi, a coding agent harness. Help users inspect files, run commands, and modify code.";

	addRule("Be concise in your responses");
	addRule("Show file paths clearly when working with files");

- 気づき・疑問：
Piと講座のエージェントには、どちらも役割とツールの使い方が書かれている。Piには、ファイルを読み、コマンドを実行し、コードを編集する役割が与えられている。回答は簡潔にし、扱ったファイルのパスを明示するという指示もある。一方、当然ながら、自分のINSTRUCTIONにはある、宿題への答え方や、回答の根拠を講座の用語集で確認するという指示はない。
自分のINSTRUCTIONS は、質問の種類ごとに使うツールを指定している。用語を聞かれたら search_glossary、各回の内容を聞かれたら get_lecture_summary を使う。さらに、用語集にないことは推測で断定せず、回答の最後に関連する回を示し、宿題にはヒントで答えるよう求めている。なお、ファイルの編集やコマンド実行についての指示はない。