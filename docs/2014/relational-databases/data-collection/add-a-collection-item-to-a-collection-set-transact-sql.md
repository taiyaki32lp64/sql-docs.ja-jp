---
title: コレクション アイテムをコレクション セットに追加する (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- collection items [SQL Server]
- collection sets [SQL Server], adding items
ms.assetid: 9fe6454e-8c0e-4b50-937b-d9871b20fd13
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9f3e7c74fcaebb0aaaf246cba94e32c6b602b6e5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62873588"
---
# <a name="add-a-collection-item-to-a-collection-set-transact-sql"></a>コレクション アイテムをコレクション セットに追加する (Transact-SQL)
  データ コレクターに備わっているストアド プロシージャを使用して、コレクション アイテムを既存のコレクション セットに追加できます。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]のクエリ エディターを使用して、次の手順を実行します。  
  
### <a name="add-a-collection-item-to-a-collection-set"></a>コレクション アイテムのコレクション セットへの追加  
  
1.  **sp_syscollector_stop_collection_set** ストアド プロシージャを実行して、アイテムを追加するコレクション セットを停止します。 たとえば、"Test Collection Set" という名前のコレクション セットを停止するには、次のステートメントを実行します。  
  
    ```sql  
    USE msdb  
    DECLARE @csid int  
    SELECT @csid = collection_set_id  
    FROM syscollector_collection_sets  
    WHERE name = 'Test Collection Set'  
    SELECT @csid  
    EXEC dbo.sp_syscollector_stop_collection_set @collection_set_id = @csid  
    ```  
  
    > [!NOTE]  
    >  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でオブジェクト エクスプローラーを使用してコレクション セットを停止することもできます。 詳細については、「 [コレクション セットの開始または停止](start-or-stop-a-collection-set.md)」を参照してください。  
  
2.  コレクション アイテムを追加するコレクション セットを宣言します。 次のコードは、コレクション セット ID を宣言する例です。  
  
    ```sql  
    DECLARE @collection_set_id_1 int  
    SELECT @collection_set_id_1 = collection_set_id FROM [msdb].[dbo].[syscollector_collection_sets]  
    WHERE name = N'Test Collection Set'; -- name of collection set  
    ```  
  
3.  コレクター型を宣言します。 次のコードは、ジェネリック T-SQL Query コレクター型を宣言する例です。  
  
    ```sql  
    DECLARE @collector_type_uid_1 uniqueidentifier  
    SELECT @collector_type_uid_1 = collector_type_uid FROM [msdb].[dbo].[syscollector_collector_types]   
       WHERE name = N'Generic T-SQL Query Collector Type';  
    ```  
  
     次のコードを実行して、インストールされているコレクター型の一覧を取得できます。  
  
    ```sql  
    USE msdb  
    SELECT * from syscollector_collector_types  
    GO  
    ```  
  
4.  **sp_syscollector_create_collection_item** ストアド プロシージャを実行してコレクション アイテムを作成します。 コレクション アイテムが目的のコレクター型に必要なスキーマにマップされるように、コレクション アイテムのスキーマを宣言する必要があります。 ジェネリック T-SQL Query の入力スキーマを使用する例を次に示します。  
  
    ```sql  
    DECLARE @collection_item_id int;  
    EXEC [msdb].[dbo].[sp_syscollector_create_collection_item]   
    @name=N'OS Wait Stats', --name of collection item  
    @parameters=N'  
    <ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
     <Query>  
      <Value>select * from sys.dm_os_wait_stats</Value>  
      <OutputTable>os_wait_stats</OutputTable>  
    </Query>  
    </ns:TSQLQueryCollector>',  
    @collection_item_id = @collection_item_id OUTPUT,  
    @frequency = 60,  
    @collection_set_id = @collection_set_id_1, --- Provides the collection set ID number  
    @collector_type_uid = @collector_type_uid_1 -- Provides the collector type UID  
    SELECT @collection_item_id     
    ```  
  
5.  更新されたコレクション セットを開始する前に、次のクエリを実行して新しいコレクション アイテムが作成されていることを確認します。  
  
    ```xaml  
    USE msdb  
    SELECT * from syscollector_collection_sets  
    SELECT * from syscollector_collection_items  
    GO  
    ```  
  
     コレクション セットとそのコレクション アイテムは、 **[結果]** タブに表示されます。  
  
## <a name="see-also"></a>関連項目  
 [ジェネリック T-SQL Query コレクター型を使用するカスタム コレクション セットの作成 &#40;Transact-SQL&#41;](create-custom-collection-set-generic-t-sql-query-collector-type.md)   
 [データ コレクター ストアド プロシージャ &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql)  
  
  
