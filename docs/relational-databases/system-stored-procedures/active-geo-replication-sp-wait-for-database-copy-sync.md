---
title: sp_wait_for_database_copy_sync
titleSuffix: Azure SQL Database
ms.date: 03/03/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sp_wait_for_database_copy_sync_TSQL
- sp_wait_for_database_copy_sync
dev_langs:
- TSQL
helpviewer_keywords:
- sp_wait_for_database_copy_sync
ms.assetid: 7068da7f-cb74-47f2-b064-eb076a0d3885
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.custom: seo-dt-2019
ms.openlocfilehash: eb274d4f022a182ac056c190a8626fa48e36511d
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73844403"
---
# <a name="active-geo-replication---sp_wait_for_database_copy_sync"></a>アクティブ Geo レプリケーション-sp_wait_for_database_copy_sync
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  このプロシージャは、プライマリとセカンダリの間の[!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)] リレーションシップを対象としています。 **Sp_wait_for_database_copy_sync**を呼び出すと、コミットされたすべてのトランザクションがアクティブなセカンダリデータベースによってレプリケートおよび確認されるまで、アプリケーションは待機します。 プライマリデータベースのみで**sp_wait_for_database_copy_sync**を実行します。  
  
||  
|-|  
|**Applies to**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
  
## <a name="syntax"></a>構文  
  
```  
sp_wait_for_database_copy_sync [ @target_server = ] 'server_name'   
     , [ @target_database = ] 'database_name'  
```  
  
## <a name="arguments"></a>引数  
 [@target_server =]' server_name '  
 アクティブなセカンダリ データベースをホストする SQL データベース サーバーの名前。 server_name は sysname であり、既定値はありません。  
  
 [ @target_database = ] 'database_name'  
 アクティブなセカンダリデータベースの名前。 database_name は sysname であり、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 成功した場合は 0 を、失敗した場合はエラー番号を返します。  
  
 最も可能性の高いエラー条件は次のとおりです。  
  
-   サーバー名またはデータベース名がない。  
  
-   指定されたサーバー名またはデータベースに対するリンクが見つからない。  
  
-   インターリンク接続が切断されました。 接続のタイムアウト後に**sp_wait_for_database_copy_sync**が返されます。  
  
## <a name="permissions"></a>アクセス許可  
 プライマリ データベース内のすべてのユーザーが、このシステム ストアド プロシージャを呼び出すことができます。 ログインは、プライマリデータベースとアクティブセカンダリデータベースの両方のユーザーである必要があります。  
  
## <a name="remarks"></a>Remarks  
 **Sp_wait_for_database_copy_sync**呼び出しの前にコミットされたすべてのトランザクションが、アクティブなセカンダリデータベースに送信されます。  
  
## <a name="examples"></a>使用例  
 次の例では、 **sp_wait_for_database_copy_sync**を呼び出して、すべてのトランザクションがプライマリデータベース db0 にコミットされていることを確認します。これは、ターゲットサーバー ubfyu5ssyt 上のアクティブなセカンダリデータベースに送信されます。  
  
```  
USE db0;  
GO  
EXEC sys.sp_wait_for_database_copy_sync @target_server = N'ubfyu5ssyt1', @target_database = N'db0';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [dm_continuous_copy_status &#40;Azure SQL Database&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-continuous-copy-status-azure-sql-database.md)   
 [Geo レプリケーションの動的管理ビューおよび関数&#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/geo-replication-dynamic-management-views-and-functions-azure-sql-database.md)  
  
  
