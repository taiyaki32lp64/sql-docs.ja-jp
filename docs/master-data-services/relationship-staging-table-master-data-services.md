---
title: リレーションシップ ステージング テーブル
ms.custom: ''
ms.date: 04/01/2016
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- relationships staging table [Master Data Services]
- database [Master Data Services], relationships table
ms.assetid: e19b6002-67bd-4e7d-9f19-ecb455522b1a
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: dff1ab73713aed3bfb635c0399028f0c9a1a8c86
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727909"
---
# <a name="relationship-staging-table-master-data-services"></a>リレーションシップ ステージング テーブル (マスター データ サービス)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースのリレーションシップ ステージング テーブル (stg.name_Relationship) を使用して、メンバーが相互に保持するリレーションシップに基づいて、明示的階層におけるメンバーの位置を変更します。  
  
##  <a name="TableColumns"></a> テーブルの列  
 次の表は、リレーションシップ ステージング テーブルの各フィールドの用途を説明しています。  
  
|列名|[説明]|ReplTest1|  
|-----------------|-----------------|-----------|  
|**ID**|自動的に割り当てられる ID。|このフィールドには値を入力しないでください。 バッチが未処理の場合、このフィールドは空白です。|  
|**RelationshipType**|必須<br /><br /> 設定しているリレーションシップの種類。|指定できる値は次のとおりです。<br /><br /> **1**: 親<br /><br /> **2**: 兄弟 (同じレベル)|  
|**ImportStatus_ID**|必須<br /><br /> インポート処理の状態。|指定できる値は次のとおりです。<br /><br /> **0**: レコードがステージング準備済みであることを示すために指定します。<br /><br /> **1**: 自動的に割り当てられ、レコードのステージング処理が正常に完了したことを示します。<br /><br /> **2**: 自動的に割り当てられ、レコードのステージング処理に失敗したことを示します。|  
|**Batch_ID**|Web サービスでのみ必須<br /><br /> ステージング用のレコードをグループ化する、自動的に割り当てられる識別子。<br /><br /> バッチが未処理の場合、このフィールドは空白です。|バッチ内のメンバーすべてにこの識別子が割り当てられます。これは、 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] ユーザー インターフェイスの **[ID]** 列に表示されます。|  
|**BatchTag**|Web サービス以外は必須<br /><br /> バッチの一意名 (最大 50 文字)。||  
|**HierarchyName**|必須<br /><br /> 明示的階層の名前。 各統合メンバーは、1 つの階層にのみ所属することができます。||  
|**ParentCode**|必須<br /><br /> 親子リレーションシップの場合、子リーフまたは統合メンバーの親になる統合メンバーのコード。<br /><br /> 兄弟リレーションシップの場合、兄弟のいずれかのコード。||  
|**ChildCode**|必須<br /><br /> 親子リレーションシップの場合、子になる統合メンバーまたはリーフ メンバーのコード。<br /><br /> 兄弟リレーションシップの場合、兄弟のいずれかのコード。||  
|**並べ替え順序**|省略可<br /><br /> 親の下にある他のメンバーに対するメンバーの順序を示す整数。 各子メンバーは一意識別子を保持します。||  
|**ErrorCode**|エラー コードを表示します。 **ImportStatus_ID** が **2** のすべてのレコードについては、「[ステージング処理のエラー (マスター データ サービス)](../master-data-services/staging-process-errors-master-data-services.md)」を参照してください。||  
  
## <a name="see-also"></a>参照  
 [概要: テーブルからデータをインポートする (マスター データ サービス)](../master-data-services/overview-importing-data-from-tables-master-data-services.md)   
 [ステージング中に発生したエラーの表示 (マスター データ サービス)](../master-data-services/view-errors-that-occur-during-staging-master-data-services.md)   
 [ステージング処理のエラー (マスター データ サービス)](../master-data-services/staging-process-errors-master-data-services.md)  
  
  
