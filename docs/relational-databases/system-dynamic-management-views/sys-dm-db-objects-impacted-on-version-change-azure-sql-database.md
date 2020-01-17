---
title: dm_db_objects_impacted_on_version_change
titleSuffix: Azure SQL Database
ms.date: 03/03/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_objects_impacted_on_version_change_TSQL
- dm_db_objects_impacted_on_version_change
- dm_db_objects_impacted_on_version_change_TSQL
- sys.dm_db_objects_impacted_on_version_change
dev_langs:
- TSQL
helpviewer_keywords:
- dm_db_objects_impacted_on_version_change
- sys.dm_db_objects_impacted_on_version_change
ms.assetid: b94af834-c4f6-4a27-80a6-e8e71fa8793a
author: stevestein
ms.author: sstein
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.custom: seo-dt-2019
ms.openlocfilehash: 0255f7260044ee5c09d020f3ba6310d24bc8cb74
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843857"
---
# <a name="sysdm_db_objects_impacted_on_version_change-azure-sql-database"></a>sys.dm_db_objects_impacted_on_version_change (Azure SQL データベース)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  このデータベーススコープのシステムビューは、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]でのメジャーリリースアップグレードの影響を受けるオブジェクトを決定するための早期警告システムを提供するように設計されています。 このビューを使用すると、アップグレードの前または後に、影響を受けるすべてのオブジェクトのリストを取得できます。 サーバー全体で完全なアカウンティングを取得するには、各データベースでこのビューに対してクエリを実行する必要があります。  
  
|列名|[データ型]|説明|  
|-----------------|---------------|-----------------|  
|class|**int**NULL 以外|影響を受けるオブジェクトのクラス。<br /><br /> **1** = 制約<br /><br /> **7** = インデックスとヒープ|  
|class_desc|**nvarchar (60)** NULL 以外|クラスの説明です。<br /><br /> **OBJECT_OR_COLUMN**<br /><br /> **INDEX**|  
|major_id|**int**NULL 以外|制約のオブジェクト ID、あるいはインデックスまたはヒープを含んでいるテーブルのオブジェクト ID。|  
|minor_id|**int**空白|制約の場合は**NULL**<br /><br /> インデックスとヒープの Index_id|  
|関係|**nvarchar (60)** NULL 以外|制約またはインデックスが影響を受ける原因となっている依存関係の説明。 アップグレード中に生成される警告にも同じ値が使用されます。<br /><br /> 例 :<br /><br /> **space** (組み込みの場合)<br /><br /> **geometry** (システム UDT の場合)<br /><br /> **geography::P arse** (システム UDT メソッド用)|  
  
## <a name="permissions"></a>アクセス許可  
 VIEW DATABASE STATE 権限が必要です。  
  
## <a name="example"></a>例  
 次の例では、次の主要なサーバーバージョンへのアップグレードによって影響を受けるオブジェクトを検索するために、dm_db_objects_impacted_on_version_change に対するクエリを示し**ます。**  
  
```  
SELECT * FROM sys.dm_db_objects_disabled_on_version_change;  
GO  
```  
  
```  
class  class_desc        major_id    minor_id    dependency                       
------ ----------------- ----------- ----------- ----------   
1      OBJECT_OR_COLUMN  181575685   NULL        geometry                        
7      INDEX             37575172    1           geometry                        
7      INDEX             2121058592  1           geometry                        
1      OBJECT_OR_COLUMN  101575400   NULL        geometry     
```  
  
## <a name="remarks"></a>解説  
  
### <a name="how-to-update-impacted-objects"></a>影響を受けるオブジェクトを更新する方法  
 次の手順は、次の 6 月のサービス リリースのアップグレード後に行う必要のある修正措置を説明しています。  
  
|書|影響を受けるオブジェクト|修正措置|  
|-----------|---------------------|-----------------------|  
|1|**インデックス**|次のように、dm_db_objects_impacted_on_version_change によって識別されるインデックスを再構築**します。** 例: `ALTER INDEX ALL ON <table> REBUILD`<br />固定サーバー ロールまたは<br />`ALTER TABLE <table> REBUILD`|  
|2|**オブジェクト**|基になるテーブルの geometry および geography データを再計算した後に、dm_db_objects_impacted_on_version_change によって識別されるすべて**の**制約を再検証する必要があります。 制約の場合は、ALTER TABLE を使用して再検証します。 <br />例: <br />`ALTER TABLE <tab> WITH CHECK CHECK CONSTRAINT <constraint name>`<br />固定サーバー ロールまたは<br />`ALTER TABLE <tab> WITH CHECK CONSTRAINT ALL`|  
  
  
