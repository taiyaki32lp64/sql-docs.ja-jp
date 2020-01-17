---
title: 並列インデックス操作の構成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 3a70d58caba2b2a443f0017c52611331e9257972
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63157480"
---
# <a name="configure-parallel-index-operations"></a>並列インデックス操作の構成
  このトピックでは、並列処理の最大限度に関する定義と、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用してこの設定を変更する方法について説明します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise 以上を実行するマルチプロセッサ コンピューターでは、他のクエリと同様に、インデックスのステートメントがこのステートメントに関連付けられているスキャン操作、並べ替え操作、インデックス操作などの実行に、複数のプロセッサを使用する場合があります。 1 つのインデックス ステートメントの実行に使用されるプロセッサの数は、 [max degree of parallelism](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) 構成オプション、現在のワークロード、およびインデックス統計によって決まります。 max degree of parallelism オプションによって、並列プランの実行で使用するプロセッサの最大数が決まります。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] によりシステムがビジー状態であることが検出されると、ステートメントの実行が開始される前に、インデックス操作の並列処理の次数が自動的に削減されます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] では、パーティション分割されていないインデックスの先頭のキー列で個々の値の数が制限されている場合や、個々の値の頻度が大きく異なる場合に、並列処理の次数を減らすこともできます。  
  
> [!NOTE]  
>  並列インデックス操作は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のすべてのエディションで使用できるわけではありません。 詳しくは「 [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)」をご覧ください。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **並列処理の最大限度を設定するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   通常は、クエリ オプティマイザーによって使用されるプロセッサ数で、最適なパフォーマンスが得られます。 ただし、非常に大きなインデックスの作成、再構築、または削除などの操作ではリソースが集中的に消費されるので、インデックス操作中に、他のアプリケーションやデータベース操作でリソースが不足する可能性があります。 この問題が発生した場合は、インデックス操作に使用するプロセッサ数を制限することで、インデックス ステートメントの実行に使用される最大プロセッサ数を手動で構成できます。  
  
-   MAXDOP インデックス オプションは、このオプションを指定しているクエリに関してのみ、max degree of parallelism 構成オプションをオーバーライドします。 次の表に、max degree of parallelism 構成オプションと MAXDOP インデックス オプションで指定できる有効な整数値を示します。  
  
    |値|Description|  
    |-----------|-----------------|  
    |0|現在のシステム ワークロードに応じて、使用する CPU 数をサーバーが決定するように指定します。 この値は既定値であり、推奨の設定です。|  
    |1|並列プラン生成を抑制します。 操作は順番に実行されます。|  
    |2～64|プロセッサ数が指定値まで制限されます。 現在のワークロードによっては、使用されるプロセッサ数が少なくなる場合があります。 使用できる CPU 数よりも大きな値を指定した場合は、実際に使用できる CPU 数が使用されます。|  
  
-   インデックスの並列実行と MAXDOP インデックス オプションは、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントに適用されます。  
  
    -   CREATE INDEX  
  
    -   ALTER INDEX REBUILD  
  
    -   DROP INDEX (このステートメントは、クラスター化インデックスのみに適用されます。)  
  
    -   ALTER TABLE ADD (インデックス) CONSTRAINT  
  
    -   ALTER TABLE DROP (クラスター化インデックス) CONSTRAINT  
  
-   ALTER INDEX REORGANIZE ステートメントには、MAXDOP インデックス オプションを指定できません。  
  
-   クエリ オプティマイザーが構築操作に 2 次以上の並列処理を適用すると、並べ替えを必要とするパーティション インデックス操作に必要なメモリ容量がさらに大きくなる場合があります。 並列処理の次数が高いと、必要なメモリ容量も大きくなります。 詳細については、「 [Partitioned Tables and Indexes](../partitions/partitioned-tables-and-indexes.md)」を参照してください。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 テーブルまたはビューに対する ALTER 権限が必要です。  
  
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
  
    ```  
    USE AdventureWorks2012;   
    GO  
    /*Alters the IX_ProductVendor_VendorID index on the Purchasing.ProductVendor table so that, if the server has eight or more processors, the Database Engine will limit the execution of the index operation to eight or fewer processors.  
    */  
    ALTER INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor  
    REBUILD WITH (MAXDOP=8);   
    GO  
    ```  
  
 詳細については、「[ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)」を参照してください。  
  
#### <a name="set-max-degree-of-parallelism-on-a-new-index"></a>新しいインデックスに並列処理の最大限度を設定する方法  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE INDEX IX_ProductVendor_NewVendorID   
    ON Purchasing.ProductVendor (BusinessEntityID)  
    WITH (MAXDOP=8);  
    GO  
    ```  
  
 詳細については、「[CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)」を参照してください。  
  
  
