---
title: sp_helpconstraint (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpconstraint
- sp_helpconstraint_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpconstraint
ms.assetid: 29d6cd36-535d-4765-bca8-62f9d9886ff5
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d722d3b54c2f0b6d73660e2195aed4039e1eda2c
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771085"
---
# <a name="sphelpconstraint-transact-sql"></a>sp_helpconstraint (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  すべての制約の種類、ユーザー定義またはシステムが指定した名前、それらが定義されている列、および制約を定義する式 (DEFAULT 制約と CHECK 制約の場合のみ) の一覧を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpconstraint [ @objname = ] 'table'   
     [ , [ @nomsg = ] 'no_message' ]   
```  
  
## <a name="arguments"></a>引数  
`[ @objname = ] 'table'`返される制約情報に関するテーブルを指定します。 指定したテーブルは現在のデータベースに対してローカルである必要があります。 *テーブル*は**nvarchar (776)** ,、既定値はありません。  
  
`[ @nomsg = ] 'no_message'`テーブル名を出力する省略可能なパラメーターです。 *no_message*は**varchar (5)** ,、既定値は**msg**です。**nomsg は**は印刷を抑制します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 **sp_helpconstraint**は、主キーに参加している場合は、降順のインデックス付き列を表示します。 降順のインデックス付き列は、名前の後にマイナス記号 (-) を付けて結果セットに一覧表示されます。 既定の昇順のインデックス付き列は、名前だけで一覧表示されます。  
  
## <a name="remarks"></a>コメント  
 **Sp_help**_テーブル_を実行すると、指定したテーブルに関するすべての情報が報告されます。 制約情報のみを表示するには、 **sp_helpconstraint**を使用します。  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 この例では、`Product` テーブルの制約をすべて表示します。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_helpconstraint 'Production.Product';  
```  
  
## <a name="see-also"></a>関連項目  
 [ストアドプロシージャ&#40;のデータベースエンジン transact-sql&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys. キー制約&#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md)   
 [check_constraints &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md)   
 [default_constraints &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-default-constraints-transact-sql.md)  
  
  
