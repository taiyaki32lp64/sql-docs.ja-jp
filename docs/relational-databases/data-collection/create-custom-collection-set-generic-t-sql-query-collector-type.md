---
title: カスタム コレクション セットの作成 - ジェネリック T-SQL Query コレクター型
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- T-SQL Query collector type
- collection sets [SQL Server], creating custom
ms.assetid: 6b06db5b-cfdc-4ce0-addd-ec643460605b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b27dda40294185f923d74b61dfd1b10ce7301ba9
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74055577"
---
# <a name="create-custom-collection-set---generic-t-sql-query-collector-type"></a>カスタム コレクション セットの作成 - ジェネリック T-SQL Query コレクター型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  データ コレクターで用意されているストアド プロシージャを使用して、ジェネリック T-SQL Query コレクター型を使用するコレクション アイテムを含むカスタム コレクション セットを作成できます。 この作業には、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のクエリ エディターを使用した次の手順の実行も含まれます。  
  
-   アップロードのスケジュールを構成する。  
  
-   コレクション セットを定義して作成する。  
  
-   コレクション アイテムを定義して作成する。  
  
-   コレクション セットとコレクション アイテムが存在することを確認する。  
  
> [!NOTE]  
>  カスタム コレクション セットを作成する前に、データ コレクションのパラメーターを構成する必要があります。 詳細については、「[データ コレクションのパラメーターの構成 &#40;Transact-SQL&#41;](../../relational-databases/data-collection/configure-data-collection-parameters-transact-sql.md)」を参照してください。  
  
### <a name="define-and-create-the-collection-set"></a>コレクション セットを定義して作成する  
  
1.  sp_syscollector_create_collection_set ストアド プロシージャを使用して、新しいコレクション セットを定義します。  
  
    ```  
    USE msdb;  
    DECLARE @collection_set_id int;  
    DECLARE @collection_set_uid uniqueidentifier;  
    EXEC sp_syscollector_create_collection_set   
        @name=N'DMV Test 1',   
        @collection_mode=0,   
        @description=N'This is a test collection set',   
        @logging_level=1,   
        @days_until_expiration=14,   
        @schedule_name=N'CollectorSchedule_Every_15min',   
        @collection_set_id=@collection_set_id OUTPUT,   
        @collection_set_uid=@collection_set_uid OUTPUT;  
    SELECT @collection_set_id, @collection_set_uid;  
    ```  
  
     コレクション モードは、0 (キャッシュ) または 1 (非キャッシュ) に設定できます。  
  
     ログ記録レベルは、0、1、または 2 に設定できます。  
  
     データ コレクターには、以下の事前に構成されたスケジュールが用意されています。  
  
    -   CollectorSchedule_Every_5min  
  
    -   CollectorSchedule_Every_10min  
  
    -   CollectorSchedule_Every_15min  
  
    -   CollectorSchedule_Every_30min  
  
    -   CollectorSchedule_Every_60min  
  
    -   CollectorSchedule_Every_6h  
  
     用意されているスケジュールのいずれも使用しない場合は、コレクション セットに新しいスケジュールを作成して使用できます。 詳細については、「 [スケジュールの作成とジョブへのアタッチ](../../ssms/agent/create-and-attach-schedules-to-jobs.md)」を参照してください。  
  
### <a name="define-and-create-a-collection-item"></a>コレクション アイテムを定義して作成する  
  
1.  新しいコレクション アイテムはインストール済みのジェネリックコレクター型に基づいているため、次のコードを実行して、ジェネリック T-SQL Query コレクター型に対応するように GUID を設定できます。  
  
    ```sql  
    DECLARE @collector_type_uid uniqueidentifier;  
    SELECT @collector_type_uid = collector_type_uid FROM [msdb].[dbo].[syscollector_collector_types]   
    WHERE name = N'Generic T-SQL Query Collector Type';  
    DECLARE @collection_item_id int;  
    ```  
  
2.  sp_syscollector_create_collection_item ストアド プロシージャを使用してコレクション アイテムを作成します。 コレクション アイテムがジェネリック T-SQL Query コレクター型に必要なスキーマにマップされるように、コレクション アイテムのスキーマを宣言します。  
  
    ```sql  
    EXEC sp_syscollector_create_collection_item   
        @name=N'Query Stats - Test 1',   
        @parameters=N'  
            <ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
            <Query>  
            <Value>SELECT * FROM sys.dm_exec_query_stats</Value>  
            <OutputTable>dm_exec_query_stats</OutputTable>  
            </Query>  
            </ns:TSQLQueryCollector>',   
        @collection_item_id=@collection_item_id OUTPUT,   
        @frequency=5,   
        @collection_set_id=@collection_set_id,   
        @collector_type_uid=@collector_type_uid;  
    SELECT @collection_item_id;  
    ```  
  
### <a name="verify-that-the-new-collection-set-and-collection-item-exist"></a>新しいコレクション セットとコレクション アイテムが存在することを確認する  
  
1.  新しいコレクション セットを開始する前に、次のクエリを実行して新しいコレクション セットとそのコレクション アイテムが作成されていることを確認します。  
  
    ```sql  
    USE msdb;  
    SELECT * FROM syscollector_collection_sets;  
    SELECT * FROM syscollector_collection_items;  
    GO  
    ```  
  
     [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で目視で確認することもできます。 オブジェクト エクスプローラーで、 **[管理]** ノードを展開し、 **[データ コレクション]** を展開します。 新しいコレクション セットが表示されます。 コレクション セットに赤い円のアイコンが付いている場合、コレクション セットが停止されていることを示します。  
  
## <a name="example"></a>例  
 次のコード サンプルは、上記の手順で説明されている例を組み合わせたものです。 コレクション セットのコレクション モードはキャッシュ モード (0) に設定されているため、コレクション アイテムに設定された収集頻度 (5 秒) は無視されます。 詳細については、「 [Data Collection](../../relational-databases/data-collection/data-collection.md)」を参照してください。  
  
```sql  
USE msdb;  
  
DECLARE @collection_set_id int;  
DECLARE @collection_set_uid uniqueidentifier  
  
EXEC dbo.sp_syscollector_create_collection_set  
    @name = N'DMV Stats Test 1',  
    @collection_mode = 0,  
    @description = N'This is a test collection set',  
    @logging_level=1,  
    @days_until_expiration = 14,  
    @schedule_name=N'CollectorSchedule_Every_15min',  
    @collection_set_id = @collection_set_id OUTPUT,  
    @collection_set_uid = @collection_set_uid OUTPUT;  
SELECT @collection_set_id,@collection_set_uid;  
  
DECLARE @collector_type_uid uniqueidentifier;  
SELECT @collector_type_uid = collector_type_uid FROM syscollector_collector_types   
WHERE name = N'Generic T-SQL Query Collector Type';  
  
DECLARE @collection_item_id int;  
EXEC sp_syscollector_create_collection_item  
@name= N'Query Stats - Test 1',  
@parameters=N'  
<ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
<Query>  
  <Value>select * from sys.dm_exec_query_stats</Value>  
  <OutputTable>dm_exec_query_stats</OutputTable>  
</Query>  
 </ns:TSQLQueryCollector>',  
    @collection_item_id = @collection_item_id OUTPUT,  
    @frequency = 5, -- This parameter is ignored in cached mode  
    @collection_set_id = @collection_set_id,  
    @collector_type_uid = @collector_type_uid;  
SELECT @collection_item_id;  
  
GO  
```  
  
## <a name="see-also"></a>参照  
 [データ コレクター ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [[スケジュールの管理]](../../ssms/agent/manage-schedules.md)   
 [コレクション セットの開始または停止](../../relational-databases/data-collection/start-or-stop-a-collection-set.md)  
  
  
