---
title: catalog.cleanup_server_execution_keys | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a79f1006-54e8-4cbf-96f8-5ed143ebb830
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 62cbd5141dfb6254415657dc3ef03d1402b0f3b4
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71281369"
---
# <a name="catalogcleanup_server_execution_keys"></a>catalog.cleanup_server_execution_keys 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  SSISDB データベースから証明書と対称キーを削除します。  
  
## <a name="syntax"></a>構文  
  
```sql
catalog.cleanup_server_execution_keys [ @cleanup_flag = ] cleanup_flag ,  
[ @delete_batch_size = ] delete_batch_size  
```  
  
## <a name="arguments"></a>引数  
 [ @cleanup_flag = ] *cleanup_flag*  
 実行レベル (1) 証明書またはプロジェクト レベル (2) 証明書と対称キーが削除されるかどうかを示します。  
  
 実行レベル (1) は、SERVER_OPERATION_ENCRYPTION_LEVEL が PER_EXECUTION (1) に設定されている場合にのみ使用します。  
  
 プロジェクト レベル (2) SERVER_OPERATION_ENCRYPTION_LEVEL が PER_PROJECT (2) に設定されている場合にのみ使用します。 削除されたプロジェクトと、操作ログが消去されているプロジェクトに対してのみ証明書と対称キーが削除されます。  
  
 [ @delete_batch_size = ] *delete_batch_size*  
 削除するキーと証明書の数。 既定値は 1000 です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 成功の場合は 0、失敗の場合は 1 です。  
  
## <a name="result-sets"></a>結果セット  
 [なし] :  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャには、次の権限のいずれかが必要です。  
  
-   プロジェクトの READ および EXECUTE アクセス許可と、該当する場合は、参照先の環境での READ アクセス許可。  
  
-   **ssis_admin** データベース ロールのメンバーシップ。  
  
-   **sysadmin** サーバー ロールのメンバーシップ。  
  
## <a name="errors-and-warnings"></a>エラーおよび警告  
 このストアド プロシージャは、次のシナリオでエラーが発生します。  
  
-   SSISDB データベースに 1 つ以上のアクティブな操作がある。  
  
-   SSISDB データベースがシングル ユーザー モードではない。  
  
## <a name="remarks"></a>Remarks  
 SQL Server 2012 Service Pack 2 により、SERVER_OPERATION_ENCRYPTION_LEVEL プロパティが **internal.catalog_properties** テーブルに追加されました。 このプロパティには、次の 2 つの有効値があります。  
  
-   **PER_EXECUTION (1)** : 機密性の高い実行パラメーターと実行ログを保護する証明書と対称キーが実行するたびに作成されます。 これが既定値です。 実行ごとに証明書/キーが生成されるため、運用環境でパフォーマンスの問題 (デッドロック、メンテナンス ジョブの失敗など) が発生する可能性があります。 ただしこの設定は、その他の値 (2) よりも高いレベルのセキュリティを提供します。  
  
-   **PER_PROJECT (2)** : 実行のたびに証明書と対称キーが作成されます。これらは機密性の高いパラメーターを保護するために使用されます。 これは、キーと証明書が実行ごとではなく、プロジェクトに対して 1 回生成されるため、PER_EXECUTION レベルより優れたパフォーマンスを提供します。  
  
 SERVER_OPERATION_ENCRYPTION_LEVEL を 1 から 2 (または) 2 から 1 に変更するには、事前に [catalog.cleanup_server_log](../../integration-services/system-stored-procedures/catalog-cleanup-server-log.md) ストアド プロシージャを実行する必要があります。 このストアド プロシージャを実行する前に、次の操作を行う必要があります。  
  
1.  [catalog.catalog_properties &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md) テーブルで OPERATION_CLEANUP_ENABLED プロパティの値が TRUE に設定されていることを確認します。  
  
2.  Integration Services データベース (SSISDB) をシングル ユーザー モードに設定します。 SQL Server Management Studio で SSISDB の [データベース プロパティ] ダイアログ ボックスを開き、[オプション] タブに切り替え、[アクセスの制限] プロパティをシングル ユーザー モード (SINGLE_USER) に設定します。 cleanup_server_log ストアド プロシージャを実行すると、プロパティ値が元の値に設定されます。  
  
3.  ストアド プロシージャ [catalog.cleanup_server_log](../../integration-services/system-stored-procedures/catalog-cleanup-server-log.md) を実行します。  
  
4.  次に、[catalog.catalog_properties &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md) テーブルで SERVER_OPERATION_ENCRYPTION_LEVEL プロパティの値を変更します。  
  
5.  ストアド プロシージャ [catalog.cleanup_server_execution_keys](../../integration-services/system-stored-procedures/catalog-cleanup-server-execution-keys.md) を実行し、SSISDB データベースから証明書とキーをクリーンアップします。 SSISDB データベースからの証明書とキーの削除は、長時間かかる場合があるため、オフピークの時間帯に定期的に実行する必要があります。  
  
     スコープまたはレベル (実行とプロジェクトの比較) および削除するキーの数を指定できます。 既定のバッチ サイズは 1000 です。 レベルを 2 に設定すると、関連するプロジェクトが削除されている場合にのみ、キーと証明書が削除されます。  
  
 詳細については、次のサポート技術情報の記事をご覧ください。 [修正: SQL Server 2012 で、SSISDB を展開ストアとして使用すると、パフォーマンスの問題が発生する](https://support.microsoft.com/kb/2972285)  
  
## <a name="example"></a>例  
 次の例では、cleanup_server_execution_keys ストアド プロシージャを呼び出します。  
  
```sql  
USE [SSISDB]  
GO  
  
DECLARE@return_value int  
  
EXEC@return_value = [internal].[cleanup_server_execution_keys]  
@cleanup_flag = 1,  
@delete_batch_size = 500  
  
SELECT'Return Value' = @return_value  
  
GO  
```  
  
  
