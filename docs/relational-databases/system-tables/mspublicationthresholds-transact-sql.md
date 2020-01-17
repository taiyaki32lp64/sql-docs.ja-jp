---
title: MSpublicationthresholds (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- mspublicationthresholds
- mspublicationthresholds_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpublicationthresholds system table
ms.assetid: 9da3879f-b1f4-4ab4-abd4-a9a8ac395eba
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2bf5659dc8a5a440b764b3264556359205646d75
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088497"
---
# <a name="mspublicationthresholds-transact-sql"></a>MSpublicationthresholds (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSpublicationthresholds**テーブルが監視されている各閾値に対して 1 つの行で、パブリケーションに対してレプリケーションのパフォーマンス メトリックを追跡するために使用します。 このテーブルは、ディストリビューション データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publication_id**|**int**|しきい値が設定されていないパブリケーションを識別します。|  
|**metric_id**|**int**|定義されている監視対象のレプリケーション パフォーマンス基準を識別、 [MSreplmonthresholdmetrics](../../relational-databases/system-tables/msreplmonthresholdmetrics-transact-sql.md)システム テーブル。|  
|**value**|**sql_variant**|監視対象のメトリックのしきい値の値。|  
|**shouldalert**|**bit**|値**1**メトリックが、定義されたしきい値を超えた場合にアラートを生成することを示します。|  
|**isenabled**|**bit**|値**1**このレプリケーションのパフォーマンス メトリックの監視が有効になっていることを示します。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
