---
title: sp_helpindex (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpindex_TSQL
- sp_helpindex
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpindex
ms.assetid: c7f73ba0-ec35-4b10-aa5f-f1487e51fbf7
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 17e43f9739b0306a42c4c454cf93fdf92b255177
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68122527"
---
# <a name="sphelpindex-transact-sql"></a>sp_helpindex (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  テーブルまたはビューのインデックスに関する情報をレポートします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpindex [ @objname = ] 'name'  
```  
  
## <a name="arguments"></a>引数  
`[ @objname = ] 'name'` ユーザー定義テーブルまたはビューの修飾付きまたは修飾なしの名前です。 引用符は、テーブルまたはビューの修飾名を指定したときにのみ必要です。 データベース名を含む、完全修飾名が指定されている場合、データベース名は、現在のデータベースの名前である必要があります。 *名前*は**nvarchar (776)** 、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**index_name**|**sysname**|インデックスの名前。|  
|**index_description**|**varchar(210)**|上にあるファイル グループを含むインデックスの説明。|  
|**index_keys**|**nvarchar(2078)**|インデックスの作成で使用するテーブルまたはビュー内の列。|  
  
 降順のインデックス付き列はその名前の後にマイナス記号 (-) を使用して結果セットに表示します。昇順のインデックス列で、既定値は、その名前だけが表示されます。  
  
## <a name="remarks"></a>コメント  
 その情報が含まれている UPDATE STATISTICS の NORECOMPUTE オプションを使用してインデックスが設定されている場合、 **index_description**列。  
  
 **sp_helpindex**は順序付け可能なインデックス列だけを公開します。 したがって、これは公開されません XML インデックスまたは空間インデックスに関する情報。  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、`Customer` テーブルのインデックスの種類に関するレポートを表示します。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_helpindex N'Sales.Customer';  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [データベース エンジン ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)  
  
  
