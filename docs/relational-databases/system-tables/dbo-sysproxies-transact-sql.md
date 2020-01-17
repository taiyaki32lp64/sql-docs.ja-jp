---
title: dbo.sysproxies (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysproxies_TSQL
- sysproxies_TSQL
- dbo.sysproxies
- sysproxies
dev_langs:
- TSQL
helpviewer_keywords:
- sysproxies system table
ms.assetid: a73da875-be22-45fc-b5e2-ea7ebd48e2d6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1dd486757a912d8f0364f55570a368292cf39ab7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67984895"
---
# <a name="dbosysproxies-transact-sql"></a>dbo.sysproxies (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  属性を定義、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェント プロキシ アカウント。 このテーブルに格納されます、 **msdb**データベース。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|プロキシ アカウントの ID。|  
|**name**|**sysname**|プロキシ アカウントの名前。|  
|**credential_id**|**int**|プロキシ アカウントが使用する資格情報の ID。|  
|**enabled**|**tinyint**|プロキシ アカウントの状態。<br /><br /> **0** = 無効になっています。 **1** = 有効にします。|  
|**description**|**nvarchar(512)**|プロキシ アカウントの作成時に、ユーザーが入力した説明。|  
|**user_sid**|**varbinary(85)**|Microsoft Windows *security_identifier*ユーザーまたはグループがプロキシ資格情報に関連付けられているのです。|  
|**credential_date_created**|**datetime**|日付と、資格情報が作成された時刻。|  
  
## <a name="remarks"></a>コメント  
 メンバーのみ、 **sysadmin**固定サーバー ロールがアクセスできる、 **sysproxies**テーブル。  
  
## <a name="see-also"></a>関連項目  
 [dbo.sysproxylogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/dbo-sysproxylogin-transact-sql.md)   
 [dbo.sysproxysubsystem &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)   
 [dbo.syssubsystems &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/dbo-syssubsystems-transact-sql.md)  
  
  
