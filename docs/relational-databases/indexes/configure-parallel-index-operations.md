---
title: 並列インデックス操作の構成 | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index parallel operations [SQL Server]
- processors [SQL Server], parallel index operations
- max degree of parallelism option
- MAXDOP index option, parallel index operations
- parallel index operations [SQL Server]
ms.assetid: 8ec8c71e-5fc1-443a-92da-136ee3fc7f88
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 627fa6a19c88507034bfbd8a7236b94e17242851
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908128"
---
# <a name="configure-parallel-index-operations"></a>並列インデックス操作の構成
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

このトピックでは、並列処理の最大限度に関する定義と、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用してこの設定を変更する方法について説明します。 

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise 以上を実行するマルチプロセッサ システムでは、他のクエリと同様、このステートメントに関連付けられているスキャン操作、並べ替え操作、インデックス操作などの実行に、インデックスのステートメントで複数のプロセッサ (CPU) が使用される場合があります。 1 つのインデックス ステートメントの実行に使用される CPU の数は、[max degree of parallelism](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) サーバー構成オプション、現在のワークロード、およびインデックス統計によって決まります。 max degree of parallelism オプションによって、並列プランの実行で使用するプロセッサの最大数が決まります。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] によりシステムがビジー状態であることが検出されると、ステートメントの実行が開始される前に、インデックス操作の並列処理の次数が自動的に削減されます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] では、パーティション分割されていないインデックスの先頭のキー列で個々の値の数が制限されている場合や、個々の値の頻度が大きく異なる場合に、並列処理の次数を減らすこともできます。 詳細については、「[クエリ処理アーキテクチャ ガイド](../../relational-databases/query-processing-architecture-guide.md#parallel-query-processing)」を参照してください。 
  
> [!NOTE]  
> 並列インデックス操作は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のすべてのエディションで使用できるわけではありません。 詳細については、「 [SQL Server 2016 の各エディションがサポートする機能](../../sql-server/editions-and-components-of-sql-server-2016.md)」を参照してください。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [セキュリティ](#Security)  
  
-   **並列処理の最大限度を設定するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   通常は、クエリ オプティマイザーによって使用されるプロセッサ数で、最適なパフォーマンスが得られます。 ただし、非常に大きなインデックスの作成、再構築、または削除などの操作ではリソースが集中的に消費されるので、インデックス操作中に、他のアプリケーションやデータベース操作でリソースが不足する可能性があります。 この問題が発生した場合は、インデックス操作に使用するプロセッサ数を制限することで、インデックス ステートメントの実行に使用される最大プロセッサ数を手動で構成できます。  
  
-   MAXDOP インデックス オプションは、このオプションを指定しているクエリに関してのみ、max degree of parallelism 構成オプションをオーバーライドします。 次の表に、max degree of parallelism 構成オプションと MAXDOP インデックス オプションで指定できる有効な整数値を示します。  
  
    |[値]|Description|  
    |-----------|-----------------|  
    |0|現在のシステム ワークロードに応じて、使用する CPU 数をサーバーが決定するように指定します。 この値は既定値であり、推奨の設定です。|  
    |1|並列プラン生成を抑制します。 操作は順番に実行されます。|  
    |2～64|プロセッサ数が指定値まで制限されます。 現在のワークロードによっては、使用されるプロセッサ数が少なくなる場合があります。 使用できる CPU 数よりも大きな値を指定した場合は、実際に使用できる CPU 数が使用されます。|  
  
-   インデックスの並列実行と MAXDOP インデックス オプションは、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントに適用されます。  
  
    -   [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md)  
  
    -   [ALTER INDEX (...)REBUILD](../../t-sql/statements/alter-index-transact-sql.md)  
  
    -   [DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md) (クラスター化インデックスのみに適用されます。)  
  
    -   [ALTER TABLE ADD (インデックス) CONSTRAINT](../../t-sql/statements/alter-table-table-constraint-transact-sql.md) 
  
    -   [ALTER TABLE DROP (クラスター化インデックス) CONSTRAINT](../../t-sql/statements/alter-table-table-constraint-transact-sql.md)   
  
-   `ALTER INDEX (...) REORGANIZE` ステートメントには、MAXDOP インデックス オプションを指定できません。  
  
-   クエリ オプティマイザーで構築操作に 2 次以上の並列処理が適用されると、並べ替えを必要とするパーティション インデックス操作に必要なメモリ容量がさらに大きくなる場合があります。 並列処理の次数が高いと、必要なメモリ容量も大きくなります。 詳細については、「 [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)」を参照してください。  
  
###  <a name="Security"></a> <a name="Permissions"></a> アクセス許可  
 テーブルまたはビューに対する `ALTER` 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-set-max-degree-of-parallelism-on-an-index"></a>インデックスに並列処理の最大限度を設定するには  
  
1.  オブジェクト エクスプローラーで、インデックスの並列処理の最大限度を設定するテーブルが格納されているデータベースをプラス記号をクリックして展開します。  
  
2.  **[テーブル]** フォルダーを展開します。  
  
3.  インデックスの並列処理の最大限度を設定するテーブルをプラス記号をクリックして展開します。  
  
4.  **[インデックス]** フォルダーを展開します。  
  
5.  並列処理の最大限度を設定するインデックスを右クリックし、 **[プロパティ]** を選択します。  
  
6.  **[ページの選択]** の **[オプション]** を選択します。  
  
7.  **[並列処理の最大限度]** を選択し、1 ～ 64 の範囲の値を入力します。  
  
8.  **[OK]** をクリックします。  

##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-set-max-degree-of-parallelism-on-an-existing-index"></a>既存のインデックスに並列処理の最大限度を設定するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```sql  
    USE AdventureWorks2012;   
    GO  
    /*Alters the IX_ProductVendor_VendorID index on the Purchasing.ProductVendor table so that, if the server has eight or more processors, the Database Engine will limit the execution of the index operation to eight or fewer processors.  
    */  
    ALTER INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor  
    REBUILD WITH (MAXDOP=8);   
    GO  
    ```  
  
 詳細については、「[ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)」を参照してください。  
  
#### <a name="set-max-degree-of-parallelism-on-a-new-index"></a>新しいインデックスに並列処理の最大限度を設定する方法  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```sql  
    USE AdventureWorks2012;  
    GO  
    CREATE INDEX IX_ProductVendor_NewVendorID   
    ON Purchasing.ProductVendor (BusinessEntityID)  
    WITH (MAXDOP=8);  
    GO  
    ```  
 
## <a name="see-also"></a>参照
[クエリ処理アーキテクチャ ガイド](../../relational-databases/query-processing-architecture-guide.md#parallel-query-processing)    
[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)     
[ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)     
[DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)      
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)      
[ALTER TABLE table_constraint &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-table-constraint-transact-sql.md)       
[ALTER TABLE index_option &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-index-option-transact-sql.md)    
