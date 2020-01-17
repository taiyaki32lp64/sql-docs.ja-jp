---
title: 属性を削除する
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [Master Data Services], deleting
- deleting attributes [Master Data Services]
ms.assetid: ec3e66f7-0e35-43d7-a80d-64899948ebfe
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 2d48e8c51f8151f8626e971f928a245ba6776c3e
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728334"
---
# <a name="delete-an-attribute-master-data-services"></a>属性を削除する (マスター データ サービス)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] で、属性とそれに関連付けられたすべての属性値を完全に削除するには、属性を削除します。  
  
## <a name="prerequisites"></a>Prerequisites  
 この手順を実行するには  
  
-   **[システム管理]** 機能領域にアクセスする権限が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「[Administrators &#40;Master Data Services&#41; (管理者 &#40;マスター データ サービス&#41;)](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
### <a name="to-delete-an-attribute"></a>属性を削除するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[システム管理]** をクリックします。  
  
2.  **[モデルの管理]** ページでグリッドからモデルを選択し、 **[エンティティ]** をクリックします。  
  
3.  **[エンティティの管理]** ページで、属性を作成するエンティティの行を選択します。  
  
4.  **[属性]** をクリックします。  
  
5.  **[属性の管理]** ページで、次のいずれかの操作を行います。  
  
    -   属性の対象がリーフ メンバーの場合、 **[メンバーの種類]** ボックスの一覧から **[リーフ]** を選択します。  
  
    -   属性の対象が統合メンバーの場合、 **[メンバーの種類]** ボックスの一覧から **[統合]** を選択します。  
  
    -   属性の対象がコレクションの場合、 **[メンバーの種類]** ボックスの一覧から **[コレクション]** を選択します。  
  
6.  削除する属性の行を選択します。  
  
    > [!NOTE]  
    >  Name 属性または Code 属性を削除することはできません。  
  
7.  **[削除]** をクリックします。  
  
8.  確認のダイアログ ボックスで **[OK]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [属性 (マスター データ サービス)](../master-data-services/attributes-master-data-services.md)   
 [ドメインベースの属性 (マスター データ サービス)](../master-data-services/domain-based-attributes-master-data-services.md)   
 [テキスト属性を作成する (マスター データ サービス)](../master-data-services/create-a-text-attribute-master-data-services.md)   
 [ドメイン ベースの属性を作成する (マスター データ サービス)](../master-data-services/create-a-domain-based-attribute-master-data-services.md)  
  
  
