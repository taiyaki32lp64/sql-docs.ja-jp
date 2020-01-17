---
title: sys.triggers (TRANSACT-SQL) |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- triggers
- triggers_TSQL
- sys.triggers
- sys.triggers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.triggers catalog view
ms.assetid: cefa4fc4-b8b9-4cd7-b124-eed5283acbfc
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 33eb5a1c4176041d64ba60a3a684b75bc4816350
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091929"
---
# <a name="systriggers-transact-sql"></a>sys.triggers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  TR トリガーまたは TA トリガーであるオブジェクトごとに、1 行のデータを格納します。 DML トリガー名は、スキーマ スコープし、そのために表示されます**sys.objects**します。 DDL トリガー名は、親エンティティによってスコープ設定され、このビューに表示されるのみです。  
  
 **Parent_class**と**名前**列は、データベースにトリガーを一意に識別します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|トリガーの名前。 DML トリガー名はスキーマ スコープです。 DDL トリガー名は、親エンティティに関してスコープされます。|  
|**object_id**|**int**|オブジェクト ID 番号。 データベース内で一意です。|  
|**parent_class**|**tinyint**|トリガーの親のクラス。<br /><br /> 0 = DDL トリガー用のデータベース<br /><br /> 1 = DML トリガー用のオブジェクトまたは列|  
|**parent_class_desc**|**nvarchar(60)**|トリガーの親クラスの説明です。<br /><br /> DATABASE<br /><br /> OBJECT_OR_COLUMN|  
|**parent_id**|**int**|次のように、トリガーの親の ID。<br /><br /> 0 = データベースが親となっているトリガー<br /><br /> これは、DML トリガーの場合、 **object_id**テーブルまたはビュー、DML トリガーが定義されているのです。|  
|**type**|**char(2)**|オブジェクトの種類:<br /><br /> TA = アセンブリ (CLR) トリガー<br /><br /> TR = SQL トリガー|  
|**type_desc**|**nvarchar(60)**|オブジェクトの種類の説明です。<br /><br /> CLR_TRIGGER<br /><br /> SQL_TRIGGER|  
|**create_date**|**datetime**|トリガーが作成された日付。|  
|**modify_date**|**datetime**|ALTER ステートメントを使用して、オブジェクトの最終更新日。|  
|**is_ms_shipped**|**bit**|ユーザーの代理として内部で作成されたトリガー[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]コンポーネント。|  
|**is_disabled**|**bit**|トリガーは無効です。|  
|**is_not_for_replication**|**bit**|トリガーは、NOT FOR REPLICATION として作成されました。|  
|**is_instead_of_trigger**|**bit**|1 = INSTEAD OF トリガー<br /><br /> 0 = AFTER トリガー|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [セキュリティ カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
