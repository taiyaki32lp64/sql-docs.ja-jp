---
title: syspolicy_conditions (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syspolicy_conditions
- syspolicy_conditions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_conditions view
ms.assetid: af97d26c-4bd5-4b08-be51-8419e3b2832c
author: stevestein
ms.author: sstein
ms.openlocfilehash: ee0f269fcfda93733d36a0b7396fd72d16bc01d9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68121172"
---
# <a name="syspolicyconditions-transact-sql"></a>syspolicy_conditions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  インスタンスでポリシー ベースの管理条件ごとに 1 つの行を表示します。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 syspolicy_conditions は、msdb データベースの dbo スキーマに属します。 次の表では、syspolicy_conditions ビュー内の列について説明します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|condition_id|**int**|この条件の識別子。 各条件は、1 つまたは複数の条件式のコレクションを表します。|  
|NAME|**sysname**|条件の名前。|  
|date_created|**datetime**|条件が作成された日付と時刻。|  
|description|**nvarchar(max)**|条件の説明。 この説明の列は省略可能であり、NULL の場合もあります。|  
|created_by|**sysname**|条件を作成したログイン。|  
|modified_by|**sysname**|最後に、条件を変更したログイン。 変更されていない場合は NULL です。|  
|date_modified|**datetime**|条件が作成された日付と時刻。 変更されていない場合は NULL です。|  
|is_name_condition|**smallint**|条件が名前付け条件であるかどうかを指定します。<br /><br /> 0 = 条件式には @Name 変数が含まれません。<br /><br /> 1 = 条件式が含まれています、@Name変数。|  
|ファセット (facet)|**nvarchar(max)**|条件に基づくファセットの名前。|  
|式|**nvarchar(max)**|ファセットの状態の式。|  
|obj_name|**sysname**|割り当てられたオブジェクト名@Name条件式には、この変数が含まれている場合。|  
  
## <a name="remarks"></a>コメント  
 ポリシー ベースの管理のトラブルシューティングを行う場合に、条件を作成または最後に変更したユーザーを特定するには、syspolicy_conditions ビューを照会します。  
  
## <a name="permissions"></a>アクセス許可  
 msdb データベースの PolicyAdministratorRole ロールのメンバーシップが必要です。  
  
## <a name="see-also"></a>関連項目  
 [ポリシー ベースの管理を使用したサーバーの管理](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [ポリシーベースの管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
