---
title: sysdac_instances_internal (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdac_instances_internal_TSQL
- sysdac_instances_internal
dev_langs:
- TSQL
helpviewer_keywords:
- sysdac_instances_internal
ms.assetid: d2d52cc4-3463-431a-b779-6fbfdeee1dfc
author: stevestein
ms.author: sstein
ms.openlocfilehash: e8cec14e22779391d954b2a666782e8783f50f3a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68084746"
---
# <a name="data-tier-application-tables---sysdacinstancesinternal"></a>データ層アプリケーション テーブル - sysdac_instances_internal
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに配置されたデータ層アプリケーション (DAC) インスタンスごとに 1 行を表示します。 このテーブルは、msdb データベースの dbo スキーマに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|instance_id|**uniqueidentifier**|DAC インスタンスの識別子。|  
|instance_name|**sysname**|DAC インスタンスの名前は、インスタンスの配置時に指定します。|  
|type_name|**sysname**|DAC の名前は、DAC パッケージの作成時に指定します。|  
|type_version|**nvarchar(64)**|DAC パッケージの作成時に指定された DAC のバージョン。|  
|description|**nvarchar (4000)**|DAC パッケージの作成時に指定された DAC の説明。|  
|type_stream|**varbinary(max)**|論理オブジェクト (テーブルやビュー、DAC に含まれているなど) のエンコード表記を含んでいるビット ストリーム。|  
|date_created|**datetime**|DAC インスタンスが作成された日付。|  
|created_by|**sysname**|DAC インスタンスを作成したログイン。|  
  
## <a name="remarks"></a>コメント  
 このビューに読み取り専用のアクセスは、master データベースに接続するアクセス許可を持つすべてのユーザーに使用できます。  
  
## <a name="permissions"></a>アクセス許可  
 sysadmin 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="see-also"></a>関連項目  
 [[データ層アプリケーション]](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [dbo.sysdac_instances &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/data-tier-application-views-dbo-sysdac-instances.md)  
  
  
