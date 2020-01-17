---
title: sp_attach_single_file_db (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_attach_single_file_db
- sp_attach_single_file_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_attach_single_file_db
ms.assetid: 13bd1044-9497-4293-8390-1f12e6b8e952
author: stevestein
ms.author: sstein
ms.openlocfilehash: b285b5032c1ccde03ef8bd3f287d6b7f60eb0ffc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046170"
---
# <a name="spattachsinglefiledb-transact-sql"></a>sp_attach_single_file_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  データ ファイルが 1 つだけ格納されているデータベースを現在のサーバーにアタッチします。 **sp_attach_single_file_db**複数のデータ ファイルでは使用できません。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] CREATE DATABASE を使用することをお勧めします。 *database_name* FOR ATTACH 代わりにします。 詳細については、「[CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)」を参照してください。 レプリケートされたデータベースには、このプロシージャを使用しないでください。  
  
> [!IMPORTANT]  
>  不明なソースや信頼されていないソースからデータベースをアタッチまたは復元しないことをお勧めします。 こうしたデータベースには、意図しない [!INCLUDE[tsql](../../includes/tsql-md.md)] コードを実行したり、スキーマまたは物理データベース構造を変更してエラーを発生させるような、悪意のあるコードが含まれている可能性があります。 不明または信頼できないソースのデータベースを使用する前に、運用サーバー以外のサーバーでそのデータベースに対し [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) を実行し、さらに、そのデータベースのストアド プロシージャやその他のユーザー定義コードなどのコードを調べます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_attach_single_file_db [ @dbname= ] 'dbname'  
    , [ @physname= ] 'physical_name'  
```  
  
## <a name="arguments"></a>引数  
`[ @dbname = ] 'dbname'` サーバーに接続するデータベースの名前です。 名前は一意である必要があります。 *dbname*は**sysname**、既定値は NULL です。  
  
`[ @physname = ] 'physical_name'` データベース ファイルのパスを含む、物理名です。 *physical_name*は**nvarchar (260)** 、既定値は NULL です。  
  
> [!NOTE]  
>  この引数は、CREATE DATABASE ステートメントの FILENAME パラメーターにマップされます。 詳細については、「[CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)」を参照してください。  
  
 フルテキスト カタログ ファイルを含む [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] データベースを [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] サーバー インスタンスにアタッチする場合、カタログ ファイルは [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]と同様に他のデータベース ファイルと一緒に以前の場所からアタッチされます。 詳細については、「 [フルテキスト検索のアップグレード](../../relational-databases/search/upgrade-full-text-search.md)」を参照してください。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>コメント  
 使用**sp_attach_single_file_db**を明示的に使用して、サーバーからデタッチされたデータベースに対してのみ**sp_detach_db**オペレーション データベース、またはコピーします。  
  
 **sp_attach_single_file_db**は単一のログ ファイルのあるデータベースに対してのみ機能します。 ときに**sp_attach_single_file_db**データベースをアタッチ、サーバーに新しいログ ファイルを作成します。 データベースが読み取り専用の場合、ログ ファイルは、アタッチされる前の場所に作成されます。  
  
> [!NOTE]  
>  データベース スナップショットのデタッチおよびアタッチは行うことができません。  
  
 レプリケートされたデータベースには、このプロシージャを使用しないでください。  
  
## <a name="permissions"></a>アクセス許可  
 データベースをアタッチするときにアクセス許可を処理する方法については、次を参照してください。 [CREATE DATABASE &#40;SQL Server TRANSACT-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)します。  
  
## <a name="examples"></a>使用例  
 次の例では、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] をデタッチした後、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] から現在のサーバーに 1 つのファイルをアタッチします。  
  
```  
USE master;  
GO  
EXEC sp_detach_db @dbname = 'AdventureWorks2012';  
EXEC sp_attach_single_file_db @dbname = 'AdventureWorks2012',   
    @physname =   
N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\AdventureWorks2012_Data.mdf';  
```  
  
## <a name="see-also"></a>参照  
 [データベースのデタッチとアタッチ &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [sp_detach_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)   
 [sp_helpfile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
