---
title: ALTER RESOURCE GOVERNOR (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER RESOURCE GOVERNOR
- ALTER_RESOURCE_GOVERNOR_TSQL
- ALTER RESOURCE GOVERNOR RECONFIGURE
- ALTER_RESOURCE_GOVERNOR_RECONFIGURE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER RESOURCE GOVERNOR
- RECONFIGURE, ALTER RESOURCE GOVERNOR
ms.assetid: 442c54bf-a0a6-4108-ad20-db910ffa6e3c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2372b07e45e952003f18270995b52eb0f7338c64
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982021"
---
# <a name="alter-resource-governor-transact-sql"></a>ALTER RESOURCE GOVERNOR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  このステートメントは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で次のリソース ガバナー操作を実行するために使用します。  
  
-   CREATE|ALTER|DROP WORKLOAD GROUP、CREATE|ALTER|DROP RESOURCE POOL、または CREATE|ALTER|DROP EXTERNAL RESOURCE POOL ステートメントの実行時に指定した構成の変更の適用  
  
-   Resource Governor の有効化と無効化  
  
-   受信要求の分類の構成  
  
-   ワークロード グループ統計とリソース プール統計のリセット  
  
-   ディスク ボリュームごとの最大 I/O 操作数の設定  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
ALTER RESOURCE GOVERNOR   
      { DISABLE | RECONFIGURE }  
    | WITH ( CLASSIFIER_FUNCTION = { schema_name.function_name | NULL } )  
    | RESET STATISTICS  
    | WITH ( MAX_OUTSTANDING_IO_PER_VOLUME = value )   
[ ; ]  
```  
  
## <a name="arguments"></a>引数  
 DISABLE  
 Resource Governor を無効にします。 Resource Governor を無効にすると、結果は次のようになります。  
  
-   分類関数は実行されません。  
  
-   すべての新しい接続が、既定のグループに自動的に分類されます。  
  
-   システムによって開始される要求は、内部ワークロード グループに分類されます。  
  
-   ワークロード グループとリソース プールの既存の設定は、すべて既定値にリセットされます。 この場合、制限に達してもイベントは発生しません。  
  
-   通常のシステム監視は影響を受けません。  
  
-   構成は変更できますが、Resource Governor を有効にするまで変更は反映されません。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の再起動時に、リソース ガバナーはその構成を読み込みません。このとき、既定および内部のグループとプールのみが存在します。  
  
 RECONFIGURE  
 リソース ガバナーが有効でない場合、RECONFIGURE でリソース ガバナーを有効にします。 リソース ガバナーを有効にすると、結果は次のようになります。  
  
-   ワークロードがワークロード グループに割り当てられるように、新しい接続に対して分類関数が実行されます。  
  
-   リソース ガバナー構成で指定されているリソース制限が有効になり適用されます。  
  
-   リソース ガバナーを有効にする前に存在していた要求に、リソース ガバナーが無効であったときに加えた構成の変更が反映されます。  
  
 リソース ガバナーの実行中に、CREATE|ALTER|DROP WORKLOAD GROUP、CREATE|ALTER|DROP RESOURCE POOL、または CREATE|ALTER|DROP EXTERNAL RESOURCE POOL ステートメントの実行時に要求された構成の変更が適用されます。  
  
> [!IMPORTANT]  
>  構成の変更を有効にするには、ALTER RESOURCE GOVERNOR RECONFIGURE を発行する必要があります。  
  
 CLASSIFIER_FUNCTION = { _schema_name_ **.** _function_name_ | NULL }  
 *schema_name.function_name* で指定された分類関数を登録します。 この関数によってすべての新しいセッションが分類され、セッションの要求とクエリがワークロード グループに割り当てられます。 NULL を使用すると、新しいセッションは既定のワークロード グループに自動的に割り当てられます。  
  
 RESET STATISTICS  
 すべてのワークロード グループとリソース プールの統計をリセットします。 詳細については、「[sys.dm_resource_governor_workload_groups &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md)」と「[sys.dm_resource_governor_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)」を参照してください。  
  
 MAX_OUTSTANDING_IO_PER_VOLUME = *value*  
 **適用対象**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降。  
  
 キューに登録される I/O 操作のディスク ボリュームごとの最大数を設定します。 これらの I/O 操作では、任意のサイズの読み取りや書き込みを行うことができます。  MAX_OUTSTANDING_IO_PER_VOLUME の最大値は 100 です。 これはパーセントではありません。 この設定は、ディスク ボリュームの IO 特性に合わせて IO リソース管理をチューニングするために設計されています。 さまざまな値をテストし、ストレージ サブシステムの最大値を識別するために IOMeter、[DiskSpd](https://gallery.technet.microsoft.com/DiskSpd-a-robust-storage-6cd2f223)、SQLIO (非推奨) などの調整ツールの使用を検討することをお勧めします。 この設定では、システム レベルの安全性チェックが提供され、他のプールで MAX_IOPS_PER_VOLUME が無制限に設定されている場合でも、SQL Server でリソース プールの最小 IOPS を満たすことができます。 MAX_IOPS_PER_VOLUME の詳細については、「[CREATE RESOURCE POOL](../../t-sql/statements/create-resource-pool-transact-sql.md)」を参照してください。  
  
## <a name="remarks"></a>Remarks  
 ALTER RESOURCE GOVERNOR DISABLE、ALTER RESOURCE GOVERNOR RECONFIGURE、および ALTER RESOURCE GOVERNOR RESET STATISTICS は、ユーザー トランザクション内で使用できません。  
  
 RECONFIGURE パラメーターはリソース ガバナー構文の一部であり、個別の DDL ステートメントである [RECONFIGURE](../../t-sql/language-elements/reconfigure-transact-sql.md) とは異なります。  
  
 DDL ステートメントを実行する前に、リソース ガバナーの状態について詳しく理解しておくことをお勧めします。 詳細については、「[リソース ガバナー](../../relational-databases/resource-governor/resource-governor.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 CONTROL SERVER 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-starting-the-resource-governor"></a>A. Resource Governor を起動する  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の最初のインストール時には、リソース ガバナーは無効になっています。 Resource Governor を起動する例を次に示します。 このステートメントを実行した後、Resource Governor が実行され、定義済みのワークロード グループとリソース プールを使用できるようになります。  
  
```  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
```  
  
### <a name="b-assigning-new-sessions-to-the-default-group"></a>B. 新しいセッションを既定のグループに割り当てる  
 次の例では、Resource Governor 構成から既存の分類関数を削除することによって、すべての新しいセッションを既定のワークロード グループに割り当てます。 関数が分類関数として指定されていない場合、新しいセッションはすべて既定のワークロード グループに割り当てられます。 この変更は新しいセッションにのみ適用されます。 既存のセッションは影響を受けません。  
  
```  
ALTER RESOURCE GOVERNOR WITH (CLASSIFIER_FUNCTION = NULL);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
```  
  
### <a name="c-creating-and-registering-a-classifier-function"></a>C. 分類関数を作成して登録する  
 次の例では、`dbo.rgclassifier_v1` という名前の分類子関数を作成します。 この関数によって、ユーザー名またはアプリケーション名に基づいてすべての新しいセッションが分類され、セッションの要求とクエリが、指定されたワークロード グループに割り当てられます。 指定されたユーザー名またはアプリケーション名にマップされていないセッションは、既定のワークロード グループに割り当てられます。 次に分類関数が登録され、構成の変更が適用されます。  
  
```  
-- Store the classifier function in the master database.  
USE master;  
GO  
SET ANSI_NULLS ON;  
GO  
SET QUOTED_IDENTIFIER ON;  
GO  
CREATE FUNCTION dbo.rgclassifier_v1() RETURNS sysname   
WITH SCHEMABINDING  
AS  
BEGIN  
-- Declare the variable to hold the value returned in sysname.  
    DECLARE @grp_name AS sysname  
-- If the user login is 'sa', map the connection to the groupAdmin  
-- workload group.   
    IF (SUSER_NAME() = 'sa')  
        SET @grp_name = 'groupAdmin'  
-- Use application information to map the connection to the groupAdhoc  
-- workload group.  
    ELSE IF (APP_NAME() LIKE '%MANAGEMENT STUDIO%')  
        OR (APP_NAME() LIKE '%QUERY ANALYZER%')  
            SET @grp_name = 'groupAdhoc'  
-- If the application is for reporting, map the connection to  
-- the groupReports workload group.  
    ELSE IF (APP_NAME() LIKE '%REPORT SERVER%')  
        SET @grp_name = 'groupReports'  
-- If the connection does not map to any of the previous groups,  
-- put the connection into the default workload group.  
    ELSE  
        SET @grp_name = 'default'  
    RETURN @grp_name  
END;  
GO  
-- Register the classifier user-defined function and update the   
-- the in-memory configuration.  
ALTER RESOURCE GOVERNOR WITH (CLASSIFIER_FUNCTION=dbo.rgclassifier_v1);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
### <a name="d-resetting-statistics"></a>D. 統計をリセットする  
 次の例では、すべてのワークロード グループとリソース プールの統計をリセットします。  
  
```  
ALTER RESOURCE GOVERNOR RESET STATISTICS;  
```  
  
### <a name="e-setting-the-max_outstanding_io_per_volume-option"></a>E. MAX_OUTSTANDING_IO_PER_VOLUME オプションを設定する  
 次の例では、MAX_OUTSTANDING_IO_PER_VOLUME オプションが 20 に設定されます。  
  
```  
ALTER RESOURCE GOVERNOR  
WITH (MAX_OUTSTANDING_IO_PER_VOLUME = 20);   
```  
  
## <a name="see-also"></a>参照  
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)   
 [DROP EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-external-resource-pool-transact-sql.md)   
 [ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [リソース ガバナー](../../relational-databases/resource-governor/resource-governor.md)   
 [sys.dm_resource_governor_workload_groups &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md)   
 [sys.dm_resource_governor_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)  
  
  
