---
title: ビジネス ルールを削除する
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deleting business rules [Master Data Services]
- business rules [Master Data Services], deleting
ms.assetid: b97aa4f9-569f-451d-ad62-65b81f980299
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: d6af3aac4ac8e2a1a4026162eb6ab5f6038b5eed
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729405"
---
# <a name="delete-a-business-rule-master-data-services"></a>ビジネス ルールを削除する (マスター データ サービス)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] で、不要になったビジネス ルールを削除します。  
  
> [!NOTE]  
>  ビジネス ルールに対するデータの検証が行われないようにするには、ビジネス ルールを削除する代わりに除外することができます。 詳細については、「[ビジネス ルールを除外する (マスター データ サービス)](../master-data-services/exclude-a-business-rule-master-data-services.md)」を参照してください。  
  
## <a name="prerequisites"></a>Prerequisites  
 この手順を実行するには  
  
-   **[システム管理]** 機能領域にアクセスする権限が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「[Administrators &#40;Master Data Services&#41; (管理者 &#40;マスター データ サービス&#41;)](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
### <a name="to-delete-a-business-rule"></a>ビジネス ルールを削除するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[システム管理]** をクリックします。  
  
2.  メニュー バーから **[管理]** をポイントして **[ビジネス ルール]** をクリックします。  
  
3.  **[ビジネス ルール]** ページの **[モデル]** ドロップダウン リストから、モデルを選択します。  
  
4.  **[エンティティ]** ドロップダウン リストから、エンティティを選択します。  
  
5.  **[メンバーの種類]** ボックスの一覧から、適用するビジネス ルールのメンバーの種類を選択します。  
  
6.  グリッドで、削除するビジネス ルールの行をクリックします。  
  
7.  **[削除]** をクリックします。  
  
8.  確認のダイアログ ボックスで **[OK]** をクリックします。 **[ビジネス ルールの状態]** 列の値は **[削除の保留中]** です。  
  
9. **[すべてパブリッシュ]** をクリックします。  
  
10. 確認のダイアログ ボックスで **[OK]** をクリックします。 削除されたビジネス ルールはグリッドに表示されなくなります。  
  
## <a name="see-also"></a>参照  
 [ビジネス ルールを除外する (マスター データ サービス)](../master-data-services/exclude-a-business-rule-master-data-services.md)   
 [ビジネス ルールを作成しパブリッシュする (マスター データ サービス)](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)   
 [ビジネス ルール (マスター データ サービス)](../master-data-services/business-rules-master-data-services.md)  
  
  
