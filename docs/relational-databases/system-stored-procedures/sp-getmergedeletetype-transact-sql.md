---
title: sp_getmergedeletetype (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_getmergedeletetype
- sp_getmergedeletetype_TSQL
helpviewer_keywords:
- sp_getmergedeletetype
ms.assetid: 64450e4d-844d-4176-874e-f3845536f7d2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 478d483da545a6b149a0fb2b03c41f106a73da60
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68123977"
---
# <a name="spgetmergedeletetype-transact-sql"></a>sp_getmergedeletetype (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  マージ削除の型を返します。 このストアド プロシージャは、パブリケーション データベースに対して、パブリッシャーまたはサブスクライバーのサブスクリプション データベースで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_getmergedeletetype [ @source_object = ] 'source_object', [ @rowguid =] 'rowguid', [ @delete_type=] delete_type OUTPUT  
```  
  
## <a name="arguments"></a>引数  
`[ @source_object = ] 'source_object'` ソース オブジェクトの名前です。 *source_object*は**nvarchar (386)** 、既定値はありません。  
  
`[ @rowguid = ] 'rowguid'` 削除の型の行の識別子です。 *rowguid*は**uniqueidentifier**、既定値はありません。  
  
`[ @delete_type = ] delete_type OUTPUT` 削除の種類をコードを示すです。 *delete_type*は**int**、既定値はありません。 *delete_type*は、出力パラメーターでも、これらの値のいずれかを指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**1**|ユーザーの削除|  
|**5**|部分的な削除|  
|**6**|システム削除|  
  
## <a name="remarks"></a>コメント  
 **sp_getmergedeletetype**はマージ レプリケーションで使用します。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールまたは**db_owner**固定データベース ロールが実行できる**sp_getmergedeletetype**します。  
  
## <a name="see-also"></a>関連項目  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
