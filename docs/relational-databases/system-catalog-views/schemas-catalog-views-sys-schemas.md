---
title: sys.schemas (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- schemas_TSQL
- sys.schemas_TSQL
- schemas
- sys.schemas
dev_langs:
- TSQL
helpviewer_keywords:
- sys.schemas catalog view
ms.assetid: 29af5ce5-2af7-4103-8f08-3ec92603ba05
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8f5a0707c599b70ec3c006b00eacb5f8c1a8a87b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68018343"
---
# <a name="schemas-catalog-views---sysschemas"></a>スキーマ カタログ ビュー - sys.schemas
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  データベース スキーマごとに 1 行が含まれています。  
  
> [!NOTE]  
>  データベース スキーマは、XML ドキュメントのコンテンツ モデルの定義に使用される XML スキーマとは異なります。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|スキーマの名前。 データベース内で一意です。|  
|**schema_id**|**int**|スキーマの ID です。 データベース内で一意です。|  
|**principal_id**|**int**|このスキーマを所有するプリンシパルの ID。|  
  
## <a name="remarks"></a>コメント  
名前空間または内にあるテーブル、ビュー、プロシージャ、関数、およびなどのオブジェクトのコンテナーとして使用するデータベース スキーマ、 **sys.objects**カタログ ビューです。  

各スキーマが、所有者。 所有者がセキュリティ[プリンシパル](../../relational-databases/security/authentication-access/principals-database-engine.md)します。
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
[プリンシパル](../../relational-databases/security/authentication-access/principals-database-engine.md)

[カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   

[スキーマ カタログ ビュー &#40;TRANSACT-SQL&#41;](https://msdn.microsoft.com/library/c516fb1c-b6ed-48ae-99c7-a78bc4336c8e)   

[sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
  
