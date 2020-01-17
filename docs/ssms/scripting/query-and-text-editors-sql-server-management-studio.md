---
title: クエリおよびテキスト エディター (SQL Server Management Studio) | Microsoft Docs
ms.prod: sql
ms.technology: scripting
ms.topic: conceptual
helpviewer_keywords:
- Query Editor [SQL Server Management Studio]
- Code Editor [SQL Server Management Studio], about Query Editor
- Query Editor [SQL Server Management Studio], full screen mode
- Query Editor [Database Engine], templates
- full screen mode [SQL Server Management Studio]
- SQL Server Management Studio [SQL Server], templates
- writing scripts
- modifying scripts
- SQL Server Management Studio [SQL Server], query editor
- Query Editor [SQL Server Management Studio], about Query Editor
- writing queries
- SQL Server Management Studio [SQL Server], editor
- scripts [SQL Server], SQL Server Management Studio
- queries [SQL Server], SQL Server Management Studio
ms.assetid: 062051e4-4b77-4969-98ae-d2547c24ce3e
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: ''
ms.date: 03/14/2017
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8d8958849239c730aa7f687cd12a559de158d5e1
ms.sourcegitcommit: da8bb7abd256b2bebee7852dc0164171eeff11be
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/14/2019
ms.locfileid: "70988160"
---
# <a name="query-and-text-editors-sql-server-management-studio"></a>クエリおよびテキスト エディター (SQL Server Management Studio)

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のいずれかのエディターを使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]、MDX、DMX、または XML/A スクリプトを対話的に編集し、テストできます。XML またはプレーンテキスト ファイルを編集することもできます。 各エディターでは、キーワードを色分け表示したり、言語固有の構文や使用方法のエラーをチェックするサービスがサポートされています。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディターには、 [!INCLUDE[tsql](../../includes/tsql-md.md)] コードの問題を解決するのに役立つ [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーが用意されています。  
  
## <a name="sql-server-management-studio-editors"></a>SQL Server Management Studio のエディター

 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] の 4 つのエディターは、共通のアーキテクチャを備えています。 テキスト エディターは基本的なレベルの機能を実装し、テキスト ファイル用の基本的なエディターとして使用できます。 それ以外の 3 つのエディター (クエリ エディター) は、SQL Server でサポートされるいずれかの言語の構文を定義する言語サービスを追加することで、この基本的な機能を拡張したものです。 クエリ エディターには、IntelliSense やデバッグなど、さまざまなエディター機能が実装されています。 クエリ エディターには、データベース エンジン クエリ エディター (Transact-SQL および XQuery ステートメントを含んだスクリプトの作成用)、MDX エディター (MDX 言語用)、DMX エディター (DMX 言語用)、および XML/A エディター (XML for Analysis 言語用) があります。  
  
## <a name="common-components"></a>共通コンポーネント

 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] のすべてのエディターに共通のコンポーネントを次に示します。  
  
 **コード ペイン**  
 クエリまたはテキストを入力する領域です。 クエリ エディターのコード ペインは、言語に応じたステートメント ビルダー機能を備えています。 テキスト編集環境は、検索と置換、一括コメントアウト、フォントと色のカスタマイズなどの機能をサポートしています。  
  
 コード ペインでは、テキストのインデント、タブ、ドラッグ アンド ドロップなどに関連する、テキストの動作に影響を与えるオプションを設定できます。 クエリ ウィンドウの機能は、ドキュメント ウィンドウ内のタブとして、または別個のドキュメントとして構成することができます。  
  
 **マージン**  
 インジケーター マージンとコード テキストの間の空白の列です。クリックするとテキストの行を選択できます。 マージンは表示または非表示にすることができます。  
  
 **水平スクロール バーと垂直スクロール バー**  
 コード ペインを横方向および縦方向にスクロールできます。これにより、コード ペインの表示可能領域を超えるコードを参照できます。  
  
 **行番号の表示**  
 エディター内のテキストまたはコードの左に行番号を表示します。 特定の行番号に移動できます。  
  
 **右端で折り返す**  
 テキストまたはコードの長い行を複数の行に分けて表示して、すべてのテキストを見ることができるようにします。 右端で折り返すオプションは、テキストの実行時または印刷時の動作には影響を与えません。 右端で折り返す設定をオンにするには、 **[ツール]** メニューの **[オプション]** ダイアログ ボックスで、[テキスト エディター] ページまたは特定のエディター ページのいずれかにある [すべての言語] の [全般] ページを使用します。  
  
## <a name="code-editor-components"></a>コード エディターのコンポーネント

 コード エディターには、テキスト エディターや XML エディターに共通の機能に加えて、次の機能があります。  
  
 **結果**  
 このウィンドウは、クエリの結果を表示するために使用します。 このウィンドウには、グリッド形式またはテキスト形式で結果が表示されます。結果をファイルに出力することもできます。 結果グリッドは、独立したタブ付きウィンドウとして表示できます。  
  
 **IntelliSense**  
 エディターで **[編集]** メニューの **[IntelliSense]** をポイントすると、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] IntelliSense のオプションが表示されます。  
  
 **コードの色分け**  
 構文要素がその種類に応じて異なる色で表示されるため、複雑なステートメントも見やすくなります。  
  
 **コードのアウトライン表示**  
 コードの左側にアウトラインを表す線を表示することにより、コード グループを表示します。 コード グループは折りたたんだり展開したりできるので、コードの確認が容易になります。  
  
 **テンプレート**  
 テンプレートは、データベース内にオブジェクトを作成するのに必要なステートメントの基本構造が含まれたファイルです。 スクリプトの作成を迅速化するのに使用できます。  
  
 **メッセージ**  
 スクリプトの実行時にサーバーから返されるエラー、警告、および情報メッセージが表示されます。 メッセージの一覧は、スクリプトが再び実行されるまで変更されません。  
  
 **ステータス バー**  
 クエリ エディター ウィンドウに関連付けられたシステム情報 (たとえばクエリ エディターの接続先のインスタンス) を表示します。  
  
## <a name="database-engine-query-editor-components"></a>データベース エンジン クエリ エディターのコンポーネント

 以下のコンポーネントは、データベース エンジン クエリ エディターにのみ該当します。  
  
 **デバッガー**  
 特定のステートメントでコードの実行を一時停止することができます。 この機能は、データおよびシステム情報を表示して、コードのエラーを見つけるのに役立ちます。  
  
 **エラー一覧**  
 構文エラーとセマンティック エラーが IntelliSense によって表示されます。 エラーの一覧は、 [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトの編集に伴って動的に変更されます。  
  
 **グラフィカルなプラン表示**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの実行プランに組み込まれる論理手順を表示します。  
  
 **クライアント統計**  
 クエリの実行に関する情報がカテゴリに分けて表示されます。 **[クエリ]** メニューの **[クライアント統計を含める]** をクリックすると、 **[クライアント統計]** ウィンドウがクエリ実行中に表示されます。 複数のクエリを連続して実行した場合、統計には平均値も表示されます。 **[クエリ]** メニューの **[クライアント統計のリセット]** をクリックすると、平均がリセットされます。  
  
 **コード スニペット**  
 データベース エンジン クエリ エディターでステートメントを追加する際のひな形として使用します。 SQL Server に付属の定義済みのスニペットを挿入できるほか、独自のスニペットを追加することもできます。  
  
 **SQLCMD モード**  
 sqlcmd ユーティリティによってサポートされる一連のコマンドを含んだ [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトを実行します。 詳細については、「 [sqlcmd 操作方法のトピック](https://msdn.microsoft.com/library/dd7a2d2b-6327-4d77-ac5a-580d36073ad4)」を参照してください。  
  
## <a name="editor-tasks"></a>エディターのタスク  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディターの基本的な機能を表示し、使用する方法について説明します。|[データベース エンジン クエリ エディター &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/database-engine-query-editor-sql-server-management-studio.md)|  
|MDX クエリ エディターの基本的な機能を表示し、使用する方法について説明します。|[MDX クエリ エディター &#40;Analysis Services - 多次元データ&#41;](https://msdn.microsoft.com/library/777f2c23-1c1c-4b72-9d19-48a4866551f8)|  
|DMX クエリ エディターの基本的な機能を表示し、使用する方法について説明します。|[DMX クエリ エディター &#40;Analysis Services - データ マイニング&#41;](https://msdn.microsoft.com/library/7ac877a1-0f29-46b9-9a51-73b02172bef1)|  
|XML/A エディターの基本的な機能を表示し、使用する方法について説明します。|[XML エディター &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/xml-editor-sql-server-management-studio.md)|  
|行番号表示や IntelliSense オプションなど、各種エディターのオプションを構成する方法について説明します。|[エディターの構成 &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/configure-editors-sql-server-management-studio.md)|  
|[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]でエディターを開くための、さまざまな方法について説明します。|[エディターの表示 &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/open-an-editor-sql-server-management-studio.md)|  
|右端での折り返し、ウィンドウの分割、タブなど、各種表示モードを管理する方法について説明します。|[エディターと表示モードの管理](../../relational-databases/scripting/manage-the-editor-and-view-mode.md)|  
|テキストの非表示やインデントなど、書式設定オプションの設定方法について説明します。|[コードの書式設定の管理](../../relational-databases/scripting/manage-code-formatting.md)|  
|インクリメンタル検索やジャンプなどの機能を使用して、エディター ウィンドウ内でテキストを検索する方法について説明します。|[コード内とテキスト内の移動](../../relational-databases/scripting/navigate-code-and-text.md)|  
|さまざまな構文の分類に対して色分けオプションを設定し、複雑なステートメントを見やすく表示する方法について説明します。|[クエリ エディターでのコードの色分け](../../relational-databases/scripting/color-coding-in-query-editors.md)|  
|現在作業していない複雑なスクリプトを、コードのアウトライン表示機能を使用して部分的に非表示する方法について説明します。|[コードのアウトライン表示](../../relational-databases/scripting/code-outlining.md)|  
|スクリプト内でドラッグ アンド ドロップによってテキストを移動する方法について説明します。|[テキストのドラッグ アンド ドロップ](../../relational-databases/scripting/drag-and-drop-text.md)|  
|列名を変更する場合などに、検索と置換をグローバルに実行する方法について説明します。|[検索と置換](../../relational-databases/scripting/search-and-replace.md)|  
|コードの重要箇所を見つけやすいようにブックマークを設定する方法について説明します。|[ブックマークの管理](../../relational-databases/scripting/manage-bookmarks.md)|  
|スクリプトまたはその結果をウィンドウまたはグリッドから印刷する方法について説明します。|[コードと結果の印刷](../../relational-databases/scripting/print-code-and-results.md)|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディターで sqlcmd の機能を使用する方法について説明します。|[クエリ エディターによる SQLCMD スクリプトの編集](../../relational-databases/scripting/edit-sqlcmd-scripts-with-query-editor.md)|  
|オブジェクト名の入力時にオート コンプリート機能を利用したり、有効な位置へと確実にブレークポイントを設定したりできるなど、IntelliSense が備えている機能の使用方法について説明します。|[IntelliSense &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/intellisense-sql-server-management-studio.md)|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] クエリ エディターでのコード スニペットの使用方法について説明します。 スニペットは、使用頻度の高いステートメントまたはブロックのテンプレートです。特定用途のスニペットを追加して拡張したりカスタマイズしたりすることができます。|[Transact-SQL コード スニペット](../../relational-databases/scripting/transact-sql-code-snippets.md)|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーを使用してコードをステップ実行したり、デバッグ情報 (変数やパラメーターの値など) を表示したりする方法について説明します。|[Transact-SQL デバッガー](../../relational-databases/scripting/transact-sql-debugger.md)|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)]の各インスタンスに対して独自の色を設定したり、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のクエリ エディターのウィンドウのステータス バーの背景としてそれらの色を設定する方法について説明します。|[ステータス バー &#40;データベース エンジン クエリ エディター&#41;](../../relational-databases/scripting/status-bar-database-engine-query-editor.md)|  
  
## <a name="next-steps"></a>次の手順

 [SQL Server Management Studio のキーボード ショートカット](../../tools/sql-server-management-studio/sql-server-management-studio-keyboard-shortcuts.md)