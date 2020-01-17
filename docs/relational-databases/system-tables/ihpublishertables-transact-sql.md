---
title: IHpublishertables (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublishertables
- IHpublishertables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishertables system table
ms.assetid: 7d16ac39-633a-4fe2-8f22-1d9afc191ee9
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9a75e78c8423b925ca2dfc617cbbae7e4bdcc11d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990155"
---
# <a name="ihpublishertables-transact-sql"></a>IHpublishertables (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHpublishertables**システム テーブルは、パブリッシャー側で格納されているメタデータを表します。 このテーブルには、1 行から、SQL Server 以外のパブリッシャー、現在のディストリビューターを使用してパブリッシュされた各ソース テーブルのデータが含まれています。 このテーブルは、ディストリビューション データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|パブリッシュされたテーブルを識別します。|  
|**publisher_id**|**smallint**|-SQL Server 以外のパブリッシャーのテーブルのパブリッシュされるを識別します。|  
|**name**|**sysname**|パブリッシュされたテーブルの名前。|  
|**owner**|**sysname**|テーブルの所有者。|  
  
## <a name="see-also"></a>関連項目  
 [異種データベース レプリケーション](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [レプリケーション テーブル &#40;Transact-SQL&#41;。](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
