---
title: SQL 実行タスク エディター ([全般] ページ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executesqltask.general.f1
helpviewer_keywords:
- Execute SQL Task Editor
ms.assetid: beb39086-28ce-46af-b6d8-f7b4fb8d9069
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 96d211defa789888a3fd7b513b4dff60fa795cb6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66058989"
---
# <a name="execute-sql-task-editor-general-page"></a>[SQL 実行タスク エディター] ([全般] タブ)
  **[SQL 実行タスク エディター]** ダイアログ ボックスの **[全般]** ページを使用すると、SQL 実行タスクを構成したり、タスクが実行する SQL ステートメントを指定したりできます。  
  
 このタスクの詳細については、「[SQL 実行タスク](control-flow/execute-sql-task.md)」、「[SQL 実行タスクのパラメーターとリターン コード](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md)」、および「[SQL 実行タスクにおける結果セット](../../2014/integration-services/result-sets-in-the-execute-sql-task.md)」を参照してください。 Transact-SQL クエリ言語の詳細については、「[Transact-SQL リファレンス &#40;データベース エンジン&#41;](/sql/t-sql/language-reference)」を参照してください。  
  
## <a name="static-options"></a>静的オプション  
 **名前**  
 ワークフロー内の SQL 実行タスクに一意な名前を指定します。 指定された名前は [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーに表示されます。  
  
 **[説明]**  
 SQL 実行タスクの説明です。 パッケージを自己文書化して目的を明確にし、保守が容易になるように、タスクの目的について記述することをお勧めします。  
  
 **[TimeOut]**  
 タスクがタイムアウトになるまでに実行される最大の秒数を指定します。この値に 0 を指定すると、時間は無制限になります。 既定値は 0 です。  
  
> [!NOTE]  
>  接続してトランザクションを完了するための時間を、 **[TimeOut]** で指定された秒数よりも長く指定することによってスリープ機能をエミュレートする場合、ストアド プロシージャはタイムアウトになりません。 ただし、クエリを実行するストアド プロシージャは、 **[TimeOut]** で指定された時間制限の影響を常に受けます。  
  
 **CodePage**  
 変数の Unicode 値を変換するときに使用するコード ページを指定します。 既定値は、ローカル コンピューターのコード ページです。  
  
> [!NOTE]  
>  SQL 実行タスクで ADO 接続マネージャーまたは ODBC 接続マネージャーを使用する場合、 **[CodePage]** プロパティは使用できません。 ソリューションでコード ページを使用する必要がある場合は、SQL 実行タスクで OLE DB 接続マネージャーまたは ADO.NET 接続マネージャーを使用します。  
  
 **[TypeConversionMode]**  
 このプロパティを `Allowed` に設定すると、SQL 実行タスクは出力パラメーターとクエリ結果を結果が割り当てられている変数のデータ型に変換します。 この機能は、結果セットの種類が **単一行** の場合に適用されます。  
  
 **[ResultSet]**  
 SQL ステートメントの実行によって予測される結果の型を指定します。 **[単一行]** 、 **[完全な結果セット]** 、 **[XML]** 、または **[なし]** から選択します。  
  
 **ConnectionType**  
 データ ソースへの接続に使用する接続マネージャーの種類を選択します。 使用可能な接続の種類は、 **[OLE DB]** 、 **[ODBC]** 、 **[ADO]** 、 **[ADO.NET]** 、および **[SQLMOBILE]** です。  
  
 **関連トピック:** [OLE DB 接続マネージャー](connection-manager/ole-db-connection-manager.md)、[ODBC 接続マネージャー](connection-manager/odbc-connection-manager.md)、[ADO 接続マネージャー](connection-manager/ado-connection-manager.md)、[ADO.NET 接続マネージャー](connection-manager/ado-net-connection-manager.md)、[SQL Server Compact Edition 接続マネージャー](connection-manager/sql-server-compact-edition-connection-manager.md)  
  
 **Connection**  
 定義済みの接続マネージャーの一覧から接続を選択します。 新しい接続を作成するには、[\<**新しい接続...** >] を選択します。  
  
 **[SQLSourceType]**  
 タスクが実行する SQL ステートメントのソースの種類を選択します。  
  
 SQL 実行タスクが使用する接続マネージャーの種類によって、パラメーター化された SQL ステートメントで特定のパラメーター マーカーを使用する必要があります。  
  
 **関連トピック:** パラメーター化 SQL コマンドのセクションを実行している[SQL 実行タスク](control-flow/execute-sql-task.md)  
  
 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|説明|  
|-----------|-----------------|  
|**[直接入力]**|Transact-SQL ステートメントをソースに設定します。 この値を選択すると、動的オプション **[SQLStatement]** が表示されます。|  
|**[ファイル接続]**|Transact-SQL ステートメントを含んでいるファイルを選択します。 この値を設定すると、動的オプション **[ファイル接続]** が表示されます。|  
|**変数**|Transact-SQL ステートメントを定義する変数をソースに設定します。 この値を選択すると、動的オプション **[SourceVariable]** が表示されます。|  
  
 **[QueryIsStoredProcedure]**  
 実行が指定された SQL ステートメントがストアド プロシージャかどうかを示します。 このプロパティは、タスクが ADO 接続マネージャーを使用する場合のみ、読み取り/書き込みになります。 それ以外の場合、このプロパティは読み取り専用となり、その値は `false` となります。  
  
 **[BypassPrepare]**  
 SQL ステートメントが準備されているかどうかを示します。  `true` の場合は準備がスキップされ、`false` の場合は実行の前に SQL ステートメントが準備されます。 このオプションは、準備をサポートしている OLE DB 接続の場合のみ使用可能です。  
  
 **関連トピック:** [準備実行](../relational-databases/native-client-odbc-queries/executing-statements/prepared-execution.md)  
  
 **[参照]**  
 **[開く]** ダイアログ ボックスを使用して、SQL ステートメントを含むファイルの場所を指定します。 ファイルを選択して、ファイルの内容を SQL ステートメントとして **[SQLStatement]** プロパティにコピーします。  
  
 **[クエリの作成]**  
 クエリの作成に使用するグラフィカルなツールである **[クエリ ビルダー]** ダイアログ ボックスを使用して SQL ステートメントを作成します。 このオプションは、 **[SQLSourceType]** オプションが **[直接入力]** に設定されている場合に使用可能です。  
  
 **[クエリの解析]**  
 SQL ステートメントの構文を検証します。  
  
## <a name="sqlsourcetype-dynamic-options"></a>[SQLSourceType] の動的オプション  
  
### <a name="sqlsourcetype--direct-input"></a>[SQLSourceType] = [直接入力]  
 **[SQLStatement]**  
 実行する SQL ステートメントをオプション ボックスに入力するか、参照ボタン ([...]) をクリックして **[SQL クエリの入力]** ダイアログ ボックスに SQL ステートメントを入力するか、 **[クエリの作成]** をクリックして **[クエリ ビルダー]** ダイアログ ボックスでステートメントを作成します。  
  
 **関連トピック:** [クエリ ビルダー](../../2014/integration-services/query-builder.md)  
  
### <a name="sqlsourcetype--file-connection"></a>[SQLSourceType] = [ファイル接続]  
 **[FileConnection]**  
 既存のファイル接続マネージャーを選択するか、[\<**新しい接続...** >] をクリックして新しい接続マネージャーを作成します。  
  
 **関連トピック:** [ファイル接続マネージャー](connection-manager/file-connection-manager.md)、[ファイル接続マネージャー エディター](../../2014/integration-services/file-connection-manager-editor.md)  
  
### <a name="sqlsourcetype--variable"></a>[SQLSourceType] = [変数]  
 **[SourceVariable]**  
 既存の変数を選択するか、\<**新しい変数...** > をクリックして新しい変数を作成します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41; の変数](integration-services-ssis-variables.md)、[変数の追加](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>関連項目  
 [Integration Services のエラーおよびメッセージのリファレンス](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [SQL 実行タスク エディター&#40;パラメーター マッピング ページ&#41;](../../2014/integration-services/execute-sql-task-editor-parameter-mapping-page.md)   
 [SQL 実行タスク エディター&#40;結果セット ページ&#41;](../../2014/integration-services/execute-sql-task-editor-result-set-page.md)  
  
  
