---
title: sp_helptrigger (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helptrigger
- sp_helptrigger_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helptrigger
ms.assetid: e486d39b-771d-488d-a786-7136433a2203
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1e6244443fc1f6ba7d83376226fedd56563e0d39
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68048218"
---
# <a name="sphelptrigger-transact-sql"></a>sp_helptrigger (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  現在のデータベースにある、指定したテーブルに定義されている DML トリガーの種類を返します。 sp_helptrigger は DDL トリガーでは使用できません。 クエリ、[システム ストアド プロシージャ](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)カタログ ビューを代わりにします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helptrigger [ @tabname = ] 'table'   
     [ , [ @triggertype = ] 'type' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @tabname = ] 'table'` トリガー情報を返す対象の現在のデータベース内のテーブルの名前です。 *テーブル*は**nvarchar (776)** 、既定値はありません。  
  
`[ @triggertype = ] 'type'` 情報を返す DML トリガーの種類です。 *型*は**char (6)** 、既定値は null の場合、これらの値のいずれかを指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**DELETE**|DELETE トリガー情報を返します。|  
|**INSERT**|INSERT トリガー情報を返します。|  
|**UPDATE**|UPDATE トリガー情報を返します。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 次の表では、結果セット内に含まれる情報を示します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**trigger_name**|**sysname**|トリガーの名前。|  
|**trigger_owner**|**sysname**|トリガーが定義されたテーブルの所有者の名前。|  
|**isupdate**|**int**|1 = UPDATE トリガー<br /><br /> 0 = UPDATE トリガーではありません|  
|**isdelete**|**int**|1 = DELETE トリガー<br /><br /> 0 = DELETE トリガーではありません|  
|**isinsert**|**int**|1 = INSERT トリガー。<br /><br /> 0 = INSERT トリガー以外。|  
|**isafter**|**int**|1 = AFTER トリガー<br /><br /> 0 = AFTER トリガーではありません|  
|**isinsteadof**|**int**|1 = instead OF トリガー<br /><br /> 0 = INSTEAD OF トリガー以外。|  
|**trigger_schema**|**sysname**|トリガーが属するスキーマの名前です。|  
  
## <a name="permissions"></a>アクセス許可  
 必要があります[Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)テーブルに対する権限。  
  
## <a name="examples"></a>使用例  
 次の例では実行`sp_helptrigger`のトリガーに関する情報を生成するために、`Person.Person`テーブル。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_helptrigger 'Person.Person';  
```  
  
## <a name="see-also"></a>関連項目  
 [データベース エンジン ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
