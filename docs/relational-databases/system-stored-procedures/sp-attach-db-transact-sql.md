---
title: sp_attach_db (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_attach_db_TSQL
- sp_attach_db
dev_langs:
- TSQL
helpviewer_keywords:
- sp_attach_db
ms.assetid: 59bc993e-7913-4091-89cb-d2871cffda95
author: stevestein
ms.author: sstein
ms.openlocfilehash: 88b0dffa84674b2d7e55895830f28cf1b95cd3dc
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305266"
---
# <a name="sp_attach_db-transact-sql"></a>sp_attach_db (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  データベースをサーバーにアタッチします。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] は、代わりに CREATE DATABASE *database_name* FOR ATTACH を使用することをお勧めします。 詳細については、「[CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)」を参照してください。  
  
> [!NOTE]  
>  複数のログファイルを再構築するには、1つまたは複数の場所に新しい場所がある場合は、CREATE DATABASE *database_name* FOR ATTACH_REBUILD_LOG を使用します。  
  
> [!IMPORTANT]  
>  不明なソースや信頼されていないソースからデータベースをアタッチまたは復元しないことをお勧めします。 こうしたデータベースには、意図しない [!INCLUDE[tsql](../../includes/tsql-md.md)] コードを実行したり、スキーマまたは物理データベース構造を変更してエラーを発生させるような、悪意のあるコードが含まれている可能性があります。 不明または信頼できないソースのデータベースを使用する前に、運用サーバー以外のサーバーでそのデータベースに対し [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) を実行し、さらに、そのデータベースのストアド プロシージャやその他のユーザー定義コードなどのコードを調べます。  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_attach_db [ @dbname= ] 'dbname'  
    , [ @filename1= ] 'filename_n' [ ,...16 ]   
```  
  
## <a name="arguments"></a>引数  
`[ @dbname = ] 'dbnam_ '` サーバーにアタッチするデータベースの名前を指定します。 名前は一意である必要があります。 *dbname*は**sysname**,、既定値は NULL です。  
  
`[ @filename1 = ] 'filename_n'` は、データベースファイルの物理名 (パスを含む) です。 *filename_n*は**nvarchar (260)** ,、既定値は NULL です。 ファイル名は 16 個まで指定できます。 パラメーター名は **\@filename1**から始まり、 **\@filename16**にインクリメントされます。 ファイル名の一覧には、少なくともプライマリファイルが含まれている必要があります。 プライマリファイルには、データベース内の他のファイルを指すシステムテーブルが含まれています。 また、データベースをデタッチした後に移動されたすべてのファイルを一覧に含める必要があります。  
  
> [!NOTE]  
>  この引数は、CREATE DATABASE ステートメントの FILENAME パラメーターにマップされます。 詳細については、「[CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)」を参照してください。  
>   
>  フルテキスト カタログ ファイルを含む [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] データベースを [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] サーバー インスタンスにアタッチする場合、カタログ ファイルは [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]と同様に他のデータベース ファイルと一緒に以前の場所からアタッチされます。 詳細については、「 [フルテキスト検索のアップグレード](../../relational-databases/search/upgrade-full-text-search.md)」を参照してください。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 [InclusionThresholdSetting]  
  
## <a name="remarks"></a>Remarks  
 **Sp_attach_db**ストアドプロシージャは、明示的な**sp_detach_db**操作またはコピーしたデータベースに対してデータベースサーバーから以前にデタッチされたデータベースでのみ実行する必要があります。 16個を超えるファイルを指定する必要がある場合は、CREATE DATABASE *database_name* FOR ATTACH または create database *database_name* FOR_ATTACH_REBUILD_LOG を使用します。 詳細については、「[CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)」を参照してください。  
  
 指定されていないファイルは、最後の既知の場所にあると見なされます。 異なる場所にあるファイルを使用するには、新しい場所を指定する必要があります。  
  
 新しいバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で作成したデータベースは、それ以前のバージョンでアタッチすることはできません。  
  
> [!NOTE]  
>  データベース スナップショットのデタッチおよびアタッチは行うことができません。  
  
 レプリケートされたデータベースをアタッチするとき、そのデータベースがデタッチではなくコピーされたものである場合は、次の点を考慮してください。  
  
-   元のデータベースと同じサーバー インスタンスおよびバージョンにデータベースをアタッチする場合は、必要な追加手順はありません。  
  
-   同じサーバー インスタンスのアップグレードされたバージョンにデータベースをアタッチする場合は、アタッチ操作が完了した後、[sp_vupgrade_replication](../../relational-databases/system-stored-procedures/sp-vupgrade-replication-transact-sql.md) を実行してレプリケーションをアップグレードする必要があります。  
  
-   バージョンに関係なく、別のサーバー インスタンスにデータベースをアタッチする場合は、アタッチ操作が完了した後、[sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) を実行してレプリケーションを削除する必要があります。  
  
 データベースが最初に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の新しいインスタンスにアタッチまたは復元されるとき、データベース マスター キー (サービス マスター キーにより暗号化されたもの) のコピーはまだサーバーに格納されていません。 **OPEN MASTER KEY** を使用して、データベース マスター キー (DMK) を暗号化解除する必要があります。 DMK の暗号化が解除されると、 **ALTER MASTER KEY REGENERATE** ステートメントを使用して、サービス マスター キー (SMK) で暗号化された DMK のコピーをサーバーに提供することにより、将来、自動的に暗号化解除することも可能となります。 データベースを以前のバージョンからアップグレードした場合、新しい AES アルゴリズムを使用するように DMK を再作成する必要があります。 DMK を再作成する方法については、「[ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)」を参照してください。 DMK キーを再作成して AES にアップグレードするのに必要な時間は、DMK によって保護されているオブジェクトの数によって異なります。 DMK キーを再作成して AES にアップグレードする作業は、1 回限りで済み、今後のキー ローテーション方法には影響を与えません。  
  
## <a name="permissions"></a>アクセス許可  
 データベースがアタッチされているときの権限の処理方法については、「 [ &#40;CREATE&#41;database SQL Server transact-sql](../../t-sql/statements/create-database-sql-server-transact-sql.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
 次の例では、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] のファイルを現在のサーバーにアタッチします。  
  
```  
EXEC sp_attach_db @dbname = N'AdventureWorks2012',   
    @filename1 =   
N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\AdventureWorks2012_Data.mdf',   
    @filename2 =   
N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\AdventureWorks2012_log.ldf';  
```  
  
## <a name="see-also"></a>参照  
 [データベースのデタッチとアタッチ &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [sp_detach_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)   
 [sp_helpfile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)   
 [sp_removedbreplication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
