---
title: 属性グループを削除する
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deleting attribute groups [Master Data Services]
- attribute groups [Master Data Services], deleting
ms.assetid: f915e89b-629d-4725-aea6-a7f051978244
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 78ba8b955fe0702a5b1737c1de24426d586f9ffa
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729369"
---
# <a name="delete-an-attribute-group-master-data-services"></a>属性グループを削除する (マスター データ サービス)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] で、**の** [エクスプローラー][!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 機能領域にタブを表示する必要がなくなった属性グループを削除します。  
  
-   **注** 属性グループが存在する場合、いずれの属性グループにも属さない属性は **[エクスプローラー]** に表示されません。 属性グループが存在しない場合、すべての属性が表示されます。  
  
## <a name="prerequisites"></a>Prerequisites  
 この手順を実行するには  
  
-   **[システム管理]** 機能領域にアクセスする権限が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「[Administrators &#40;Master Data Services&#41; (管理者 &#40;マスター データ サービス&#41;)](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
### <a name="to-delete-an-attribute-group"></a>属性グループを削除するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[システム管理]** をクリックします。  
  
2.  **[モデルの管理]** ページでグリッドからモデルを選択し、 **[エンティティ]** をクリックします。  
  
3.  **[Manage Entity]** (エンティティの管理) ページで、属性グループを編集するエンティティの行をグリッドから選択します。  
  
4.  **[属性グループ]** をクリックします。  
  
5.  **[属性グループの管理]** ページで、 **[メンバーの種類]** ドロップダウン リストからメンバーの種類を選択し、削除するグループの種類に応じて **[リーフ]** 、 **[統合]** 、 **[コレクション]** を展開します。  
  
6.  削除する属性グループをクリックします。  
  
7.  **[削除]** をクリックします。  
  
8.  確認のダイアログ ボックスで **[OK]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [属性グループ (マスター データ サービス)](../master-data-services/attribute-groups-master-data-services.md)   
 [属性グループを作成する (マスター データ サービス)](../master-data-services/create-an-attribute-group-master-data-services.md)  
  
  
