---
title: managed_backup fn_get_health_status (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_get_health_status_TSQL
- smart_admin.fn_get_health_status_TSQL
- smart_admin.fn_get_health_status
- fn_get_health_status
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.fn_get_health_status
- fn_get_health_status
ms.assetid: b376711d-444a-4b5e-b483-8df323b4e31f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: bc2bfdbd8714bf4211373e921c1b054ed224feb3
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155813"
---
# <a name="managed_backupfn_get_health_status-transact-sql"></a>managed_backup fn_get_health_status (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  指定した期間内に拡張イベントによって報告されたエラーの集計数を示す0行のテーブルを返します。  
  
 関数は、Smart Admin でサービスの正常性状態を報告するために使用されます。現在[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 、Smart Admin の包括的な環境でサポートされています。 したがって、返されるエラーは[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]に関連しています。  
  
 
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
managed_backup.fn_get_health_status([@begin_time = ] 'time_1' , [ @end_time = ] 'time_2')  
```  
  
##  <a name="Arguments"></a> 引数  
 [@begin_time]  
 エラーの集計数を計算する期間の開始時刻。  @begin_timeパラメーターは DATETIME です。 既定値は NULL です。 値が NULL の場合、この関数は現在の時刻の 30 分前に報告されたイベントから処理します。  
  
 [ @end_time]  
 エラーの集計数を計算する期間の終了時刻。 パラメーター @end_timeは DATETIME で、既定値は NULL です。 値が NULL の場合、関数は現在の時刻まで拡張イベントを処理します。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|number_of_storage_connectivity_errors|int|プログラムが Azure ストレージアカウントに接続するときの接続エラーの数。|  
|number_of_sql_errors|int|プログラムが SQL Server エンジンに接続したときに返されたエラーの数。|  
|number_of_invalid_credential_errors|int|プログラムが SQL 資格情報を使用して認証しようとしたときに返されたエラーの数。|  
|number_of_other_errors|int|接続、SQL、資格情報以外のカテゴリに関するエラーの数。|  
|number_of_corrupted_or_deleted_backups|int|削除または破損したバックアップファイルの数。|  
|number_of_backup_loops|int|で[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]構成されたすべてのデータベースをバックアップエージェントがスキャンする回数。|  
|number_of_retention_loops|int|保有期間を評価するためにデータベースがスキャンされた回数。|  
  
## <a name="best-practices"></a>ベスト プラクティス  
 このような集計されたカウントは、システム正常性の監視に使用できます。 たとえば、number_ of_retention_loops 列が30分間0の場合、リテンション期間の管理に時間がかかったり、正常に機能しなくなったりする可能性があります。 0以外のエラー列は問題を示している可能性があり、拡張イベントログをチェックして問題の詳細を確認する必要があります。 または、ストアドプロシージャ**managed_backup**を使用して、拡張イベントの一覧を取得し、エラーの詳細を確認します。  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 関数に対する**SELECT**権限が必要です。  
  
## <a name="examples"></a>使用例  
  
-   次の例では、関数を実行した時点の 30 分前から集計されたエラー数が返されます。  
  
    ```  
    SELECT *  
    FROM managed_backup.fn_get_health_status(NULL, NULL)  
  
    ```  
  
-   次の例では、現在の週の集計されたエラー数を返します。  
  
    ```  
    Use msdb  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
    SELECT *  
    FROM managed_backup.fn_get_health_status(@startofweek, @endofweek)  
  
    ```  
  
  
