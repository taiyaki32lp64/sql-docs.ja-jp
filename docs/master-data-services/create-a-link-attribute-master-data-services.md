---
title: "リンク属性 (マスター データ サービス) を作成 |Microsoft ドキュメント"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- attributes [Master Data Services], creating link attributes
- creating link attributes [Master Data Services]
ms.assetid: e6658e9c-5b08-4b8d-b556-17ec2dd041d2
caps.latest.revision: 9
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1b5c1a0c51283b981daf0df5e65740892fb830c2
ms.contentlocale: ja-jp
ms.lasthandoff: 08/02/2017

---
# <a name="create-a-link-attribute-master-data-services"></a>リンク属性を作成する (マスター データ サービス)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]でユーザーに属性値としてハイパーリンク (http://www.contoso.com など) を入力させる場合、リンク属性を作成します。  
  
> [!NOTE]  
>  ユーザーがリンク属性の値を入力するとき、文字列は **http://** で始まる必要があり、そうでないとエラーが表示されます。  
  
## <a name="prerequisites"></a>前提条件  
 この手順を実行するには  
  
-   **[システム管理]** 機能領域にアクセスする権限が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「[Administrators &#40;Master Data Services&#41; (管理者 &#40;マスター データ サービス&#41;)](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
-   属性を作成するエンティティが存在する必要があります。 詳細については、「[エンティティを作成する (マスター データ サービス)](../master-data-services/create-an-entity-master-data-services.md)」を参照してください。  
  
## <a name="attribute-information"></a>属性情報  
 作成された属性ごとに、7 列の行がグリッドに追加されます。 次の表で各列について説明します。  
  
|列|Description|  
|------------|-----------------|  
|状態|属性の状態。<br /><br /> 保存をクリックすると、![ステータスの更新のアイコン](../master-data-services/media/mds-statusicon-updating.png "ステータスの更新のアイコン")イメージ属性を更新していることを示すが表示されます。<br /><br /> 作成または属性を編集するときにエラーがある場合、![のエラー状態をアイコン](../master-data-services/media/mds-statusicon-error.png "のエラー状態をアイコン")イメージが表示されます。<br /><br /> 状態が [ok] をそれ以外の場合、および![OK ステータス アイコン](../master-data-services/media/mds-statusicon-ok.png "OK ステータス アイコン")イメージが表示されます。|  
|名前|属性名です。|  
|表示名|属性の表示名。|  
|Description|属性の説明。|  
|ピクセル幅の表示|属性の幅。|  
|種類とプロパティ|属性の種類とデータ型の情報。|  
|変更の追跡を有効化|変更の追跡に対して属性が有効になっているかどうかを指定し、グループ番号を括弧で表示します。|  
  
 属性をクリックすると、次の情報が表示されます。  
  
-   **作成者**: 属性を作成したユーザーの名前。  
  
-   **作成日時**: 属性が作成された日時。  
  
-   **更新者**: 属性を最後に更新したユーザーの名前。  
  
-   **更新日時**: 属性が最後に更新された日時。  
  
### <a name="to-create-a-link-attribute"></a>リンク属性を作成するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[システム管理]**をクリックします。  
  
2.  **[モデルの管理]** ページでグリッドからモデルを選択し、 **[エンティティ]**をクリックします。  
  
3.  **[エンティティの管理]** ページで、属性を作成するエンティティの行を選択します。  
  
4.  **[属性]**をクリックします。  
  
5.  **[属性の管理]** ページで、次のいずれかの操作を行い、 **[追加]**をクリックします。  
  
    -   属性の対象がリーフ メンバーの場合、 **[メンバーの種類]** ボックスの一覧から **[リーフ]** を選択します。  
  
    -   属性の対象が統合メンバーの場合、 **[メンバーの種類]** ボックスの一覧から **[統合]** を選択します。  
  
    -   属性の対象がコレクションの場合、 **[メンバーの種類]** ボックスの一覧から **[コレクション]** を選択します。  
  
6.  **[名前]** ボックスに属性の名前を入力します。 属性名として使用できない単語の一覧については、「[予約語 (マスター データ サービス)](../master-data-services/reserved-words-master-data-services.md)」を参照してください。  
  
7.  (省略可能) 表示名を入力し、 **[説明]** ボックスに説明を入力します。  
  
8.  **[ピクセル幅の表示]** ボックスに、 **[エクスプローラー]** グリッドに表示する属性列の幅を入力します。  
  
9. **[属性の種類]** リストから、 **[自由形式]**を選択します。  
  
10. **[データ型]** ボックスの一覧から **[リンク]**を選択します。  
  
11. **[長さ]** ボックスに、許可する文字の最大数を入力します。  
  
12. 必要に応じて、 **[変更の追跡を有効化]** を選択して、属性のグループに対する変更を追跡します。 詳細については、「[変更の追跡グループに属性を追加する方法 (マスター データ サービス)](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)」を参照してください。  
  
13. **[保存]**をクリックします。  
  
## <a name="see-also"></a>参照  
 [属性 (マスター データ サービス)](../master-data-services/attributes-master-data-services.md)   
 [属性名とデータ型 &#40; を変更します。マスター データ サービス &#41;](../master-data-services/change-an-attribute-name-and-data-type-master-data-services.md)   
 [ドメイン ベースの属性 &#40; を作成します。マスター データ サービス &#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)   
 [ファイル属性を作成する (マスター データ サービス)](../master-data-services/create-a-file-attribute-master-data-services.md)  
  
  