---
title: MSmerge_conflict_publication_article (T-sql)
description: データの収束を実現するために元に戻された、競合または行の変更があった行に関する情報を含む MSmerge_conflict_publication_article ストアドプロシージャについて説明します。
ms.custom: seo-lt-2019
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_conflict_publication_article_TSQL
- MSmerge_conflict_publication_article
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_conflict_publication_article system table
ms.assetid: dc4490b4-02d8-4dfc-98f5-0cf8de8e11be
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8d2c324f032f9cdd3206f6f2bed77fba74c2c0f5
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75322123"
---
# <a name="msmerge_conflict_publication_article-transact-sql"></a>MSmerge_conflict_publication_article (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_conflict_publication_article**テーブルには、データの収束を実現するために元に戻された、競合または行の変更が行われた行に関する情報が含まれています。 競合テーブルはパブリケーション内のレプリケートされたテーブルごとに存在し、競合テーブルの名前にパブリケーションとアーティクルの名前が付加されます。 このアーティクル固有の競合テーブルは、競合ログで使用するデータベースに保存されます。通常、これはパブリケーション データベースですが、集中型でない競合ログの場合はサブスクリプション データベースの場合もあります。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**_アーティクル\_列\_名_**|**変動**|レプリケートされたテーブルの列。 このシステム テーブルにはテーブル アーティクルの列ごとに 1 行のデータが格納されます。|  
|**rowguid**|**一意**|競合行の行識別子。|  
|**ModifiedDate**|**/**|競合が発生した時刻。|  
|**配信\_元\_データソース id**|**一意**|行変更が取り消された、または競合が失われたサブスクリプション。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーションビュー &#40;Transact-sql&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
