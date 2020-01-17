---
title: sp_detach_db (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 09/30/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_detach_db
- sp_detach_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_detach_db
- detaching databases [SQL Server]
ms.assetid: abcb1407-ff78-4c76-b02e-509c86574462
author: stevestein
ms.author: sstein
ms.openlocfilehash: ec7758ad2f9443ad29f0da799e3f286612f95cab
ms.sourcegitcommit: 710d60e7974e2c4c52aebe36fceb6e2bbd52727c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/11/2019
ms.locfileid: "72278183"
---
# <a name="sp_detach_db-transact-sql"></a>sp_detach_db (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  サーバー インスタンスから現在使用されていないデータベースを切り離します。必要に応じて、切り離す前に、すべてのテーブルに対して UPDATE STATISTICS を実行します。  
  
> [!IMPORTANT]  
>  レプリケートしたデータベースをデタッチする場合、パブリッシュを解除する必要があります。 詳細については、このトピックで後述する「解説」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_detach_db [ @dbname= ] 'database_name'   
    [ , [ @skipchecks= ] 'skipchecks' ]   
    [ , [ @keepfulltextindexfile = ] 'KeepFulltextIndexFile' ]   
```  
  
## <a name="arguments"></a>引数  
`[ @dbname = ] 'database_name'` デタッチするデータベースの名前を指定します。 *database_name*は**sysname**値で、既定値は NULL です。  
  
`[ @skipchecks = ] 'skipchecks'` 更新プログラムの統計をスキップするか実行するかを指定します。 *skipchecks*は**nvarchar (10)** 値で、既定値は NULL です。 統計の更新をスキップするには、 **true**を指定します。 UPDATE STATISTICS を明示的に実行するには、 **false**を指定します。  
  
 既定では、UPDATE STATISTICS は、テーブルとインデックスのデータに関する情報を更新するために実行されます。 UPDATE STATISTICS の実行は、データベースを読み取り専用メディアに移動する場合に使用すると便利です。  
  
`[ @keepfulltextindexfile = ] 'KeepFulltextIndexFile'` は、デタッチされているデータベースに関連付けられているフルテキストインデックスファイルが、データベースのデタッチ操作中に削除されないように指定します。 *KeepFulltextIndexFile*は**nvarchar (10)** 値、既定値は**true**です。 *KeepFulltextIndexFile*が**false**の場合、データベースに関連付けられているすべてのフルテキストインデックスファイルとフルテキストインデックスのメタデータは、データベースが読み取り専用でない限り削除されます。 NULL または**true**の場合、フルテキスト関連のメタデータが保持されます。  
  
> [!IMPORTANT]
>  **\@keepfulltextindexfile**パラメーターは、今後のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では削除される予定です。 新しい開発作業ではこのパラメーターを使用しないようにし、現在このパラメーターを使用しているアプリケーションはできるだけ早く変更してください。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 [InclusionThresholdSetting]  
  
## <a name="remarks"></a>Remarks  
 データベースをデタッチすると、そのすべてのメタデータが削除されます。 データベースが任意のログインアカウントの既定のデータベースであった場合、 **master**が既定のデータベースになります。  
  
> [!NOTE]  
>  すべてのログインアカウントの既定のデータベースを表示する方法の詳細については、「 [transact-sql &#40;&#41;の sp_helplogins](../../relational-databases/system-stored-procedures/sp-helplogins-transact-sql.md)」を参照してください。 必要なアクセス許可がある場合は、 [ALTER login](../../t-sql/statements/alter-login-transact-sql.md)を使用して、新しい既定のデータベースをログインに割り当てることができます。  
  
## <a name="restrictions"></a>制限  
 次のいずれかに該当する場合、データベースをデタッチすることはできません。  
  
-   データベースは現在使用されています。 詳細については、このトピックで後述する「排他アクセスの取得」を参照してください。  
  
-   レプリケートされると、データベースがパブリッシュされます。  
  
     データベースをデタッチする前に、 [sp_replicationdboption](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)を実行してパブリッシングを無効にする必要があります。  
  
    > [!NOTE]  
    >  **sp_replicationdboption**を使用できない場合、 [sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)を実行してレプリケーションを削除できます。  
  
-   データベースに、データベース スナップショットが存在する。  
  
     データベースをデタッチするには、すべてのデータベース スナップショットを削除する必要があります。 詳細については、「 [データベース スナップショットの削除 &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)」を参照してください。  
  
    > [!NOTE]  
    >  データベース スナップショットのデタッチおよびアタッチは行うことができません。  
  
-   データベースがミラー化されている。  
  
     データベースミラーリングセッションが終了するまで、データベースをデタッチすることはできません。 詳細については、「[データベース ミラーリングを削除する &#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md)」を参照してください。  
  
-   データベースに問題がある。  
  
     データベースをデタッチする前に、問題のあるデータベースを緊急モードに設定する必要があります。 データベースを緊急モードに設定する方法の詳細については、「 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)」を参照してください。  
  
-   データベースがシステム データベースである。  
  
## <a name="obtaining-exclusive-access"></a>排他アクセスの取得  
 データベースをデタッチするには、データベースへの排他アクセスが必要です。 デタッチするデータベースが使用中の場合は、デタッチする前に、データベースを SINGLE_USER モードに設定して、排他アクセスを取得します。

 データベースを SINGLE_USER に設定する前に、AUTO_UPDATE_STATISTICS_ASYNC オプションが OFF に設定されていることを確認します。 このオプションが ON に設定されていると、統計の更新に使用されるバックグラウンド スレッドによってデータベースへの接続が使用されるため、シングル ユーザー モードではデータベースにアクセスできなくなります。 詳細については、「[データベースをシングルユーザーモードに設定する](../databases/set-a-database-to-single-user-mode.md)」を参照してください。

 たとえば、次の `ALTER DATABASE` ステートメントは、すべての現在のユーザーがデータベースから切断された後に、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースに対する排他アクセスを取得します。  
  
```  
USE master;  
ALTER DATABASE AdventureWorks2012  
SET SINGLE_USER;  
GO  
```  
  
> [!NOTE]  
>  現在のユーザーをデータベースから直ちに、または指定された秒数内に強制的に戻すには、ROLLBACK オプションを使用します。 ALTER DATABASE *database_name* SET SINGLE_USER WITH rollback *rollback_option*です。 詳細については、「[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)」を参照してください。  
  
## <a name="reattaching-a-database"></a>データベースの再アタッチ  
 デタッチされたファイルはそのまま残り、CREATE DATABASE (FOR ATTACH または FOR ATTACH_REBUILD_LOG オプション) を使用して再アタッチできます。 ファイルを別のサーバーに移動し、そこにアタッチすることもできます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sysadmin**固定サーバーロールのメンバーシップ、またはデータベースの**db_owner**ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースを*skipchecks チェック*を true に設定してデタッチします。  
  
```  
EXEC sp_detach_db 'AdventureWorks2012', 'true';  
```  
  
 次の例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースをデタッチし、フルテキストインデックスファイルとフルテキストインデックスのメタデータを保持します。 このコマンドでは、UPDATE STATISTICS が実行されます。これは既定の動作です。  
  
```  
exec sp_detach_db @dbname='AdventureWorks2012'  
    , @keepfulltextindexfile='true';  
```  
  
## <a name="see-also"></a>参照  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [データベースのデタッチとアタッチ &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [データベースのデタッチ](../../relational-databases/databases/detach-a-database.md)  
  
  
