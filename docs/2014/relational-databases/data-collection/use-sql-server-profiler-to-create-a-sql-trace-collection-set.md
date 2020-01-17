---
title: SQL Server Profiler を使用して SQL トレース コレクション セット (SQL Server Management Studio) を作成する |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- SQL Trace collector set
ms.assetid: b6941dc0-50f5-475d-82eb-ce7c68117489
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a9e37fd917dc2716967623648a62057e45df73dc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62873340"
---
# <a name="use-sql-server-profiler-to-create-a-sql-trace-collection-set-sql-server-management-studio"></a>SQL Server Profiler を使用して SQL トレース コレクション セットを作成する (SQL Server Management Studio)
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] のサーバー側のトレース機能を利用して、ジェネリック SQL トレース コレクター型を使用するコレクション セットを作成するためのトレース定義をエクスポートできます。 このプロセスは 2 つの部分で構成されます。  
  
1.  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] トレースの作成とエクスポート  
  
2.  エクスポートされたトレースに基づく新しいコレクション セットのスクリプト化  
  
 次の手順のシナリオでは、完了に 80 ミリ秒以上かかるストアド プロシージャに関するデータを収集します。 この手順を完了するには、次の操作を実行できる必要があります。  
  
-   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を使用したトレースの作成および構成  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用したクエリの表示、編集、および実行  
  
### <a name="create-and-export-a-sql-server-profiler-trace"></a>SQL Server Profiler トレースの作成とエクスポート  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]を開きます ( **[ツール]** メニューの **[SQL Server Profiler]** をクリックします)。  
  
2.  **[サーバーへの接続]** ダイアログ ボックスで、 **[キャンセル]** をクリックします。  
  
3.  このシナリオでは、実行時間の値が既定でミリ秒で表示されるように設定されていることを確認します。 これを行うには、次の手順を実行します。  
  
    1.  **[ツール]** メニューの **[オプション]** をクリックします。  
  
    2.  **[表示オプション]** 領域で、[実行時間列の値をマイクロ秒で表示する] チェック ボックスがオフになっていることを確認します。  
  
    3.  **[OK]** をクリックして **[全般オプション]** ダイアログ ボックスを閉じます。  
  
4.  **[ファイル]** メニューの **[新しいトレース]** をクリックします。  
  
5.  **[サーバーへの接続]** ダイアログ ボックスで、接続するサーバーを選択して **[接続]** をクリックします。  
  
     **[トレースのプロパティ]** ダイアログ ボックスが表示されます。  
  
6.  **[全般]** タブで、次の操作を行います。  
  
    1.  **[トレース名]** ボックスに、トレースに使用する名前を入力します。 この例では、トレース名は「`SPgt80`」です。  
  
    2.  **[使用するテンプレート]** ボックスの一覧でトレースに使用するテンプレートを選択します。 この例では、 **[TSQL_SPs]** をクリックします。  
  
7.  **[イベントの選択]** タブで、次の操作を行います。  
  
    1.  トレースに使用するイベントを指定します。 この例では、 **[ExistingConnection]** と **[SP:Completed]** を除く **[イベント]** 列のすべてのチェック ボックスをオフにします。  
  
    2.  右上隅の **[すべての列を表示する]** チェック ボックスを選択します。  
  
    3.  **[SP:Completed]** 行をクリックします。  
  
    4.  行をスクロールして **[実行時間]** 列を表示し、 **[実行時間]** チェック ボックスを選択します。  
  
8.  右下隅の **[列フィルター]** をクリックし、 **[フィルターの編集]** ダイアログ ボックスを開きます。 **[フィルターの編集]** ダイアログ ボックスで、次の操作を行います。  
  
    1.  フィルター一覧で、 **[実行時間]** をクリックします。  
  
    2.  ブール演算子ウィンドウで、展開、**より大きいか等しい**ノードで、「`80`値、およびクリックとして **[ok]** します。  
  
9. **[実行]** をクリックしてトレースを開始します。  
  
10. ツール バーの **[選択されたトレースの停止]** または **[選択されたトレースの一時停止]** をクリックします。  
  
11. **[ファイル]** メニューで **[エクスポート]** 、 **[トレース定義のスクリプト]** の順にポイントし、 **[SQL トレース コレクション セット]** をクリックします。  
  
12. **[名前を付けてファイルを保存]** ダイアログ ボックスの **[ファイル名]** ボックスに、トレース定義に使用する名前を入力し、目的の場所に保存します。 この例では、ファイル名はトレース名 (SPgt80) と同じです。  
  
13. ファイルが正常に保存されたことを通知するメッセージを受信したら **[OK]** をクリックし、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]を閉じます。  
  
### <a name="script-a-new-collection-set-from-a-sql-server-profiler-trace"></a>SQL Server Profiler トレースに基づく新しいコレクション セットのスクリプト化  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で **[ファイル]** メニューの **[開く]** をポイントし、 **[ファイル]** をクリックします。  
  
2.  **[ファイルを開く]** ダイアログ ボックスで、前の手順で作成したファイル (SPgt80) を探して開きます。  
  
     保存したトレース情報がクエリ ウィンドウで開かれ、新しいコレクション セットを作成するために実行できるスクリプトにマージされます。  
  
3.  スクリプトをスクロールし、スクリプトのコメント テキストに示されている次の置換を行います。  
  
    -   **SQLTrace Collection Set Name Here** をコレクション セットに使用する名前に置換します。 この例では、コレクション セット名は "`SPROC_CollectionSet`" です。  
  
    -   **SQLTrace Collection Item Name Here** をコレクション アイテムに使用する名前に置換します。 この例では、コレクション アイテム名は "`SPROC_Collection_Item`" です。  
  
4.  **[実行]** をクリックして、クエリを実行してコレクション セットを作成します。  
  
5.  [オブジェクト エクスプローラー] で、コレクション セットが作成されたことを確認します。 これを行うには、次の手順を実行します。  
  
    1.  **[管理]** を右クリックし、 **[更新]** をクリックします。  
  
    2.  **[管理]** 、 **[データ コレクション]** の順に展開します。  
  
     `SPROC_CollectionSet`と同じレベルでコレクション セットが表示されます、**システム データ コレクション セット**ノード。 既定では、このコレクション セットは無効になっています。  
  
6.  オブジェクト エクスプローラーを使用して、コレクション モードやアップロード スケジュールなどの SPROC_CollectionSet のプロパティを編集します。 編集方法は、データ コレクターで用意されているシステム データ コレクション セットの場合と同じです。  
  
## <a name="example"></a>例  
 次のコード例は、前述の手順を実行することによって得られる最終的なスクリプトです。  
  
```  
/*************************************************************/  
-- SQL Trace collection set generated from SQL Server Profiler  
-- Date: 11/19/2007  12:55:31 AM  
/*************************************************************/  
  
USE msdb  
GO  
  
BEGIN TRANSACTION  
BEGIN TRY  
  
-- Define collection set  
-- ***  
-- *** Replace 'SqlTrace Collection Set Name Here' in the   
-- *** following script with the name you want  
-- *** to use for the collection set.  
-- ***  
DECLARE @collection_set_id int;  
EXEC [dbo].[sp_syscollector_create_collection_set]  
    @name = N'SPROC_CollectionSet',  
    @schedule_name = N'CollectorSchedule_Every_15min',  
    @collection_mode = 0, -- cached mode needed for Trace collections  
    @logging_level = 0, -- minimum logging  
    @days_until_expiration = 5,  
    @description = N'Collection set generated by SQL Server Profiler',  
    @collection_set_id = @collection_set_id output;  
SELECT @collection_set_id;  
  
-- Define input and output variables for the collection item.  
DECLARE @trace_definition xml;  
DECLARE @collection_item_id int;  
  
-- Define the trace parameters as an XML variable  
SELECT @trace_definition = convert(xml,   
N'<ns:SqlTraceCollector xmlns:ns"DataCollectorType" use_default="0">  
<Events>  
  <EventType name="Sessions">  
    <Event id="17" name="ExistingConnection" columnslist="1,2,14,26,3,35,12" />  
  </EventType>  
  <EventType name="Stored Procedures">  
    <Event id="43" name="SP:Completed" columnslist="1,2,26,34,3,35,12,13,14,22" />  
  </EventType>  
</Events>  
<Filters>  
  <Filter columnid="13" columnname="Duration" logical_operator="AND" comparison_operator="GE" value="80000L" />  
</Filters>  
</ns:SqlTraceCollector>  
');  
  
-- Retrieve the collector type GUID for the trace collector type.  
DECLARE @collector_type_GUID uniqueidentifier;  
SELECT @collector_type_GUID = collector_type_uid FROM [dbo].[syscollector_collector_types] WHERE name = N'Generic SQL Trace Collector Type';  
  
-- Create the trace collection item.  
-- ***  
-- *** Replace 'SqlTrace Collection Item Name Here' in   
-- *** the following script with the name you want to  
-- *** use for the collection item.  
-- ***  
EXEC [dbo].[sp_syscollector_create_collection_item]  
   @collection_set_id = @collection_set_id,  
   @collector_type_uid = @collector_type_GUID,  
   @name = N'SPROC_Collection_Item',  
   @frequency = 900, -- specified the frequency for checking to see if trace is still running  
   @parameters = @trace_definition,  
   @collection_item_id = @collection_item_id output;  
SELECT @collection_item_id;  
  
COMMIT TRANSACTION;  
END TRY  
  
BEGIN CATCH  
ROLLBACK TRANSACTION;  
DECLARE @ErrorMessage nvarchar(4000);  
DECLARE @ErrorSeverity int;  
DECLARE @ErrorState int;  
DECLARE @ErrorNumber int;  
DECLARE @ErrorLine int;  
DECLARE @ErrorProcedure nvarchar(200);  
SELECT @ErrorLine = ERROR_LINE(),  
       @ErrorSeverity = ERROR_SEVERITY(),  
       @ErrorState = ERROR_STATE(),  
       @ErrorNumber = ERROR_NUMBER(),  
       @ErrorMessage = ERROR_MESSAGE(),  
       @ErrorProcedure = ISNULL(ERROR_PROCEDURE(), '-');  
RAISERROR (14684, @ErrorSeverity, 1 , @ErrorNumber, @ErrorSeverity, @ErrorState, @ErrorProcedure, @ErrorLine, @ErrorMessage);  
END CATCH;  
GO  
```  
  
  
