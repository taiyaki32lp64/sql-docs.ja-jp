---
title: ビジネス ルールに対して特定のメンバーを検証する (マスター データ サービス) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- applying business rules [Master Data Services]
- business rules [Master Data Services], applying to select members
ms.assetid: 2288ef43-5392-47ea-b651-ec25e5692a14
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: edf6d73edb8c4409f82302c2cdf013f18037e4bc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65478533"
---
# <a name="validate-specific-members-against-business-rules-master-data-services"></a>ビジネス ルールに対して特定のメンバーを検証する (マスター データ サービス)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]では、ビジネス ルールに対してメンバーのサブセットを更新または検証する場合にビジネス ルールを選択的に適用します。  
  
> [!NOTE]  
>  ビジネス ルールをモデルのバージョンのすべてのメンバーに適用する場合は、「[ビジネス ルールに対してバージョンを検証する (マスター データ サービス)](validate-a-version-against-business-rules-master-data-services.md)」を参照してください。  
  
## <a name="prerequisites"></a>前提条件  
 この手順を実行するには  
  
-   **[エクスプローラー]** 機能領域にアクセスする権限が必要です。  
  
-   ビジネス ルールを適用するモデル オブジェクトに対して、 **更新** 権限が最低限必要です。  
  
### <a name="to-apply-business-rules-selectively"></a>ビジネス ルールを選択的に適用するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] のホーム ページで、 **[モデル]** ボックスの一覧からモデルを選択します。  
  
2.  **[バージョン]** ボックスの一覧からバージョンを選択します。  
  
3.  **[エクスプローラー]** をクリックします。  
  
4.  メニュー バーの **[エンティティ]** をポイントして、ルールを適用するメンバーを含むエンティティの名前をクリックします。  
  
5.  **[ビジネス ルールの適用]** をクリックします。 ビジネス ルールは、グリッドに表示されているメンバーにのみ適用されます。  
  
## <a name="see-also"></a>参照  
 [ビジネス ルールに対してバージョンを検証する (マスター データ サービス)](validate-a-version-against-business-rules-master-data-services.md)   
 [ビジネス ルール (マスター データ サービス)](../../2014/master-data-services/business-rules-master-data-services.md)  
  
  
