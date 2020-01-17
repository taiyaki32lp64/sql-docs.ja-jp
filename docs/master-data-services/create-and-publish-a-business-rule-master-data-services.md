---
title: ビジネス ルールを作成しパブリッシュする
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], creating
- creating business rules [Master Data Services]
ms.assetid: 6961d636-4d69-468e-81f7-8d0be6a4a039
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: e8deee97bd80404df5851f0845aa02b51bfe0cfc
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729445"
---
# <a name="create-and-publish-a-business-rule-master-data-services"></a>ビジネス ルールを作成しパブリッシュする (マスター データ サービス)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]で、マスター データの精度を保証するためにビジネス ルールを作成します。 ルールを作成した後、データに適用する前に、そのルールをパブリッシュする必要があります。  
  
## <a name="prerequisites"></a>Prerequisites  
 この手順を実行するには  
  
-   **[システム管理]** 機能領域にアクセスする権限が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「[Administrators &#40;Master Data Services&#41; (管理者 &#40;マスター データ サービス&#41;)](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
### <a name="to-create-and-publish-a-business-rule"></a>ビジネス ルールを作成してパブリッシュするには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[システム管理]** をクリックします。  
  
2.  メニュー バーから **[管理]** をポイントして **[ビジネス ルール]** をクリックします。  
  
3.  **[ビジネス ルール]** ページの **[モデル]** ドロップダウン リストから、モデルを選択します。  
  
4.  **[エンティティ]** ドロップダウン リストから、エンティティを選択します。  
  
5.  **[メンバーの種類]** ボックスの一覧から、適用するビジネス ルールのメンバーの種類を選択します。  
  
6.  **[追加]** をクリックします。  
  
7.  **[名前]** ボックスにビジネス ルールの名前を入力します。  
  
8.  必要に応じて、 **[説明]** フィールドに、ビジネス ルールの説明を入力します。  
  
9. 必要に応じて、 **[通知を送信する]** オプションをオンにして、ドロップダウン リストから、電子メール通知を送信するユーザーまたはグループを選択します。  
  
    > [!NOTE]  
    >  通知は、検証アクションを含むルールに対してのみ送信されます。  
  
10. **If** ブロックの下で **[追加]** をクリックします。 パネルが表示されます。  
  
11. **[属性]** ドロップダウン リストから、属性を選択します。  
  
12. **[演算子]** ドロップダウン リストから、条件を選択します。  
  
13. すべての必須フィールドに入力します。  
  
14. **[保存]** ボタンをクリックします。 新しい行が **If** グリッドに追加されます。  
  
    > [!TIP]  
    >  ビジネス ルールからアイテムを削除するには、各項目を右クリックして **[削除]** をクリックします。  
  
15. オプションで、ビジネス ルールに複数の条件を追加します。 詳細については、「[ビジネス ルールに複数の条件を追加する (マスター データ サービス)](../master-data-services/add-multiple-conditions-to-a-business-rule-master-data-services.md)」を参照してください。  
  
16. **Then** ブロックの下で **[追加]** をクリックします。 パネルが表示されます。  
  
17. **[属性]** ドロップダウン リストから、属性を選択します。  
  
18. **[演算子]** ドロップダウン リストから、アクションを選択します。  
  
19. すべての必須フィールドに入力します。  
  
20. **[保存]** をクリックします。 新しい行が **Then** グリッドに追加されます。  
  
21. 必要に応じて **Else** アクションを追加するには、次の手順を実行します。  
  
    1.  **Else** ブロックの下で **[追加]** をクリックします。 パネルが表示されます。  
  
    2.  **[属性]** ドロップダウン リストから、属性を選択します。  
  
    3.  **[演算子]** ドロップダウン リストから、アクションを選択します。  
  
    4.  すべての必須フィールドに入力します。  
  
    5.  **[保存]** をクリックします。 新しい行が **Else** グリッドに追加されます。  
  
22. **[保存]** をクリックします。 新しい行がビジネス ルール グリッドに追加されます。  
  
23. **[すべてパブリッシュ]** をクリックします。  
  
24. 確認のダイアログ ボックスで **[OK]** をクリックします。 **[ビジネス ルールの状態]** 列の値は **[アクティブ]** です。  
  
## <a name="grid-columns"></a>グリッド列  
 作成されたビジネス ルールごとに、6 列の行がグリッドに追加されます。 次の列が追加されます。  
  
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|[状態]|**[保存]** をクリックすると、ビジネス ルールが更新中であることを示す次のイメージが表示されます。<br /><br /> ![mds_BR_refresh](../master-data-services/media/mds-br-refresh.png "mds_BR_refresh ")<br /><br /> ビジネス ルールの作成または編集中にエラーが発生すると、次のイメージが表示されます。<br /><br /> ![mds_br_error](../master-data-services/media/mds-br-error.png "mds_br_error ")<br /><br /> 適切な状態の場合は、次のイメージが表示されます。<br /><br /> ![mds_BR_success](../master-data-services/media/mds-br-success.png "mds_BR_success ")|  
|[オブジェクト名]|ビジネス ルール名。|  
|[説明]|ビジネス ルールの説明。|  
|[ビジネス ルールの状態]|次のビジネス ルールの状態のいずれか: ルール未定義、アクティブ、除外、保留中の変更、保留中の実行、保留中の削除。|  
|除外|ビジネス ルールを除外するかどうかを指定します。|  
|Notification|電子メール通知を送信するユーザーまたはグループを指定します。|  
  
## <a name="next-steps"></a>Next Steps  
  
-   以下のいずれかの手順でビジネス ルールをデータに適用します。  
  
    -   [ビジネス ルールに対して特定のメンバーを検証する (マスター データ サービス)](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [ビジネス ルールに対してバージョンを検証する (マスター データ サービス)](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## <a name="see-also"></a>参照  
 [通知を送信するようにビジネス ルールを構成する (マスター データ サービス)](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)   
 [ビジネス ルールの名前を変更する (マスター データ サービス)](../master-data-services/change-a-business-rule-name-master-data-services.md)   
 [ビジネス ルールに複数の条件を追加する (マスター データ サービス)](../master-data-services/add-multiple-conditions-to-a-business-rule-master-data-services.md)  
  
  
