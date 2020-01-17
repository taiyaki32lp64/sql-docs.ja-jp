---
title: 階層 (マスター データ サービス) 内のメンバーの移動 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- hierarchies [Master Data Services], moving members
- explicit hierarchies, moving members
- derived hierarchies, moving members
- members [Master Data Services], moving
ms.assetid: 049c9a15-89c1-478c-8438-028fffc9e187
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 58b39d2dc660fd51d1ba21308ff056874a239731
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66054088"
---
# <a name="move-members-within-a-hierarchy-master-data-services"></a>階層内のメンバーを移動する (マスター データ サービス)
  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で、階層内のメンバーを移動してその場所または親割り当てを変更します。  
  
## <a name="prerequisites"></a>前提条件  
 この手順を実行するには  
  
-   **[エクスプローラー]** 機能領域にアクセスする権限が必要です。  
  
-   明示的階層の場合の最小値があります**Update**エンティティへのアクセスを許可します。  
  
-   派生階層での最小値があります**Update**モデルを任意のドメイン ベースの属性を階層内で使用します。  
  
### <a name="to-move-members-within-a-hierarchy"></a>階層内のメンバーを移動するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] のホーム ページで、 **[モデル]** ボックスの一覧からモデルを選択します。  
  
2.  **[バージョン]** ボックスの一覧からバージョンを選択します。  
  
3.  **[エクスプローラー]** をクリックします。  
  
4.  ポイントして、メニュー バーから**階層**クリック*hierarchy_name*します。  
  
5.  **階層**ペイン、階層がツリー構造で表示される場所を移動する各メンバーのチェック ボックスをクリックします。  
  
6.  上部にある、**階層**ウィンドウで、をクリックして**切り取り**します。  
  
7.  **階層**ウィンドウにメンバーを移動するメンバーのチェック ボックスをクリックします。  
  
8.  クリックして**貼り付け**します。  
  
    > [!NOTE]  
    >  派生階層では、メンバーは同じレベルにのみ移動できます。 また、メンバーの並べ替え順序は変更できません。  
  
## <a name="see-also"></a>参照  
 [ステージング処理を使用して明示的階層メンバーの移動&#40;マスター データ サービス&#41;](add-update-and-delete-data-master-data-services.md)   
 [派生階層 (マスター データ サービス)](../../2014/master-data-services/derived-hierarchies-master-data-services.md)   
 [明示的階層 (マスター データ サービス)](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)  
  
  
