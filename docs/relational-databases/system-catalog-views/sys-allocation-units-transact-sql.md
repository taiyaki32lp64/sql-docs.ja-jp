---
title: sys.allocation_units (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.allocation_units_TSQL
- sys.allocation_units
- allocation_units_TSQL
- allocation_units
dev_langs:
- TSQL
helpviewer_keywords:
- sys.allocation_units catalog view
ms.assetid: ec9de780-68fd-4551-b70b-2d3ab3709b3e
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 73ee5d7ac8bd512b69cc187f9860b9e7f2c38a78
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001297"
---
# <a name="sysallocationunits-transact-sql"></a>sys.allocation_units (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  データベースの各アロケーション ユニットの行が含まれています。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|allocation_unit_id|**bigint**|アロケーション ユニットの ID。 データベース内で一意です。|  
|type|**tinyint**|アロケーション ユニットの種類:<br /><br /> 0 = 削除されました。<br /><br /> 1 = 行内データ (すべてのデータ型、LOB データ型を除く)<br /><br /> 2 = ラージ オブジェクト (LOB) データ (**テキスト**、 **ntext**、**イメージ**、 **xml**、大きな値型、および CLR ユーザー定義型)<br /><br /> 3 = 行オーバーフロー データ|  
|type_desc|**nvarchar(60)**|アロケーション ユニットの種類の説明。<br /><br /> **削除**<br /><br /> **IN_ROW_DATA**<br /><br /> **LOB_DATA**<br /><br /> **ROW_OVERFLOW_DATA**|  
|container_id|**bigint**|アロケーション ユニットに関連付けられているストレージ コンテナーの ID。<br /><br /> type = 1 または 3 の場合、container_id = sys.partitions.hobt_id になります。<br /><br /> type = 2 の場合、container_id = sys.partitions.partition_id になります。<br /><br /> 0 = 遅延削除のマークされたアロケーション ユニット|  
|data_space_id|**int**|このアロケーション ユニットが存在するファイル グループの ID。|  
|total_pages|**bigint**|ページの合計数は、割り当てまたは、このアロケーション ユニットによって予約されています。|  
|used_pages|**bigint**|合計ページ数を実際に使用します。|  
|data_pages|**bigint**|使用されているページの数:<br /><br /> In-row data<br /><br /> LOB データ<br /><br /> Row-overflow data<br /><br /> <br /><br /> 内部インデックス ページとアロケーション管理ページに返される値を除くことに注意してください。|  
  
> [!NOTE]  
>  ドロップまたは大きなインデックスを再構築または削除や、大規模なテーブルを切り捨てる、[!INCLUDE[ssDE](../../includes/ssde-md.md)]トランザクションがコミットされた後に、まで、実際のページの割り当て解除と、関連するロックを延期します。 遅延された削除操作では、割り当てられた領域をすぐに解放しません。 このため、ラージ オブジェクトを削除するか切り捨てた直後に sys.allocation_units を実行して返された値は、実際に使用できるディスク領域を反映していないことがあります。  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [sys.partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
