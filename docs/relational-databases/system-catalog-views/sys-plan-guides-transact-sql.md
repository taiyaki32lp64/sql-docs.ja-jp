---
title: sys.plan_guides (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.planguides_TSQL
- plan_guides
- sys.planguides
- plan_guides_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.plan_guides catalog view
ms.assetid: 3dde0397-ef6f-4b3f-8250-3f25584eb62b
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 19b78ff53b5640d74b49d2e5956c39aa1df2e230
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068074"
---
# <a name="sysplanguides-transact-sql"></a>sys.plan_guides (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  データベース内のプラン ガイドごとに 1 行のデータを保持します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**plan_guide_id**|**int**|データベースのプラン ガイドの一意の識別子。|  
|**name**|**sysname**|プラン ガイドの名前です。|  
|**create_date**|**datetime**|プラン ガイドが作成された日時。|  
|**modify_date**|**DateTime**|プラン ガイドの最終変更日。|  
|**is_disabled**|**bit**|1 = プラン ガイドが無効になっています。<br /><br /> 0 = プラン ガイドは有効です。|  
|**ステートメント**|**nvarchar(max)**|プラン ガイドの作成対象であるクエリのテキストです。|  
|**scope_type**|**tinyint**|プラン ガイドのスコープを識別します。<br /><br /> 1 = OBJECT<br /><br /> 2 = SQL<br /><br /> 3 = TEMPLATE|  
|**scope_type_desc**|**nvarchar(60)**|プラン ガイドのスコープの説明。<br /><br /> OBJECT<br /><br /> SQL<br /><br /> TEMPLATE|  
|**scope_object_id**|**Int**|スコープがオブジェクトである場合に、プラン ガイドのスコープを定義するオブジェクトの object_id です。<br /><br /> プラン ガイドのスコープはオブジェクトにない場合は NULL です。|  
|**scope_batch**|**nvarchar(max)**|バッチ テキスト場合**scope_type**は SQL です。<br /><br /> バッチ型が SQL でない場合は、NULL です。<br /><br /> NULL の場合と**scope_type** SQL では、値は、**ステートメント**適用されます。|  
|**parameters**|**nvarchar(max)**|プラン ガイドに関連付けられているパラメーターの一覧を定義する文字列です。<br /><br /> NULL = パラメーターはありません ボックスの一覧は、プラン ガイドに関連付けられています。|  
|**ヒント**|**nvarchar(max)**|プラン ガイドに関連付けられている OPTION 句のヒント。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
  
