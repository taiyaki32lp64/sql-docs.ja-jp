---
title: sys.change_tracking_tables (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- change_tracking_tables_TSQL
- sys.change_tracking_tables
- change_tracking_tables
- sys.change_tracking_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- change tracking [SQL Server], sys.change_tracking_tables
- sys.change_tracking_tables
ms.assetid: 97ec69b6-0d49-4d98-82f0-d3e77ba1ad2b
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 158203b7dedfec3228821f6368c8f6c92b8041f7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68050873"
---
# <a name="change-tracking-catalog-views---syschangetrackingtables"></a>変更の追跡カタログ ビューでは、sys.change_tracking_tables
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  変更の追跡が有効な現在のデータベース内のテーブルごとに 1 行のデータを返します。  
   
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|object_id|**int**|変更ジャーナルを持つテーブルの ID。 テーブルは、変更の追跡が現在無効になっている場合でも、変更ジャーナルを持つことができます。<br /><br /> テーブル ID はデータベース内で一意です。|  
|is_track_columns_updated_on|**bit**|テーブルに対する変更の追跡の現在の状態。<br /><br /> 0 = OFF<br /><br /> 1 = ON|  
|begin_version|**bigint**|テーブルに対する変更の追跡を開始したときのデータベースのバージョン。 通常、このバージョンは変更の追跡が有効にされた日時を示します。ただし、テーブルが切り捨てられると、この値はリセットされます。|  
|cleanup_version|**bigint**|クリーンアップによって変更追跡情報が削除された可能性がある最大バージョン。|  
|min_valid_version|**bigint**|テーブルで使用できる変更追跡情報の有効な最小バージョン。<br /><br /> この行に関連付けられているテーブルから変更を取得する場合、last_sync_version には、この列に表示されるバージョンと同じ値か、それよりも大きい値を指定する必要があります。 詳細については、次を参照してください。 [CHANGE_TRACKING_MIN_VALID_VERSION &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md)します。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [CHANGE_TRACKING_MIN_VALID_VERSION &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md)   
 [変更の追跡カタログ ビュー &#40;TRANSACT-SQL&#41;](https://msdn.microsoft.com/library/6e8fd949-5560-4b34-879f-4e25aa24b183)   
 [データ変更の追跡 &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
  
