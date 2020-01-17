---
title: 属性値の変更に基づいてアクションを開始する
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], tracking attribute changes
- change tracking groups [Master Data Services], initiating actions
ms.assetid: 5e4402ce-31db-4774-a2a1-552335f87693
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: a83b51479aadc92941da073e5bf9f0da394691ff
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729167"
---
# <a name="initiate-actions-based-on-attribute-value-changes-master-data-services"></a>属性値の変更に基づいてアクションを開始する (マスター データ サービス)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] で、属性値に対する変更に基づいてアクションを開始するビジネス ルールを作成します。 たとえば、特定の属性値が変更されたときに、値の変更、通知の送信、または外部ワークフローの開始を行うことができます。  
  
## <a name="prerequisites"></a>Prerequisites  
 この手順を実行するには  
  
-   **[システム管理]** 機能領域にアクセスする権限が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「[Administrators &#40;Master Data Services&#41; (管理者 &#40;マスター データ サービス&#41;)](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
-   属性は、変更の追跡グループに含まれている必要があります。 詳細については、「 [Add Attributes to a Change Tracking Group &#40;Master Data Services&#41;](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md) 」を参照してください。  
  
### <a name="to-create-a-business-rule-to-initiate-actions-based-on-attribute-value-changes"></a>属性値の変更に基づいてアクションを開始するビジネス ルールを作成するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[システム管理]** をクリックします。  
  
2.  メニュー バーから **[管理]** をポイントして **[ビジネス ルール]** をクリックします。  
  
3.  **[ビジネス ルールのメンテナンス]** ページの **[モデル]** の一覧からモデルを選択します。  
  
4.  **[エンティティ]** の一覧からエンティティを選択します。  
  
5.  **[メンバーの種類]** の一覧から、適用するビジネス ルールのメンバーの種類を選択します。  
  
6.  **[属性]** の一覧で、属性を選択するか、 **[すべて]** の既定値のままにします。  
  
7.  **[ビジネス ルールの追加]** をクリックします。  
  
8.  **[選択したビジネス ルールの編集]** をクリックします。  
  
9. **[コンポーネント]** ペインで **[条件]** ノードを展開します。  
  
10. **[値の比較演算]** ノードの下で、 **[が変更されている]** を **[IF]** ペインの **[条件]** ラベルにドラッグします。  
  
11. **[条件の編集]** ペインの **[変更の追跡グループ]** ボックスに、前提条件の一部として割り当てた変更の追跡グループの数を入力します。  
  
12. **[条件の編集]** ペインの **[アイテムの保存]** をクリックします。  
  
13. **[コンポーネント]** ペインで **[アクション]** ノードを展開します。  
  
14. アクションをクリックして、 **[THEN]** ペインの **[アクション]** ラベルにドラッグします。  
  
15. **[属性]** ペインで属性をクリックして、 **[アクションの編集]** ペインの **[属性の選択]** ラベルにドラッグします。  
  
16. **[アクションの編集]** ペインで、必須の各フィールドを入力します。  
  
17. **[アクションの編集]** ペインの **[アイテムの保存]** をクリックします。  
  
18. **[戻る]** をクリックします。  
  
19. 必要に応じて、 **[ビジネス ルールのメンテナンス]** ページで、ビジネス ルールを含む行の **[名前]** 、 **[説明]** 、または **[通知]** 列のセルをダブルクリックして値を更新します。  
  
    > [!NOTE]  
    >  通知は、検証アクションを含むルールに対してのみ送信されます。  
  
20. **[ビジネス ルールのパブリッシュ]** をクリックします。  
  
21. 確認のダイアログ ボックスで **[OK]** をクリックします。 ルールの状態が **[アクティブ]** に変わります。  
  
## <a name="next-steps"></a>Next Steps  
  
-   以下のいずれかの手順でビジネス ルールをデータに適用します。  
  
    -   [ビジネス ルールに対して特定のメンバーを検証する (マスター データ サービス)](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [ビジネス ルールに対してバージョンを検証する (マスター データ サービス)](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## <a name="see-also"></a>参照  
 [変更の追跡グループに属性を追加する (マスター データ サービス)](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)   
 [ビジネス ルール (マスター データ サービス)](../master-data-services/business-rules-master-data-services.md)  
  
  
