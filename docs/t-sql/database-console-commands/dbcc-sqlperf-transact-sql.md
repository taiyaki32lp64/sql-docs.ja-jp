---
title: DBCC SQLPERF (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SQLPERF
- DBCC_SQLPERF_TSQL
- SQLPERF_TSQL
- DBCC SQLPERF
dev_langs:
- TSQL
helpviewer_keywords:
- statistical information [SQL Server], transaction logs
- transaction logs [SQL Server], space usage
- space [SQL Server], transaction logs
- DBCC SQLPERF statement
ms.assetid: ec9225ce-e20f-4b03-8b3a-7bcad8a649df
author: pmasl
ms.author: umajay
ms.openlocfilehash: 8cb409823bad1370c38b6dc99f04c7e49d58796a
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982406"
---
# <a name="dbcc-sqlperf-transact-sql"></a>DBCC SQLPERF (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

すべてのデータベースを対象として、トランザクション ログ領域の使用状況に関する統計情報を提供します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、待機統計情報とラッチ統計情報のリセットにも使用できます。
  
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降)、[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ([一部の地域ではプレビュー版](https://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag))
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```
DBCC SQLPERF   
(  
     [ LOGSPACE ]  
     | [ "sys.dm_os_latch_stats" , CLEAR ]  
     | [ "sys.dm_os_wait_stats" , CLEAR ]  
)   
     [WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>引数  
LOGSPACE  
データベースごとに、トランザクション ログの現在のサイズと使用されているログ領域の割合を返します。 この情報を利用して、トランザクション ログで使用されている領域の量を監視します。

> [!IMPORTANT]
> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降のトランザクション ログの容量利用情報については、このトピックの「[注釈](#Remarks)」セクションを参照してください。
  
**"sys.dm_os_latch_stats"** , CLEAR  
ラッチ統計をリセットします。 詳細については、「[sys.dm_os_latch_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)」を参照してください。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]では、このオプションは使用できません。  
  
**"sys.dm_os_wait_stats"** , CLEAR  
待機統計をリセットします。 詳細については、「[sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)」を参照してください。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]では、このオプションは使用できません。  
  
WITH NO_INFOMSGS  
重大度レベル 0 から 10 のすべての情報メッセージを表示しないようにします。  
  
## <a name="result-sets"></a>結果セット  
 次の表では、結果セットの列について説明します。  
  
|列名|定義|  
|---|---|
|**Database Name**|ログ統計情報を表示するデータベースの名前。|  
|**ログ サイズ (MB)**|ログに割り当てられている現在のサイズ。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]では内部ヘッダー情報の格納用に少量のディスク容量が確保されるので、この値は最初にログ領域に割り当てられた容量よりも常に小さくなります。|  
|**ログの使用済み領域 (%)**|現在トランザクション ログ情報の保存に使用されているログ ファイルのパーセンテージ。|  
|**ステータス**|ログ ファイルの状態。 常に 0 です。|  
  
## <a name="Remarks"></a> 解説  
[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降、データベース別のトランザクション ログの容量利用情報を返すには、`DBCC SQLPERF(LOGSPACE)` の代わりに [sys.dm_db_log_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md) DMV を使用します。    
 
トランザクション ログには、データベースで実行された各トランザクションが記録されます。 詳細については、「[トランザクション ログ &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)」と「[SQL Server トランザクション ログのアーキテクチャと管理ガイド](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)」を参照してください。
  
## <a name="permissions"></a>アクセス許可  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で `DBCC SQLPERF(LOGSPACE)` を実行するには、サーバーに対する `VIEW SERVER STATE` 権限が必要です。 待機統計情報とラッチ統計情報をリセットするには、サーバーに対する `ALTER SERVER STATE` 権限が必要です。
  
[!INCLUDE[ssSDS](../../includes/sssds-md.md)] の Premium 階層および Business Critical 階層では、データベースで `VIEW DATABASE STATE` アクセス許可が必要です。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Standard、Basic、および General Purpose 階層の場合、[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 管理者アカウントが必要です。 待機およびラッチ統計をリセットすることはできません。
  
## <a name="examples"></a>使用例  
  
### <a name="a-displaying-log-space-information-for-all-databases"></a>A. すべてのデータベースのログ領域情報を表示する  
次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに含まれているすべてのデータベースの `LOGSPACE` 情報を表示します。
  
```sql  
DBCC SQLPERF(LOGSPACE);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Database Name Log Size (MB) Log Space Used (%) Status        
------------- ------------- ------------------ -----------   
master         3.99219      14.3469            0   
tempdb         1.99219      1.64216            0   
model          1.0          12.7953            0   
msdb           3.99219      17.0132            0   
AdventureWorks 19.554688    17.748701          0  
```  
  
### <a name="b-resetting-wait-statistics"></a>B. 待機統計をリセットする  
次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの待機統計をリセットします。
  
```sql  
DBCC SQLPERF("sys.dm_os_wait_stats",CLEAR);  
```  
  
## <a name="see-also"></a>参照  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)   
[sys.dm_os_latch_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)    
[sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)     
[sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)    
[sys.dm_db_log_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)    
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)     
[sys.dm_db_log_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md)     

