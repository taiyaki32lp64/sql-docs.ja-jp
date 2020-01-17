---
title: ビジネス ルールの適用 (Excel 用 MDS アドイン) | Microsoft Docs
ms.custom: microsoft-excel-add-in
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: cd106345-f561-4966-88d3-a69139b2bd78
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 75bbf9f18a6cbc7dd8ef78ff63e505299cf596c4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67988140"
---
# <a name="apply-business-rules-mds-add-in-for-excel"></a>ビジネス ルールの適用 (Excel 用 MDS アドイン)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] では、データを検証してデータが有効であることを確認する必要がある場合に、ビジネス ルールを適用できます。 検証に基づいて修正し、データを再度パブリッシュできます。  
  
> [!NOTE]  
>  データの検証は、データをパブリッシュするときに自動的に行われます。 詳細については、「[検証 (マスター データ サービス)](../../master-data-services/validation-master-data-services.md)」を参照してください。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 この手順を実行するには  
  
-   **[エクスプローラー]** 機能領域へのアクセス権が必要です。  
  
-   MDS によって管理されるデータが含まれているアクティブなワークシートが必要です。  
  
### <a name="to-apply-business-rules"></a>ビジネス ルールを適用するには  
  
1.  **[パブリッシュと検証]** グループの **[ルールの適用]** をクリックします。  
  
    > [!NOTE]  
    >  一度に検証されるメンバー (行) の数は、 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]の設定によって異なります。 詳細については、「 [ビジネス ルール設定](../../master-data-services/system-settings-master-data-services.md#BusinessRules)」を参照してください。  
  
2.  データがビジネス ルールに対して検証され、2 つの状態列が表示されます。 これらの列が自動的に表示されない場合は、 **[パブリッシュと検証]** グループの **[状態の表示]** をクリックして列を表示します。  
  
## <a name="see-also"></a>関連項目  
 [概要:Excel からデータをインポートする&#40;MDS アドインの Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
  
