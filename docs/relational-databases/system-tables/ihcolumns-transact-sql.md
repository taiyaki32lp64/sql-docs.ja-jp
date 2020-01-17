---
title: IHcolumns (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHcolumns_TSQL
- IHcolumns
dev_langs:
- TSQL
helpviewer_keywords:
- IHcolumns system table
ms.assetid: 5bb027e5-5279-487b-9c33-5f402987253c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9985b0587316641955219eb5179ffd6ed07916d3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990389"
---
# <a name="ihcolumns-transact-sql"></a>IHcolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHcolumns**列がパブリッシュされた各システム テーブルに 1 つの行が含まれます。 このテーブルは基本的に SQL Server 以外のデータベース管理システム (DBMS) 間のデータ型にマップする発行されるの列のデータ型から、SQL Server 以外のパブリッシャーの表現方法の定義に使用し、SQL Server。 このテーブルは、ディストリビューション データベースに格納されます。  
  
## <a name="definition"></a>定義  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**column_id**|**int**|パブリッシュされた列を識別します。|  
|**publishercolumn_id**|**int**|パブリッシュされた列に格納されている列のメタデータを関連付けます、 [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md)システム テーブル。|  
|**name**|**sysname**|列名を指定します。|  
|**article_id**|**int**|列が所属するアーティクルを識別します。|  
|**column_ordinal**|**int**|順序に基づいた列の識別子。|  
|**mapped_type**|**tinyint**|サブスクライバーのマップ先となる列のデータ型です。|  
|**mapped_length**|**bigint**|サブスクライバーの列の長さです。|  
|**mapped_prec**|**int**|サブスクライバーの列の有効桁数。|  
|**mapped_scale**|**int**|サブスクライバーの列の小数点以下桁数。|  
|**mapped_nullable**|**bit**|サブスクライバーの列に NULL 値を受け入れるかどうかを示す、 **1** NULL 値を受け入れることを意味します。|  
  
## <a name="see-also"></a>関連項目  
 [異種データベース レプリケーション](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_articlecolumn (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sysarticlecolumns&#40;システム ビュー&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)   
 [sysarticlecolumns &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
