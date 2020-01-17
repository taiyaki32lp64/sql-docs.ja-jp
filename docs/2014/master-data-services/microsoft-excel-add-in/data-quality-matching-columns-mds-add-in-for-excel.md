---
title: データ品質照合の列 (Excel 用 MDS アドイン) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: f683fdc6-0d4c-4793-8143-567616cb2094
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: ecbbaba1441fa150daaecbfcbc7cbdf65636de55
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65482639"
---
# <a name="data-quality-matching-columns-mds-add-in-for-excel"></a>データ品質照合の列 (Excel 用 MDS アドイン)
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]でデータを照合した後、リボンの **[データ品質]** グループの **[詳細の表示]** をクリックすると照合の詳細が含まれる列を表示できます。  
  
 次の表に、データの照合時に表示される列を示します。  
  
|名前|説明|  
|----------|-----------------|  
|**CLUSTER_ID**|類似レコードのグループ化に使用する一意識別子です。 類似するすべての行は、同じ **CLUSTER_ID**を持ちます。 **CLUSTER_ID** が行に対して表示されない場合、類似レコードが見つかっていません。|  
|**RECORD_ID**|レコードの識別に使用する一意識別子です。 MDS リポジトリに格納されているコード値と同様に、レコードの識別に使用される値です。 照合が実行されるたびに自動的に生成されます。|  
|**PIVOT_MARK**|他のレコードと比較される任意のレコードで、スコアの値はありません。|  
|**SCORE**|グループ内のレコードがピボット レコードとどの程度類似しているかを表します。 このスコアは DQS によって決定されます。 スコアが表示されない場合、そのレコードは他のレコードのピボットであるか、照合が見つかりませんでした。|  
  
## <a name="see-also"></a>参照  
 [Excel 用 MDS アドインでのデータ品質照合](data-quality-matching-in-the-mds-add-in-for-excel.md)   
 [類似データの照合 (Excel 用 MDS アドイン)](match-similar-data-mds-add-in-for-excel.md)   
 [データ照合](../../data-quality-services/data-matching.md)  
  
  
