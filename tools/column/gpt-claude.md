# コラム: GPT3.5とClaude3 Opusはどっちが優秀？

GPT-3.5とClaude3 Opusはどちらも優れた言語モデルですが、それぞれ特徴や長所が異なります。

GPT-3.5は、OpenAIが開発した大規模な言語モデルで、膨大なテキストデータを学習しています。そのため、幅広い分野の知識を持ち、高い文章生成能力を示します。また、few-shot learningにも優れており、少ない例示でも新しいタスクに適応できます。

一方、Claude3 Opusは、Anthropic社が開発した言語モデルで、「構成的AI」の手法を用いています。これにより、安全性や倫理的配慮、一貫性などの点で優れたパフォーマンスを示すと言われています。また、対話においてユーザーの意図を汲み取り、適切な応答を生成することに長けています。

どちらの言語モデルが優れているかは、用途や要件によって異なります。例えば、多様な分野の知識が必要な場合はGPT-3.5が、倫理的配慮や一貫性が重要な場合はClaude3 Opusが適しているかもしれません。
ただし、言語モデルは常に進化しており、それぞれの特徴も変化していく可能性があります。また、APIの利用可能性やコストなども考慮する必要があるでしょう。

今回のNode-REDとobnizを使ったIoTアプリケーション開発では、両方の言語モデルを試してみることをお勧めします。それぞれの言語モデルが生成するJSONを比較し、どちらがより安定して要件を満たすフローを生成できるか確認してみてください。

また、プロンプトの改善を通じて、どちらの言語モデルがプロンプトの変更に適応しやすいかも観察できるかもしれません。
言語モデルの選択は、プロジェクトの成功に大きく影響します。適切な言語モデルを選ぶために、複数のモデルを試し、その特性を理解することが大切です。

これからも、GPT-3.5とClaude3 Opusの両方を活用しながら、生成AIを用いたIoTアプリケーション開発の可能性を探っていきましょう。

## という質問をClaudeにしてみた

GPT3.5だとClaude3 Opusの方が優秀とはされていますが、やることによって変わってきますし、自分がやりたいことにどの生成AIが向いているかは検証を自分で進めないといけないタイミングの様ですね。

> <img src="https://i.gyazo.com/e081a35b70b792a88ff980f409fe192f.png" width="400px" />

## この質問のように知識を問う内容はググる時代じゃなくなってきている

[ChatGPTのリリースでGoogleは「コードレッド」を宣言、AIチャットボットが検索ビジネスにもたらす脅威に対応するためにチームを再割り当て](https://gigazine.net/news/20221223-google-code-red-against-chatgpt/)

といった話題が1年半前くらいに出てました。少し前まではググって調べるが基本できたけどこういった知識を調べる系はAIに聞くのが良い時代になってきていますね。

授業で分からない単語などあればどんどんAIに聞いて調べてみましょう。