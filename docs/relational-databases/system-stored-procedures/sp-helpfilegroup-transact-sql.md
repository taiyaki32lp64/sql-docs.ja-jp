---
title: sp_helpfilegroup (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpfilegroup_TSQL
- sp_helpfilegroup
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpfilegroup
ms.assetid: 619716b5-95dc-4538-82ae-4b90b9da8ebc
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6fe9798b6a9f560621eba9806e25081f72e316c8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68122544"
---
# <a name="sphelpfilegroup-transact-sql"></a>sp_helpfilegroup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  現在のデータベースに関連付けられたファイル グループの名前と属性を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpfilegroup [ [ @filegroupname = ] 'name' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @filegroupname = ] 'name'` 現在のデータベース内のファイル グループの論理名です。 *名前* は **sysname** 、既定値は NULL です。 場合*名前*が指定されていない、現在のデータベース内のすべてのファイル グループが一覧表示され、結果セット セクションに表示される設定最初の結果だけが表示されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**groupname**|**sysname**|ファイル グループの名前。|  
|**groupid**|**smallint**|数値ファイル グループ識別子です。|  
|**filecount**|**int**|ファイル グループ内のファイルの数。|  
  
 場合*名前*は指定すると、ファイル グループ内の各ファイルの 1 つの行が返されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**file_in_group**|**sysname**|グループ内のファイルの論理名。|  
|**fileid**|**smallint**|数値ファイル識別子です。|  
|**filename**|**nchar(260)**|ディレクトリ パスを含むファイルの物理名。|  
|**size**|**nvarchar(15)**|ファイル サイズ (KB 単位) です。|  
|**maxsize**|**nvarchar(15)**|ファイルの最大サイズ。<br /><br /> この値は、ファイルのサイズの上限です。 このフィールドの値が UNLIMITED である場合、ディスクがいっぱいになるまでファイルを拡張できることを示します。|  
|**growth**|**nvarchar(15)**|ファイルの拡張増分値。 これは、新しい領域が必要するたびに、ファイルに追加される領域の容量を示します。<br /><br /> 0 = ファイルのサイズは固定されており、容量を追加することはできません。|  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-returning-all-filegroups-in-a-database"></a>A. データベース内のすべてのファイル グループを返す  
 次の例は、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] サンプル データベースのファイル グループに関する情報を返します。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_helpfilegroup;  
GO  
```  
  
### <a name="b-returning-all-files-in-a-filegroup"></a>B. ファイル グループ内のすべてのファイルを返す  
 次の例は、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] サンプル データベースの `PRIMARY` ファイル グループにあるすべてのファイルの情報を返します。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_helpfilegroup 'PRIMARY';  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [データベース エンジン ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_helpfile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [データベース ファイルとファイル グループ](../../relational-databases/databases/database-files-and-filegroups.md)  
  
  
