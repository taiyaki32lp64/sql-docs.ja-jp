---
title: sys.dm_xe_object_columns (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_xe_object_columns
- sys.dm_xe_object_columns_TSQL
- dm_xe_object_columns_TSQL
- dm_xe_object_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_object_columns dynamic management view
- extended events [SQL Server], views
ms.assetid: d96a14f3-4284-45ff-b1fe-4858e540a013
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8b44824310637b279388ea367cd4ab1d07401d1f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68090283"
---
# <a name="sysdmxeobjectcolumns-transact-sql"></a>sys.dm_xe_object_columns (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  すべてのオブジェクトのスキーマ情報を返します。  
  
> [!NOTE]  
>  イベント オブジェクトは、読み取り専用と読み取り/書き込みデータの両方の固定スキーマを公開します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|NAME|**nvarchar (256)**|列の名前です。 名前は、オブジェクト内で一意です。 NULL 値は許可されません。|  
|column_id|**int**|列の識別子。 column_id は、column_type と共に使用する場合、オブジェクト内で一意です。 NULL 値は許可されません。|  
|object_name|**nvarchar (256)**|この列が所属するオブジェクトの名前。 Sys.dm_xe_objects.id 多対一のリレーションシップがあります。NULL 値は許可されません。|  
|object_package_guid|**uniqueidentifier**|オブジェクトを含むパッケージの GUID です。 NULL 値は許可されません。|  
|type_name|**nvarchar (256)**|この列の型の名前。 NULL 値は許可されません。|  
|type_package_guid|**uniqueidentifier**|列のデータ型を含むパッケージの GUID。 NULL 値は許可されません。|  
|column_type|**nvarchar(60)**|この列の使用方法を示します。 NULL 値は許可されません。 column_type には、次のいずれかを指定できます。<br /><br /> 読み取り専用です。 列には、変更できない静的な値が含まれています。<br /><br /> data。 オブジェクトによって公開される実行時データが列に格納されます。<br /><br /> カスタマイズ可能です。 列には、変更可能な値が含まれています。<br /><br /> 注:この値を変更すると、オブジェクトの動作を変更できます。|  
|column_value|**nvarchar (256)**|オブジェクト列に関連付けられた静的な値を表示します。 NULL 値が許可されます。|  
|機能|**int**|列の機能を説明するビットマップ。 NULL 値が許可されます。|  
|capabilities_desc|**nvarchar (256)**|このオブジェクトの列の機能の説明。 この値には、次のいずれかを指定できます。<br /><br /> 必須。 親オブジェクトをイベント セッションにバインドするときに値を設定する必要があります。<br /><br /> NULL 値が許可されます。|  
|description|**nvarchar(3072)**|このオブジェクトの列の説明です。 NULL 値が許可されます。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
### <a name="relationship-cardinalities"></a>リレーションシップの基数  
  
|From|変換先|リレーションシップ|  
|----------|--------|------------------|  
|sys.dm_xe_object_columns.object_name、sys.dm_xe_object_columns.object_package_guid|sys.dm_xe_objects.name、<br /><br /> sys.dm_xe_objects.package_guid|多対一|  
|sys.dm_xe_object_columns.type_name<br /><br /> sys.dm_xe_object_columns.type_package_guid|sys.dm_xe_objects.name<br /><br /> sys.dm_xe_objects.package_guid|多対一|  
  
## <a name="see-also"></a>関連項目  
 [動的管理ビューおよび関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

