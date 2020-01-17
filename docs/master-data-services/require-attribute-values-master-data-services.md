---
title: 属性値を要求する
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], requiring attribute values
- attributes [Master Data Services], requiring values
ms.assetid: a360ef13-0c34-43b8-a87e-2f5d8732d30e
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 0e4a49778b9c75c696d079549f586187b1204fd8
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728938"
---
# <a name="require-attribute-values-master-data-services"></a>属性値を要求する (マスター データ サービス)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]で、マスター データが完全であることを保証するために属性値を要求します。  
  
> [!NOTE]  
>  ドメイン ベースの属性値がないメンバーは、それらのリレーションシップに基づく派生階層に表示されません。  
  
## <a name="prerequisites"></a>Prerequisites  
 この手順を実行するには  
  
-   **[システム管理]** 機能領域にアクセスする権限が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「[Administrators &#40;Master Data Services&#41; (管理者 &#40;マスター データ サービス&#41;)](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
### <a name="to-require-attribute-values"></a>属性値を要求するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[システム管理]** をクリックします。  
  
2.  メニュー バーから **[管理]** をポイントして **[ビジネス ルール]** をクリックします。  
  
3.  **[ビジネス ルール]** ページの **[モデル]** ドロップダウン リストから、モデルを選択します。  
  
4.  **[エンティティ]** ドロップダウン リストから、エンティティを選択します。  
  
5.  **[メンバーの種類]** ボックスの一覧から、適用するビジネス ルールのメンバーの種類を選択します。  
  
6.  **[追加]** をクリックします。  
  
7.  **[名前]** ボックスにビジネス ルールの名前を入力します。  
  
8.  必要に応じて、 **[説明]** フィールドに、ビジネス ルールの説明を入力します。  
  
9. **Then** ブロックの下で **[追加]** をクリックします。 パネルが表示されます。  
  
10. **[演算子]** ボックスの一覧から、 **必要なアクション**を選択します。  
  
11. **[属性]** ドロップダウン リストから、属性を選択します。  
  
12. **[保存]** をクリックします。 新しい行が **Then** グリッドに追加されます。  
  
13. **[保存]** をクリックします。  
  
14. **[すべてパブリッシュ]** をクリックします。  
  
15. 確認のダイアログ ボックスで **[OK]** をクリックします。 **[ビジネス ルールの状態]** 列の値は **[アクティブ]** です。  
  
## <a name="next-steps"></a>Next Steps  
  
-   以下のいずれかの手順でビジネス ルールをデータに適用します。  
  
    -   [ビジネス ルールに対して特定のメンバーを検証する (マスター データ サービス)](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [ビジネス ルールに対してバージョンを検証する (マスター データ サービス)](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## <a name="see-also"></a>参照  
 [ビジネス ルール (マスター データ サービス)](../master-data-services/business-rules-master-data-services.md)   
 [派生階層 (マスター データ サービス)](../master-data-services/derived-hierarchies-master-data-services.md)  
  
  
