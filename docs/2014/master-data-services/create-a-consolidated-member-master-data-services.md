---
title: 統合メンバーを作成する (マスター データ サービス) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- creating consolidated members [Master Data Services]
- members [Master Data Services], creating consolidated members
- consolidated members [Master Data Services], creating
ms.assetid: 431ab2d2-5517-4372-9980-142b05427c08
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: f96ab2cb9c2076d36ae36d3aa3358ae4886a1b23
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65483430"
---
# <a name="create-a-consolidated-member-master-data-services"></a>統合メンバーを作成する (マスター データ サービス)
  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で明示的階層の親ノードが必要な場合、統合メンバーを作成します。 統合メンバーには、独自の属性を含めることができます。 これはグループ化のために使用されます。 次の例に示すように、統合メンバーは、その下にアカウントを持つアカウント グループに使用できます。  
  
 ![統合メンバーを MDS](../../2014/master-data-services/media/mds-consolidated-members.png "MDS の統合メンバー")  
  
## <a name="prerequisites"></a>前提条件  
 この手順を実行するには  
  
-   **[エクスプローラー]** 機能領域にアクセスする権限が必要です。  
  
-   メンバーを追加するエンティティの統合モデル オブジェクトに対する **更新** 権限が最低限必要です。  
  
### <a name="to-create-a-consolidated-member"></a>統合メンバーを作成するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] のホーム ページで、 **[モデル]** ボックスの一覧からモデルを選択します。  
  
2.  **[バージョン]** ボックスの一覧からバージョンを選択します。  
  
3.  **[エクスプローラー]** をクリックします。  
  
4.  メニュー バーの **[階層]** をポイントして、統合メンバーを追加する階層の名前をクリックします。  
  
5.  グリッドの上にある **[統合メンバー]** または **[階層内のすべての統合メンバー]** をクリックします。  
  
6.  **[追加]** をクリックします。  
  
7.  右側のペインのフィールドに入力します。  
  
8.  任意。 **[注釈]** ボックスに、メンバーを追加した理由についてのコメントを入力します。 そのメンバーにアクセスできるすべてのユーザーが、その注釈を表示できます。  
  
9. **[OK]** をクリックします。  
  
## <a name="next-steps"></a>次の手順  
  
-   [階層内のメンバーを移動&#40;マスター データ サービス&#41;](move-members-within-a-hierarchy-master-data-services.md)  
  
## <a name="see-also"></a>関連項目  
 [明示的階層を作成する (マスター データ サービス)](../../2014/master-data-services/create-an-explicit-hierarchy-master-data-services.md)   
 [リーフ メンバーを作成する &#40;マスター データ サービス&#41;](../../2014/master-data-services/create-a-leaf-member-master-data-services.md)   
 [読み込むか、ステージング処理を使用してマスター データ サービス内のメンバーを更新します。](add-update-and-delete-data-master-data-services.md)   
 [メンバー (マスター データ サービス)](../../2014/master-data-services/members-master-data-services.md)   
 [明示的階層 (マスター データ サービス)](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)  
  
  
