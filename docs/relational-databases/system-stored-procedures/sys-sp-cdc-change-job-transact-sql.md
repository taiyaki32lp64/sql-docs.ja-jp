---
title: sp_cdc_change_job (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_cdc_change_job_TSQL
- sys.sp_cdc_change_job
- sp_cdc_change_job_TSQL
- sp_cdc_change_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_change_job
ms.assetid: ea918888-0fc5-4cc1-b301-26b2a9fbb20d
author: rothja
ms.author: jroth
ms.openlocfilehash: 0c2c39363ca1b0824b27645df8c8501931b674a2
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056764"
---
# <a name="syssp_cdc_change_job-transact-sql"></a>sp_cdc_change_job (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  現在のデータベースの変更データキャプチャのクリーンアップジョブまたはキャプチャジョブの構成を変更します。 ジョブの現在の構成を表示するには、 [cdc_jobs](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)テーブルに対してクエリを実行するか、 [sp_cdc_help_jobs](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md)を使用します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.sp_cdc_change_job [ [ @job_type = ] 'job_type' ]  
    [ , [ @maxtrans = ] max_trans ]   
    [ , [ @maxscans = ] max_scans ]   
    [ , [ @continuous = ] continuous ]   
    [ , [ @pollinginterval = ] polling_interval ]   
    [ , [ @retention ] = retention ]   
    [ @threshold = ] 'delete threshold'  
```  
  
## <a name="arguments"></a>引数  
変更するジョブの種類 `[ @job_type = ] 'job_type'` ます。 *job_type*は**nvarchar (20)** で、既定値は ' capture ' です。 有効な入力は ' capture ' と ' cleanup ' です。  
  
各スキャンサイクルで処理するトランザクションの最大数 `[ @maxtrans ] = max_trans_` します。 *max_trans*は**int**で、既定値は NULL です。これは、このパラメーターに変更がないことを示します。 指定する場合、値は正の整数である必要があります。  
  
 *max_trans*は、キャプチャジョブに対してのみ有効です。  
  
ログからすべての行を抽出するために実行するスキャンサイクルの最大数 `[ @maxscans ] = max_scans_` ます。 *max_scans*は**int**で、既定値は NULL です。これは、このパラメーターに変更がないことを示します。  
  
 *max_scan*は、キャプチャジョブに対してのみ有効です。  
  
`[ @continuous ] = continuous_` は、キャプチャジョブを連続的に実行するか (1)、1回だけ実行するか (0) を示します。 *continuous*は**bit**で、既定値は NULL です。これは、このパラメーターに変更がないことを示します。  
  
 *Continuous* = 1 の場合、 [sp_cdc_scan](../../relational-databases/system-stored-procedures/sys-sp-cdc-scan-transact-sql.md)ジョブによってログがスキャンされ、最大 (*max_trans* \* *max_scans*) トランザクションが処理されます。 次に、 *polling_interval*で指定された秒数だけ待機してから、次のログスキャンを開始します。  
  
 *Continuous* = 0 の場合、 **sp_cdc_scan**ジョブはログの*max_scans*スキャンまで実行され、各スキャン中に*max_trans*トランザクションまで処理された後、終了します。  
  
 **\@continuous**が1から0に変更された場合、 **\@pollinginterval**は自動的に0に設定されます。 0以外の **\@pollinginterval**に指定された値は無視されます。  
  
 **\@continuous**を省略した場合、または明示的に NULL に設定し、 **\@pollinginterval**が明示的に0よりも大きい値に設定されている場合、 **\@continuous**は自動的に1に設定されます。  
  
 *continuous*は、キャプチャジョブに対してのみ有効です。  
  
ログスキャンサイクルの間隔を秒単位で `[ @pollinginterval ] = polling_interval_` します。 *polling_interval*は**bigint**で、既定値は NULL です。これは、このパラメーターに変更がないことを示します。  
  
 *polling_interval*は、 *continuous*が1に設定されている場合にのみ、キャプチャジョブに対して有効です。  
  
変更行が変更テーブルに保持される `[ @retention ] = retention_` 時間 (分単位)。 *retention*は**bigint**であり、既定値は NULL です。これは、このパラメーターに変更がないことを示します。 最大値は 52494800 (100 年) です。 指定する場合、値は正の整数である必要があります。  
  
 *retention*はクリーンアップ ジョブでのみ有効です。  
  
クリーンアップ時に1つのステートメントを使用して削除できる削除エントリの最大数 `[ @threshold = ] 'delete threshold'` ます。 *delete threshold*は**bigint**であり、既定値は NULL です。これは、このパラメーターに変更がないことを示します。 *削除のしきい値*は、クリーンアップジョブに対してのみ有効です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 [InclusionThresholdSetting]  
  
## <a name="remarks"></a>Remarks  
 パラメーターを省略した場合、 [cdc_jobs](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)テーブルの関連付けられた値は更新されません。 明示的に NULL に設定されたパラメーターは、パラメーターが省略されているかのように扱われます。  
  
 ジョブの種類に対して無効なパラメーターを指定すると、ステートメントは失敗します。  
  
 ジョブに対する変更は、 [sp_cdc_stop_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-stop-job-transact-sql.md)を使用してジョブを停止し、 [sp_cdc_start_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-start-job-transact-sql.md)を使用して再起動するまで有効になりません。  
  
## <a name="permissions"></a>アクセス許可  
 **Db_owner**固定データベースロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-changing-a-capture-job"></a>A. キャプチャ ジョブを変更する  
 次の例では、`AdventureWorks2012` データベースのキャプチャジョブの `@job_type`、`@maxscans`、および `@maxtrans` パラメーターを更新します。 キャプチャジョブのその他の有効なパラメーターである `@continuous` と `@pollinginterval`は省略されます。これらの値は変更されません。  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_change_job   
    @job_type = N'capture',  
    @maxscans = 1000,  
    @maxtrans = 15;  
GO  
```  
  
### <a name="b-changing-a-cleanup-job"></a>b. クリーンアップジョブの変更  
 次の例では、`AdventureWorks2012` データベースのクリーンアップジョブを更新します。 このジョブの種類のすべての有効なパラメーター ( **\@threshold**を除く) が指定されています。 **\@threshold**の値は変更されません。  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_change_job   
    @job_type = N'cleanup',  
    @retention = 2880;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [dbo. cdc_jobs &#40;transact-sql&#41; ](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sp_cdc_enable_table &#40;transact-sql&#41; ](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [sys.sp_cdc_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)  
  
  
