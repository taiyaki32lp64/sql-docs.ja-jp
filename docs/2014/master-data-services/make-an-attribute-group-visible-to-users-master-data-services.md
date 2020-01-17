---
title: 属性グループのユーザーへの表示 (マスター データ サービス) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: b2f6cc27-dbc9-4f3f-961e-e81e76375248
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 97cc4c9955b64583571a63fa72df4663c1acd812
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65479152"
---
# <a name="make-an-attribute-group-visible-to-users-master-data-services"></a>属性グループのユーザーへの表示 (マスター データ サービス)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]で、 **[エクスプローラー]** 機能領域のグリッドの上部にタブを表示させる場合は、ユーザーまたはグループに対して属性グループを表示します。  
  
 属性グループを作成すると、作成者以外のすべてのユーザーに対して自動的に非表示に設定されます。  
  
## <a name="prerequisites"></a>前提条件  
 この手順を実行するには  
  
-   **[システム管理]** 機能領域にアクセスする権限が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「 [管理者 &#40;マスター データ サービス&#41;](administrators-master-data-services.md)にアクセスすることなくグループに対してユーザーの追加または削除を行うことができます。  
  
-   少なくとも 1 つの属性グループが必要です。 詳細については、「[属性グループを作成する (マスター データ サービス)](../../2014/master-data-services/create-an-attribute-group-master-data-services.md)」を参照してください。  
  
### <a name="to-make-an-attribute-group-visible-to-users"></a>属性グループをユーザーに表示するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[システム管理]** をクリックします。  
  
2.  **モデル ビュー**  ページで、ポイントして、メニュー バーから**管理** をクリック**属性グループ**します。  
  
3.  **[モデル]** ボックスの一覧からモデルを選択します。  
  
4.  **[エンティティ]** の一覧からエンティティを選択します。  
  
5.  展開するプラス記号をクリックします。**リーフ グループ**、**統合グループ**、または**コレクション グループ**、表示されるようにするグループの種類によって異なります。  
  
6.  プラス記号をクリックして、表示するグループを展開します。  
  
7.  いずれかをクリックして**ユーザー**または**グループ**にするかどうかをグループを表示するユーザーまたはグループに依存します。  
  
8.  クリックして**選択した項目の編集**します。  
  
9. ユーザーまたはグループをクリックして、**利用可能な**ボックス、をクリックし、**追加**矢印。 すべてを追加するには、 **[すべて追加]** 矢印をクリックします。  
  
10. **[保存]** をクリックします。  
  
## <a name="see-also"></a>関連項目  
 [属性グループ (マスター データ サービス)](../../2014/master-data-services/attribute-groups-master-data-services.md)   
 [属性グループを作成する (マスター データ サービス)](../../2014/master-data-services/create-an-attribute-group-master-data-services.md)  
  
  
