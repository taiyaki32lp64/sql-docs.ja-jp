---
title: OLE DB 変換先エディター ([接続マネージャー] ページ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.oledbdestadapter.connection.f1
helpviewer_keywords:
- OLE DB Destination Editor
ms.assetid: ae2200c6-8ba0-49b7-b01a-53425b84d2ed
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 436b758abdde0c05539bc17aabd2c11b240642df
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66057134"
---
# <a name="ole-db-destination-editor-connection-manager-page"></a>[OLE DB 変換先エディター] ([接続マネージャー] ページ)
  **[OLE DB 変換先エディター]** ダイアログ ボックスの **[接続マネージャー]** ページを使用すると、変換先の OLE DB 接続を選択できます。 さらにこのページを使用して、データベースのテーブルやビューを選択できます。  
  
> [!NOTE]  
>  `CommandTimeout` OLE DB 変換先のプロパティでは使用できません、 **OLE DB 変換先エディター**を使用して設定できますが、**高度なエディター**します。 また、一部の高速読み込みオプションは **[詳細エディター]** でしか使用できません。 これらのプロパティの詳細については、「 [OLE DB カスタム プロパティ](data-flow/ole-db-custom-properties.md)」の OLE DB 変換先に関するセクションを参照してください。  
  
 OLE DB 変換先の詳細については、「 [OLE DB Destination](data-flow/ole-db-destination.md)」を参照してください。  
  
## <a name="static-options"></a>静的オプション  
 **[キャッシュなし]**  
 既存の接続マネージャーを一覧から選択するか、 **[新規作成]** をクリックして新しい接続を作成します。  
  
 **[新規作成]**  
 **[OLE DB 接続マネージャーの構成]** ダイアログ ボックスを使用して、新しい接続マネージャーを作成します。  
  
 **[データ アクセス モード]**  
 データを変換先に読み込む方法を指定します。 2 バイト文字セット (DBCS) データを読み込むには、高速読み込みオプションのいずれかを使用する必要があります。 一括挿入用に最適化された高速読み込みデータ アクセス モードの詳細については、「 [OLE DB 変換先](data-flow/ole-db-destination.md)」を参照してください。  
  
|オプション|説明|  
|------------|-----------------|  
|[テーブルまたはビュー]|データを OLE DB 変換先のテーブルまたはビューに読み込みます。|  
|[テーブルまたはビュー - 高速読み込み]|高速読み込みオプションを使用し、データを OLE DB 変換先のテーブルまたはビューに読み込みます。 一括挿入用に最適化された高速読み込みデータ アクセス モードの詳細については、「 [OLE DB 変換先](data-flow/ole-db-destination.md)」を参照してください。|  
|[テーブル名またはビュー名の変数]|テーブル名またはビュー名を変数で指定します。<br /><br /> **関連情報**:[パッケージで変数を使用する](../../2014/integration-services/use-variables-in-packages.md)|  
|[テーブル名またはビュー名の変数 - 高速読み込み]|高速読み込みオプションを使用し、テーブル名またはビュー名を変数で指定します。 一括挿入用に最適化された高速読み込みデータ アクセス モードの詳細については、「 [OLE DB 変換先](data-flow/ole-db-destination.md)」を参照してください。|  
|[SQL コマンド]|SQL クエリを使用し、データを OLE DB 変換先に読み込みます。|  
  
 **プレビュー**  
 **[クエリ結果のプレビュー]** ダイアログ ボックスを使用して、結果をプレビューします。 プレビューでは、最大で 200 行を表示できます。  
  
## <a name="data-access-mode-dynamic-options"></a>データ アクセス モードの動的オプション  
 **[データ アクセス モード]** の各設定には、その設定に固有のオプションの動的なセットが表示されます。 次のセクションでは、各 **[データ アクセス モード]** 設定で使用可能な各動的オプションについて説明します。  
  
### <a name="data-access-mode--table-or-view"></a>[データ アクセス モード] = [テーブルまたはビュー]  
 **[テーブル名またはビュー名]**  
 データ ソースで使用できるテーブルまたはビューの一覧から、テーブルまたはビューの名前を選択します。  
  
 **[新規作成]**  
 **[テーブルの作成]** ダイアログ ボックスを使用して新しいテーブルを作成します。  
  
> [!NOTE]  
>  **[新規作成]** をクリックすると、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] により、接続されているデータ ソースに基づいて既定の CREATE TABLE ステートメントが生成されます。 基になるテーブルの列に FILESTREAM 属性が宣言されていても、この既定の CREATE TABLE ステートメントには FILESTREAM 属性が含まれません。 FILESTREAM 属性を使用して [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] コンポーネントを実行するには、まず対象データベースに FILESTREAM ストレージを実装します。 次に、 **[テーブルの作成]** ダイアログ ボックスで CREATE TABLE ステートメントに FILESTREAM 属性を追加します。 詳細については、「[バイナリ ラージ オブジェクト &#40;Blob&#41; データ &#40;SQL Server&#41;](../relational-databases/blob/binary-large-object-blob-data-sql-server.md)」を参照してください。  
  
### <a name="data-access-mode--table-or-view---fast-load"></a>[データ アクセス モード] = [テーブルまたはビュー - 高速読み込み]  
 **[テーブル名またはビュー名]**  
 この一覧を使用してデータベースからテーブルまたはビューを選択するか、 **[新規作成]** をクリックして新しいテーブルを作成します。  
  
 **[新規作成]**  
 **[テーブルの作成]** ダイアログ ボックスを使用して新しいテーブルを作成します。  
  
> [!NOTE]  
>  **[新規作成]** をクリックすると、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] により、接続されているデータ ソースに基づいて既定の CREATE TABLE ステートメントが生成されます。 基になるテーブルの列に FILESTREAM 属性が宣言されていても、この既定の CREATE TABLE ステートメントには FILESTREAM 属性が含まれません。 FILESTREAM 属性を使用して [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] コンポーネントを実行するには、まず対象データベースに FILESTREAM ストレージを実装します。 次に、 **[テーブルの作成]** ダイアログ ボックスで CREATE TABLE ステートメントに FILESTREAM 属性を追加します。 詳細については、「[バイナリ ラージ オブジェクト &#40;Blob&#41; データ &#40;SQL Server&#41;](../relational-databases/blob/binary-large-object-blob-data-sql-server.md)」を参照してください。  
  
 **[ID を保持する]**  
 データが読み込まれるときに ID 値をコピーするかどうかを指定します。 このプロパティは、高速読み取りオプションを指定した場合にのみ使用できます。 このプロパティの既定値は `false` です。  
  
 **[NULL を保持する]**  
 データが読み込まれるときに NULL 値をコピーするかどうかを指定します。 このプロパティは、高速読み取りオプションを指定した場合にのみ使用できます。 このプロパティの既定値は `false` です。  
  
 **[テーブル ロック]**  
 読み込み中にテーブルをロックするかどうかを指定します。 このプロパティの既定値は `true` です。  
  
 **CHECK 制約**  
 データの読み込み中に変換先で制約をチェックするかどうかを指定します。 このプロパティの既定値は `true` です。  
  
 **[バッチごとの行数]**  
 バッチ内の行数を指定します。 このプロパティの既定値は、 **-1**です。これは、割り当てられた値がないことを示します。  
  
> [!NOTE]  
>  このプロパティにカスタム値を割り当てない場合、 **[OLE DB 変換先エディター]** のテキスト ボックスをクリアします。  
  
 **[挿入コミット サイズの最大値]**  
 高速読み込み操作の実行中に OLE DB 変換先でコミットを試行するバッチ サイズを指定します。 値 **0** は、すべての行が処理された後、すべてのデータを 1 つのバッチでコミットすることを示します。  
  
> [!NOTE]  
>  値を **0** にすると、OLE DB 変換先と別のデータ フロー コンポーネントが同じソース テーブルを更新している場合に、実行中のパッケージが応答を停止する可能性があります。 パッケージが停止しないようにするには、 **[挿入コミット サイズの最大値]** オプションを **2147483647**に設定します。  
  
 このプロパティに値を指定すると、変換先で **[挿入コミット サイズの最大値]** 未満の行数のバッチがコミットされます。値を指定しない場合は、現在処理されているバッファー内の残りの行数がコミットされます。  
  
> [!NOTE]  
>  変換先で制約が失敗すると、 **[挿入コミット サイズの最大値]** で定義された行数のバッチ全体が失敗します。  
  
### <a name="data-access-mode--table-name-or-view-name-variable"></a>[データ アクセス モード] = [テーブル名またはビュー名の変数]  
 **[変数名]**  
 テーブル名またはビュー名を含む変数を選択します。  
  
### <a name="data-access-mode--table-name-or-view-name-variable---fast-load"></a>[データ アクセス モード] = [テーブル名またはビュー名の変数 - 高速読み込み]  
 **[変数名]**  
 テーブル名またはビュー名を含む変数を選択します。  
  
 **[新規作成]**  
 **[テーブルの作成]** ダイアログ ボックスを使用して新しいテーブルを作成します。  
  
> [!NOTE]  
>  **[新規作成]** をクリックすると、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] により、接続されているデータ ソースに基づいて既定の CREATE TABLE ステートメントが生成されます。 基になるテーブルの列に FILESTREAM 属性が宣言されていても、この既定の CREATE TABLE ステートメントには FILESTREAM 属性が含まれません。 FILESTREAM 属性を使用して [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] コンポーネントを実行するには、まず対象データベースに FILESTREAM ストレージを実装します。 次に、 **[テーブルの作成]** ダイアログ ボックスで CREATE TABLE ステートメントに FILESTREAM 属性を追加します。 詳細については、「[バイナリ ラージ オブジェクト &#40;Blob&#41; データ &#40;SQL Server&#41;](../relational-databases/blob/binary-large-object-blob-data-sql-server.md)」を参照してください。  
  
 **[ID を保持する]**  
 データが読み込まれるときに ID 値をコピーするかどうかを指定します。 このプロパティは、高速読み取りオプションを指定した場合にのみ使用できます。 このプロパティの既定値は `false` です。  
  
 **[NULL を保持する]**  
 データが読み込まれるときに NULL 値をコピーするかどうかを指定します。 このプロパティは、高速読み取りオプションを指定した場合にのみ使用できます。 このプロパティの既定値は `false` です。  
  
 **[テーブル ロック]**  
 読み込み中にテーブルをロックするかどうかを指定します。 このプロパティの既定値は `false` です。  
  
 **CHECK 制約**  
 タスクで制約をチェックするかどうかを指定します。 このプロパティの既定値は `false` です。  
  
 **[バッチごとの行数]**  
 バッチ内の行数を指定します。 このプロパティの既定値は、 **-1**です。これは、割り当てられた値がないことを示します。  
  
> [!NOTE]  
>  このプロパティにカスタム値を割り当てない場合、 **[OLE DB 変換先エディター]** のテキスト ボックスをクリアします。  
  
 **[挿入コミット サイズの最大値]**  
 高速読み込み操作の実行中に OLE DB 変換先でコミットを試行するバッチ サイズを指定します。 既定値の **2147483647** は、すべての行が処理された後、すべてのデータを 1 つのバッチでコミットすることを示します。  
  
> [!NOTE]  
>  値を **0** にすると、OLE DB 変換先と別のデータ フロー コンポーネントが同じソース テーブルを更新している場合に、実行中のパッケージが応答を停止する可能性があります。 パッケージが停止しないようにするには、 **[挿入コミット サイズの最大値]** オプションを **2147483647**に設定します。  
  
### <a name="data-access-mode--sql-command"></a>[データ アクセス モード] = [SQL コマンド]  
 **[SQL コマンド テキスト]**  
 SQL クエリのテキストを入力し、 **[クエリの作成]** をクリックしてクエリを作成するか、 **[参照]** をクリックしてクエリ テキストを含むファイルを指定します。  
  
> [!NOTE]  
>  OLE DB 変換先ではパラメーターがサポートされません。 パラメーター化された INSERT ステートメントを実行する必要がある場合は、OLE DB コマンド変換を検討してください。 詳細については、「 [OLE DB Command Transformation](data-flow/transformations/ole-db-command-transformation.md)」を参照してください。  
  
 **[クエリの作成]**  
 SQL クエリを視覚的に作成するには、 **[クエリ ビルダー]** ダイアログ ボックスを使用します。  
  
 **[参照]**  
 **[開く]** ダイアログ ボックスを使用して、SQL クエリのテキストが含まれているファイルを指定します。  
  
 **[クエリの解析]**  
 クエリ テキストの構文を検査します。  
  
## <a name="see-also"></a>参照  
 [Integration Services のエラーおよびメッセージのリファレンス](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [[OLE DB 変換先エディター] &#40;[マッピング] ページ&#41;](../../2014/integration-services/ole-db-destination-editor-mappings-page.md)   
 [[OLE DB 変換先エディター] &#40;[エラー出力] ページ&#41;](../../2014/integration-services/ole-db-destination-editor-error-output-page.md)   
 [OLE DB 変換先を使用してデータを読み込む](data-flow/load-data-by-using-the-ole-db-destination.md)  
  
  
