---
title: sp_helpfile を実行する (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpfile
- sp_helpfile_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpfile
ms.assetid: 1546e0ae-5a99-4e01-9eb9-d147fa65884c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7b60f4929bd537089c05211cc3ecc548b82b6307
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67943492"
---
# <a name="sphelpfile-transact-sql"></a>sp_helpfile を実行する (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  現在のデータベースに関連付けられたファイルの物理名と属性を返します。 このストアド プロシージャを使用して、アタッチまたはサーバーからデタッチするファイルの名前を決定します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpfile [ [ @filename= ] 'name' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @filename = ] 'name'` 現在のデータベース内のすべてのファイルの論理名です。 *名前* は **sysname** 、既定値は NULL です。 場合*名前*が指定されていない、現在のデータベース内のすべてのファイルの属性が返されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|論理ファイル名です。|  
|**fileid**|**smallint**|ファイルの数値識別子。 場合は返されません*名前*が指定されて*します。*|  
|**filename**|**nchar(260)**|物理ファイル名。|  
|**filegroup**|**sysname**|ファイルが属しているファイル グループ。<br /><br /> NULL = ファイルは、ログ ファイル。 ファイル グループの一部ではありません。|  
|**size**|**nvarchar(15)**|ファイル サイズ (KB 単位) です。|  
|**maxsize**|**nvarchar(15)**|ファイルの最大拡張サイズです。 このフィールドの値が UNLIMITED である場合、ディスクがいっぱいになるまでファイルを拡張できることを示します。|  
|**growth**|**nvarchar(15)**|ファイルの拡張増分値。 これは、その新しい領域が必要するたびに、ファイルに追加される領域の容量を示します。<br /><br /> 0 = ファイルのサイズは固定されており、容量を追加することはできません。|  
|**使用状況**|**varchar (9)**|データ ファイルの場合、値は **'data only'** とログ ファイルの値が **'ログのみ'** します。|  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例は、内のファイルに関する情報を返します[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]します。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_helpfile;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [データベース エンジン ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_helpfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpfilegroup-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [データベース ファイルとファイル グループ](../../relational-databases/databases/database-files-and-filegroups.md)  
  
  
