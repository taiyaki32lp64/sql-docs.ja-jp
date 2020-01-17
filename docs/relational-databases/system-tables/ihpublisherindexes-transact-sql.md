---
title: IHpublisherindexes (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublisherindexes
- IHpublisherindexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublisherindexes system table
ms.assetid: 6008ef89-eeb9-46dc-93a2-f7623298cf0f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 114ffee3ca13d7b5a42c3843957df0a2450b787f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990247"
---
# <a name="ihpublisherindexes-transact-sql"></a>IHpublisherindexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHpublisherindexes**システム テーブルにはから SQL Server 以外のパブリッシャー、現在のディストリビューターを使用してレプリケートされたインデックスごとに 1 行が含まれています。 このテーブルは、ディストリビューション データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publisherindex_id**|**int**|パブリッシュされたインデックスを識別します。|  
|**table_id**|**int**|テーブルを識別する[IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md)インデックスが属しています。|  
|**publisher_id**|**smallint**|SQL Server 以外のパブリッシャー、インデックスの発行元を識別します。|  
|**name**|**sysname**|パブリッシュされたインデックスの名前。|  
|**type**|**nvarchar (255)**|サポートされているインデックスの種類、 [IHindextypes](../../relational-databases/system-tables/ihindextypes-transact-sql.md)システム テーブル。|  
  
## <a name="see-also"></a>関連項目  
 [異種データベース レプリケーション](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
