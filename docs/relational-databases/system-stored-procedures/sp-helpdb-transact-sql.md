---
title: sp_helpdb (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpdb
- sp_helpdb_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpdb
ms.assetid: 4c3e3302-6cf1-4b2b-8682-004049b578c3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7acc14d3950e0e2d1004727b2efbffd2e4963a2b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67903017"
---
# <a name="sphelpdb-transact-sql"></a>sp_helpdb (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定されたデータベースまたはすべてのデータベースに関する情報が報告されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpdb [ [ @dbname= ] 'name' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @dbname = ] 'name'` 情報を報告するデータベースの名前です。 *名前*は**sysname**、既定値はありません。 場合*名前*が指定されていない**sp_helpdb**のすべてのデータベース上のレポート、 **sys.databases**カタログ ビューです。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|データベース名。|  
|**db_size**|**nvarchar(13)**|データベースの合計サイズ。|  
|**所有者**|**sysname**|データベースの所有者は、 **sa**します。|  
|**dbid**|**smallint**|データベース ID。|  
|**created**|**nvarchar(11)**|データベースの作成日です。|  
|**status**|**nvarchar(600)**|データベースで現在設定されているデータベース オプションの値のコンマ区切りリスト。<br /><br /> ブール値を持つオプションは、有効になっている場合にのみリストに追加されます。 形式でそれらの値、ブール型以外のオプションが表示*option_name*=*値*します。<br /><br /> 詳細については、「[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)」を参照してください。|  
|**compatibility_level**|**tinyint**|データベース互換性レベル:60、65、70、80、または 90 です。|  
  
 場合*名前*を指定すると、指定されたデータベースのファイルの割り当てを表示する追加の結果セットが存在します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**nchar(128)**|論理ファイル名です。|  
|**fileid**|**smallint**|ファイル ID。|  
|**filename**|**nchar(260)**|オペレーティング システムのファイルの名前 (物理ファイル名)。|  
|**filegroup**|**nvarchar(128)**|ファイルが属しているファイル グループ。<br /><br /> NULL = ファイルは、ログ ファイル。 ファイル グループの一部ではありません。|  
|**size**|**nvarchar(18)**|ファイル サイズ (メガバイト単位)。|  
|**maxsize**|**nvarchar(18)**|ファイルの最大拡張サイズです。 このフィールドの値が UNLIMITED である場合、ディスクがいっぱいになるまでファイルを拡張できることを示します。|  
|**growth**|**nvarchar(18)**|ファイルの拡張増分値。 これは、新しい領域が必要なファイルに追加される領域の容量を示します。|  
|**使用状況**|**varchar (9)**|ファイルの使用量。 データ ファイルの場合、値は **'data only'** とログ ファイルの値が **'ログのみ'** します。|  
  
## <a name="remarks"></a>コメント  
 **状態**結果の列は、オプションは、データベースで ON に設定されているレポートを設定します。 すべてのデータベース オプションがによって報告されていない、**状態**列。 現在のデータベース オプションの設定の完全な一覧を表示する、 **sys.databases**カタログ ビューです。  
  
## <a name="permissions"></a>アクセス許可  
 1 つのデータベースが指定されている場合、メンバーシップ、**パブリック**データベース内のロールが必要です。 データベースが指定されていない場合のメンバーシップ、**パブリック**における役割、**マスター**データベースが必要です。  
  
 データベースにアクセスできない場合**sp_helpdb**可能な限り、データベースに関するエラー メッセージ 15622 とあまり情報が表示されます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-returning-information-about-a-single-database"></a>A. 1 つのデータベースに関する情報を返す  
 次の例では、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースに関する情報を表示します。  
  
```sql  
EXEC sp_helpdb N'AdventureWorks2012';  
```  
  
### <a name="b-returning-information-about-all-databases"></a>B. すべてのデータベースに関する情報を返す  
 次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行するサーバー上のすべてのデータベースに関する情報を表示します。  
  
```sql  
EXEC sp_helpdb;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [データベース エンジン ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
