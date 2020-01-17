---
title: sp_rda_reauthorize_db (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sp_rda_reauthorize_db
- sp_rda_reauthorize_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reauthorize_db stored procedure
ms.assetid: f6f3e4b2-8c72-4d23-a5de-fe671ca5c5cd
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 01809f0d4eb494d58f035d23846025578aada7c7
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2019
ms.locfileid: "72251262"
---
# <a name="syssp_rda_reauthorize_db-transact-sql"></a>sp_rda_reauthorize_db (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Stretch が有効なローカルデータベースとリモートデータベースとの間の認証された接続を復元します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_rda_reauthorize_db @credential = @credential, @with_copy = @with_copy [ , @azure_servername = @azure_servername, @azure_databasename = @azure_databasename ]  
```  
  
## <a name="arguments"></a>引数  
 @credential = *\@資格情報*  
 ローカル Stretch 対応データベースに関連付けられたデータベーススコープ資格情報を指定します。  
  
 @with_copy = *\@with_copy*  
 リモートデータのコピーを作成してコピーに接続するかどうかを指定します (推奨)。 *\@with_copy*はビットです。  
  
 @azure_servername = *\@azure_servername*  
 リモートデータを含む Azure サーバーの名前を指定します。 *\@azure_servername*は sysname です。  
  
 @azure_databasename = *\@azure_databasename*  
 リモートデータが格納されている Azure データベースの名前を指定します。 *\@azure_databasename*は sysname です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または > 0 (失敗)  
  
## <a name="permissions"></a>アクセス許可  
 Db_owner アクセス許可が必要です。  
  
## <a name="remarks"></a>Remarks  
 [Sp_rda_reauthorize_db (transact-sql)](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)を実行してリモートの Azure データベースに再接続すると、この操作によってクエリモードが自動的に LOCAL_AND_REMOTE にリセットされます。これは Stretch Database の既定の動作です。 つまり、クエリはローカルとリモートの両方のデータから結果を返します。  
  
## <a name="example"></a>例  
 次の例では、Stretch が有効なローカルデータベースとリモートデータベースとの間の認証された接続を復元します。 リモートデータのコピーを作成し (推奨)、新しいコピーに接続します。  
  
```sql  
DECLARE @credentialName nvarchar(128);   
SET @credentialName = N'<existing_database_scoped_credential_name>';   
EXEC sp_rda_reauthorize_db @credential = @credentialName, @with_copy = 1;  
  
```  
  
## <a name="see-also"></a>参照  
 [sp_rda_deauthorize_db &#40;transact-sql&#41; ](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
