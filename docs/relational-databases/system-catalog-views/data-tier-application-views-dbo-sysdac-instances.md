---
title: dbo.sysdac_instances (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysdac_instances_TSQL
- sysdac_instances
- sysdac_instances_TSQL
- dbo.sysdac_instances
dev_langs:
- TSQL
helpviewer_keywords:
- dbo.sysdac_instances
- sysdac_instances
ms.assetid: 28285f3d-3889-439f-8b24-3bdef08e46b4
author: stevestein
ms.author: sstein
ms.openlocfilehash: b1530e58597947a7e19f4ca264808fbfefd164ef
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68033113"
---
# <a name="data-tier-application-views---dbosysdacinstances"></a>データ層アプリケーション ビュー - dbo.sysdac_instances
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに配置されたデータ層アプリケーション (DAC) インスタンスごとに 1 行を表示します。 sysdac_instances は、msdb データベースの dbo スキーマに属しています。 次の表では、sysdac_instances ビュー内の列について説明します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|instance_id|**uniqueidentifier**|DAC インスタンスの識別子。|  
|instance_name|**sysname**|DAC インスタンスの名前は、DAC の配置を指定します。|  
|type_name|**sysname**|DAC の名前は、DAC パッケージの作成時に指定します。|  
|type_version|**nvarchar(64)**|DAC パッケージの作成時に指定された DAC のバージョン。|  
|description|**nvarchar (4000)**|DAC パッケージの作成時に指定された DAC の説明。|  
|type_stream|**varbinary(max)**|論理オブジェクト (テーブルやビュー、DAC に含まれているなど) のエンコード表記を含んでいるビット ストリーム。|  
|date_created|**datetime**|DAC インスタンスが作成された日付。|  
|created_by|**sysname**|DAC インスタンスを作成したログイン。|  
|database_name|**sysname**|DAC インスタンスのために作成したデータベースの名前。|  
  
## <a name="remarks"></a>コメント  
 DAC には、テーブルやビューなど、アプリケーションによって使用される論理データ層オブジェクトの定義である DAC 型が含まれています。 DAC パッケージは、DAC を配置に使用するファイルです。 DAC パッケージは、DAC 型に含まれるすべての論理オブジェクトの表現を含んでいます。 DAC パッケージは、1 つ以上のコピー、またはのインスタンスに dac のインスタンスをデプロイするために使用できます、[!INCLUDE[ssDE](../../includes/ssde-md.md)]します。 各 DAC インスタンスは、同じ型で同じ DAC パッケージの共有から展開されているが、一意のインスタンスの名前と識別子を割り当てられています。  
  
## <a name="permissions"></a>アクセス許可  
 すべての列を表示するには、sysadmin 固定サーバー ロールのメンバーシップが必要です。 パブリック ロールのメンバーは、instance_name、description、および type_version の各列を表示できます。  
  
## <a name="see-also"></a>関連項目  
 [[データ層アプリケーション]](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [データ層アプリケーション ビュー &#40;TRANSACT-SQL&#41;](https://msdn.microsoft.com/library/0de01328-d7a6-4677-b7a0-dcd3098c23d4)  
  
  
