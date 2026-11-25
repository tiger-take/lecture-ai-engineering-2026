# 第6回 解答

## 演習

<!-- [tool call] の行は、表示された行をそのまま貼り付けてください。終わらなかった STEP は、空欄のままでかまいません。 -->

- STEP 1 のツールの名前：glossary_search_glossary
- STEP 2 の [tool call]：glossary_search_glossary({'query': '3レベル'})
- STEP 3 の [tool call]：fetch_fetch({'url': 'https://modelcontextprotocol.io/', 'max_length': 1000})
- STEP 4 の [tool call]：aws_aws___search_documentation({'search_phrase': 'Amazon S3 バージョニング', 'limit': 1})
- 気づき・疑問：ローカルのPythonスクリプト、uvxで動的に取得する外部パッケージ、URL接続のリモートサービス（AWS）の3種類が、エージェント側からはすべて統一された形式（プレフィックス付きツール名）で呼び出せる点が非常に分かりやすかったです。サーバー名のプレフィックスが付くことで、複数サーバー間でツール名が衝突しない設計になっていることも確認できました。

## 宿題

<!-- 基礎・実装・発展のどれか1つに取り組めば完了です。 -->

- 取り組んだレベル：基礎
- やったこと：`app/mcp_server.py` に `server.tool()(tools.get_lecture_summary)` を追加して `get_lecture_summary` を MCP ツールとして公開しました。エージェント側のコードや設定を変更せずに `--list-tools` で `glossary_get_lecture_summary` が認識されることを確認し、「第2回では何を学びますか？」と質問してツール呼び出しをトレースしました。
- 結果：`glossary_get_lecture_summary({'lecture': 2})` が正しく呼び出され、第2回の要点（ファインチューニングとLoRA）を踏まえた回答が得られました。`uv run pytest -q` でも 21 件すべてのテストが通過しました。
- 気づき・疑問：クライアント側が起動時にサーバーへ利用可能なツール一覧を問い合わせるプロトコルになっているため、サーバー側でツールを追加・更新するだけでクライアント側の実装や設定を一切変えずに新ツールを活用できるのが MCP の優れた利便性だと実感しました。
