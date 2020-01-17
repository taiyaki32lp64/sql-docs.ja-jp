---
title: sp_help_targetservergroup (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_targetservergroup_TSQL
- sp_help_targetservergroup
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_targetservergroup
ms.assetid: ec3a4a68-b591-431c-9518-053ede522d0c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 63a3d9daa48bb98408c3f0d9b8282e8083849cf0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085073"
---
# <a name="sphelptargetservergroup-transact-sql"></a>sp_help_targetservergroup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定したグループ内のすべてのターゲット サーバーを表示します。 グループを指定しない場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではすべてのターゲット サーバー グループに関する情報が返されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_targetservergroup  
    [ [ @name = ] 'name' ]  
```  
  
## <a name="argument"></a>引数  
`[ @name = ] 'name'` 情報を返す対象サーバー グループの名前です。 *名前* は **sysname** 、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**servergroup_id**|**int**|サーバー グループの識別番号|  
|**name**|**sysname**|サーバー グループの名前|  
  
## <a name="permissions"></a>アクセス許可  
 既定ではこのプロシージャを実行する権限、 **sysadmin**固定サーバー ロール。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-listing-information-for-all-target-server-groups"></a>A. すべてのターゲット サーバー グループの情報を一覧表示する  
 次の例では、すべてのターゲット サーバー グループの情報を一覧表示します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_targetservergroup ;  
GO  
```  
  
### <a name="b-listing-information-for-a-specific-target-server-group"></a>B. 特定のターゲット サーバー グループの情報を一覧表示する  
 次の例では、ターゲット サーバー グループ `Servers Maintaining Customer Information` の情報を一覧表示します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_targetservergroup   
    N'Servers Maintaining Customer Information' ;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [sp_add_targetservergroup &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-targetservergroup-transact-sql.md)   
 [sp_delete_targetservergroup &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-targetservergroup-transact-sql.md)   
 [sp_update_targetservergroup &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-targetservergroup-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
