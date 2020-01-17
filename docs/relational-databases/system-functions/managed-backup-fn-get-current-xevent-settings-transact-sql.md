---
title: managed_backup.fn_get_current_xevent_settings (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_get_current_xevent_settings
- smart_admin.fn_get_current_xevent_settings_TSQL
- fn_get_current_xevent_settings_TSQL
- smart_admin.fn_get_current_xevent_settings
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.fn_get_current_xevent_settings
- fn_get_current_xevent_settings
ms.assetid: 95d3adaa-bb9d-4833-b8b4-3d9fd4f9c82a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4133f8bb64d5d7e2e2b511c2128b9ddbca1fa550
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67910245"
---
# <a name="managedbackupfngetcurrentxeventsettings-transact-sql"></a>managed_backup.fn_get_current_xevent_settings (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  スマート Admn でサポートされている拡張イベントの種類ごとに 1 つの行を返します。  
  
 返すか、構成可能なイベントと、現在の構成の種類を識別する拡張イベントの現在の設定を確認するには、この関数を使用します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
smart_admin.fn_get_current_xevent_settings ()   
```  
  
##  <a name="Arguments"></a> 引数  
 この関数には、任意の引数はありません。  
  
## <a name="table-returned"></a>返されるテーブル  
 拡張イベントの管理、分析、運用のチャネルは必須であり、既定で有効になっていますが、構成することはできません。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|Event_name|NVARCHAR (128)|拡張イベントの種類|  
|is_configurable|NVARCHAR (128)|設定されているこの**True**イベントが構成可能な場合は、それ以外の場合に設定が**False**します。|  
|is_enabled|NVARCHAR (128)|イベントが有効な場合は True に設定されます。有効でない場合は False に設定されます。 デバッグ イベントを有効にするには、smart_admin.sp_set_parameter を使用します。|  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 必要があります**選択**関数に対する権限。  
  
## <a name="examples"></a>使用例  
 次の例では、すべての拡張イベントが現在の状態と共に返されます。  
  
```  
SELECT *   
FROM smart_admin.fn_get_current_xevent_settings ()  
  
```  
  
  
