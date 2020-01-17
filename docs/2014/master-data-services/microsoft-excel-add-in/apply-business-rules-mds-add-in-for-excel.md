---
title: ビジネス ルールの適用 (Excel 用 MDS アドイン) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: cd106345-f561-4966-88d3-a69139b2bd78
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 32819a694769092c255c4b2ed918dd8fde99362e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65482603"
---
# <a name="apply-business-rules-mds-add-in-for-excel"></a>ビジネス ルールの適用 (Excel 用 MDS アドイン)
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] では、データを検証してデータが有効であることを確認する必要がある場合に、ビジネス ルールを適用できます。 検証に基づいて修正し、データを再度パブリッシュできます。  
  
> [!NOTE]  
>  データの検証は、データをパブリッシュするときに自動的に行われます。 詳細については、「 [検証ストアド プロシージャ (マスター データ サービス)](../validation-stored-procedure-master-data-services.md)」を参照してください。  
  
## <a name="prerequisites"></a>前提条件  
 この手順を実行するには  
  
-   **[エクスプローラー]** 機能領域へのアクセス権が必要です。  
  
-   MDS によって管理されるデータが含まれているアクティブなワークシートが必要です。  
  
### <a name="to-apply-business-rules"></a>ビジネス ルールを適用するには  
  
1.  **[パブリッシュと検証]** グループの **[ルールの適用]** をクリックします。  
  
    > [!NOTE]  
    >  一度に検証されるメンバー (行) の数は、 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]の設定によって異なります。 詳細については、「 [ビジネス ルール設定](../system-settings-master-data-services.md#BusinessRules)」を参照してください。  
  
2.  データがビジネス ルールに対して検証され、2 つの状態列が表示されます。 これらの列が自動的に表示されない場合は、 **[パブリッシュと検証]** グループの **[状態の表示]** をクリックして列を表示します。  
  
## <a name="see-also"></a>参照  
 [データのパブリッシュ&#40;MDS アドインの Excel&#41;](overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
  
