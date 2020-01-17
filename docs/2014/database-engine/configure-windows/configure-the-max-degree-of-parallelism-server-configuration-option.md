---
title: max degree of parallelism サーバー構成オプションの構成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- parallel queries [SQL Server]
- processors [SQL Server], parallel queries
- number of processors for parallel queries
- max degree of parallelism option
ms.assetid: 86b65bf1-a6a1-4670-afc0-cdfad1558032
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 46598cf66c80d07383fb033436bbe1792b1eec64
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62786945"
---
# <a name="configure-the-max-degree-of-parallelism-server-configuration-option"></a>max degree of parallelism サーバー構成オプションの構成
  このトピックでは、構成する方法を説明します、`max degree of parallelism`サーバー構成オプション[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]を使用して[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]または[!INCLUDE[tsql](../../includes/tsql-md.md)]します。 複数のマイクロプロセッサまたは CPU が搭載されているコンピューター上で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを実行するときは、並列処理の最適な程度、つまり各並列プラン実行で 1 つのステートメントを実行するために使用するプロセッサの数が検出されます。 `max degree of parallelism` オプションを使用すると、並列プラン実行で使用するプロセッサの数を制限できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クエリ、インデックス データ定義言語 (DDL) 操作、および静的およびキーセット ドリブン カーソルの作成用の並列実行プランを検討します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [推奨事項](#Recommendations)  
  
     [Security](#Security)  
  
-   **Max degree of parallelism 構成するオプションを使用します。**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **補足情報:** [Max degree of parallelism オプションを構成した後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   affinity mask オプションを既定値に設定していないと、対称型多重処理 (SMP) システムで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が使用できるプロセッサの数が制限されることがあります。  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   このオプションは詳細設定オプションであるため、熟練したデータベース管理者または認定された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技術者だけが変更するようにしてください。  
  
-   サーバーで並列処理の最大限度を特定できるようにするには、このオプションを 0 (既定値) に設定します。 並列処理の最大限度を 0 に設定すると、使用可能なすべてのプロセッサ (最大 64 プロセッサ) を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が使用できます。 並列プランの生成を中止するには、`max degree of parallelism` を 1 に設定します。 1 つのクエリ実行で使用できるプロセッサ コアの最大数を指定するには、値を 1 ～ 32,767 に設定します。 使用可能なプロセッサ数よりも多い値を指定すると、実際に使用可能なプロセッサ数が使用されます。 コンピューターにプロセッサが 1 つしか搭載されていない場合、`max degree of parallelism` の値は無視されます。  
  
-   クエリ ステートメントに MAXDOP クエリ ヒントを指定して、クエリの max degree of parallelism 値をオーバーライドできます。 詳細については、「[クエリ ヒント &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query)」を参照してください。  
  
-   インデックスを作成または再構築したり、クラスター化インデックスを削除するインデックス操作には、リソースを集中して使用するものがあります。 インデックス ステートメントの MAXDOP インデックス オプションを指定して、インデックス操作の max degree of parallelism 値をオーバーライドできます。 MAXDOP 値は実行時にステートメントに適用され、インデックス メタデータには保存されません。 詳細については、「 [並列インデックス操作の構成](../../relational-databases/indexes/configure-parallel-index-operations.md)」を参照してください。  
  
-   クエリおよびインデックスの操作だけでなく、このオプションも DBCC CHECKTABLE、DBCC CHECKDB、および DBCC CHECKFILEGROUP の並列処理を制御します。 トレース フラグ 2528 を使用して、これらのステートメントの並列実行プランを無効にすることができます。 詳細については、「[トレース フラグ &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql)」を参照してください。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 パラメーターなしで、または最初のパラメーターだけを指定して **sp_configure** を実行する権限は、既定ですべてのユーザーに付与されます。 両方のパラメーターを指定して **sp_configure** を実行し構成オプションを変更したり RECONFIGURE ステートメントを実行したりするには、ALTER SETTINGS サーバーレベル権限がユーザーに付与されている必要があります。 ALTER SETTINGS 権限は、 **sysadmin** 固定サーバー ロールと **serveradmin** 固定サーバー ロールでは暗黙のうちに付与されています。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-configure-the-max-degree-of-parallelism-option"></a>max degree of parallelism オプションを構成するには  
  
1.  **オブジェクト エクスプローラー**で、サーバーを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **[詳細設定]** ノードをクリックします。  
  
3.  **[並列処理の最大限度]** ボックスで、並列プランの実行で使用するプロセッサの最大数を指定します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-configure-the-max-degree-of-parallelism-option"></a>max degree of parallelism オプションを構成するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) を使用して、 `max degree of parallelism` オプションを `8`に設定する方法を示します。  
  
```sql  
USE AdventureWorks2012 ;  
GO   
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE WITH OVERRIDE;  
GO  
EXEC sp_configure 'max degree of parallelism', 8;  
GO  
RECONFIGURE WITH OVERRIDE;  
GO  
```  
  
 詳細については、「 [サーバー構成オプション &#40;SQL Server&#41;](server-configuration-options-sql-server.md)」を参照してください。  
  
##  <a name="FollowUp"></a>補足情報: max degree of parallelism オプションを構成した後  
 新しい設定は、サーバーを再起動しなくてもすぐに有効になります。  
  
## <a name="see-also"></a>参照  
 [affinity mask サーバー構成オプション](affinity-mask-server-configuration-option.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [サーバー構成オプション &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)   
 [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)   
 [DBCC CHECKTABLE &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checktable-transact-sql)   
 [DBCC CHECKDB &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)   
 [DBCC CHECKFILEGROUP &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkfilegroup-transact-sql)   
 [並列インデックス操作の構成](../../relational-databases/indexes/configure-parallel-index-operations.md)   
 [クエリ ヒント &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query)   
 [インデックス オプションの設定](../../relational-databases/indexes/set-index-options.md)  
  
  
