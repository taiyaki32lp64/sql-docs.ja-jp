---
title: IHpublishercolumnconstraints (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublishercolumnconstraints
- IHpublishercolumnconstraints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishercolumnconstraints system table
ms.assetid: d7a41da6-e067-430a-8da2-3f6745b8a4f3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 58ef9c5e68e7d209262ebf43891ba5c1bcc4174f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990286"
---
# <a name="ihpublishercolumnconstraints-transact-sql"></a>IHpublishercolumnconstraints (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHpublishercolumnconstraints**システム テーブル内の SQL Server 以外のパブリケーションの列をマップ、 [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md)システム テーブル内の制約、 [IHpublisherconstraints](../../relational-databases/system-tables/ihpublisherconstraints-transact-sql.md)システム テーブル。 このテーブルは、ディストリビューション データベースに格納されます。  
  
## <a name="definition"></a>定義  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publishercolumn_id**|**int**|列を識別する[IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md)を関連付けられている制約。|  
|**publisherconstraint_id**|**int**|制約[IHpublisherconstraints](../../relational-databases/system-tables/ihpublisherconstraints-transact-sql.md)列に関連付けられています。|  
|**indid**|**int**|パブリッシュされたテーブルの列の位置を示します。|  
  
## <a name="see-also"></a>関連項目  
 [異種データベース レプリケーション](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [レプリケーション テーブル &#40; Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
