---
title: 類似データの結合 (Excel 用 MDS アドイン) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: f6fd6fc1-3569-42a5-b6cb-87a921c88f3b
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 4f4bc927b5b82402977328b592185e14286c2466
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65479004"
---
# <a name="match-similar-data-mds-add-in-for-excel"></a>類似データの照合 (Excel 用 MDS アドイン)
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]で、Data Quality Services (DQS) 機能を使用してデータ内の類似性を見つけます。  
  
 この手順を実行するには、次のどちらかの操作を実行します。  
  
-   既定の Data Quality Services ナレッジ ベースを使用します。  
  
-   独自のカスタムな DQS ナレッジ ベースと照合ポリシーを作成します。 詳細については、「 [Create a Matching Policy](../../data-quality-services/create-a-matching-policy.md)」をご参照ください。  
  
## <a name="prerequisites"></a>前提条件  
  
-   MDS によって管理されるデータが含まれているワークシートが必要です。 詳細については、次を参照してください。[を Excel に MDS からのデータの読み込み](export-data-to-excel-from-master-data-services.md)します。  
  
-   任意。 類似性をチェックする前に、MDS によって管理されるデータとその他のデータを結合することができます。 詳細については、「 [データの結合 (Excel 用 MDS アドイン)](combine-data-mds-add-in-for-excel.md)」を参照してください。  
  
### <a name="to-find-similarities-by-using-the-default-knowledge-base"></a>既定のナレッジ ベースを使用して類似性を見つけるには  
  
1.  MDS によって管理されるデータを含むワークシートで、 **[データ品質]** グループの **[データの照合]** をクリックします。  
  
2.  **[データの照合]** ダイアログ ボックスで、 **[DQS 知識ベース]** の一覧から **[DQS データ (既定値)]** を選択します。  
  
3.  照合するデータを含む各列について、ダイアログ ボックスで行を追加します。 このダイアログ ボックスのフィールドの詳細については、「 [照合ルールのパラメーターを設定する方法](../../data-quality-services/create-a-matching-policy.md#MatchingRules)」を参照してください。  
  
4.  すべての重み値の合計が 100% になったら、 **[OK]** をクリックします。  
  
### <a name="to-find-similarities-by-using-a-custom-knowledge-base"></a>カスタム ナレッジ ベースを使用して類似性を見つけるには  
  
1.  MDS によって管理されるデータを含むワークシートで、 **[データ品質]** グループの **[データの照合]** をクリックします。  
  
2.  **[DQS 知識ベース]** の一覧から、カスタム ナレッジ ベースの名前を選択します。  
  
3.  ワークシート内の各列について、DQS ドメインを選択します。  
  
4.  すべての DQS ドメインがワークシート内の列にマップされたら、 **[OK]** をクリックします。  
  
## <a name="next-steps"></a>次の手順  
  
-   類似するデータを判別するには、追加情報を表示します。 詳細については、「[データ品質照合の列 (Excel 用 MDS アドイン)](data-quality-matching-columns-mds-add-in-for-excel.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Excel 用 MDS アドインでのデータ品質照合](data-quality-matching-in-the-mds-add-in-for-excel.md)   
 [データ照合](../../data-quality-services/data-matching.md)  
  
  
