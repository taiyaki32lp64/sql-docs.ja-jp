---
title: IHpublishercolumns (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublishercolumns
- IHpublishercolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishercolumns system table
ms.assetid: a5347750-224c-40d9-ae12-57e7213b7db9
author: stevestein
ms.author: sstein
ms.openlocfilehash: a5e2f64294652586a87fcd25fda3c29517dc295d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990269"
---
# <a name="ihpublishercolumns-transact-sql"></a>IHpublishercolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHpublishercolumns**システム テーブルは、パブリッシャー側で格納されているメタデータを表します。 このテーブルには、1 行から SQL Server 以外のパブリッシャー、現在のディストリビューターを使用してレプリケートされた各列のデータが含まれています。 データ型情報**IHpublishercolumns**データの発行元の SQL Server データベース管理システム (DBMS) に固有です。 このテーブルは、ディストリビューション データベースに格納されます。  
  
## <a name="definition"></a>定義  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publishercolumn_id**|**int**|パブリッシュされた列を識別します。|  
|**table_id**|**int**|ソース テーブルを識別する[IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md)列が属しています。|  
|**publisher_id**|**smallint**|-SQL Server 以外のパブリッシャーの列がパブリッシュされる元を識別します。|  
|**name**|**sysname**|パブリッシュされた列の名前。|  
|**column_ordinal**|**int**|順序に基づいた列の識別子。|  
|**type**|**varchar(255)**|パブリッシャー側の基になる列の列のデータ型。|  
|**length**|**bigint**|パブリッシャー側の基になる列の長さ。|  
|**prec**|**int**|パブリッシャー側の基になる列の有効桁数。|  
|**scale**|**int**|パブリッシャー側の基になる列の小数点以下桁数。|  
|**isnullable**|**bit**|列に NULL 値を受け入れるかどうかを示す、 **1** NULL 値を受け入れることを意味します。|  
|**iscaptured**|**bit**|内の列がアーティクルでパブリッシュされていない場合でもある可能性のある列にトリガーが存在するかどうかを示します。 値**1**列に、トリガーが存在することを意味します。|  
  
## <a name="see-also"></a>関連項目  
 [異種データベース レプリケーション](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sysarticlecolumns&#40;システム ビュー&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)   
 [sysarticlecolumns &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
