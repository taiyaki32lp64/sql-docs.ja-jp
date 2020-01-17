---
title: 日付属性を作成する
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- creating date attributes [Master Data Services]
- attributes [Master Data Services], creating date attributes
ms.assetid: 22a8f1a3-b4f2-4cfa-8495-7daad5ce9d12
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 8ffc7c1e901e3c93701c4e94ed62b8e70dbb7c0a
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728517"
---
# <a name="create-a-date-attribute-master-data-services"></a>日付属性を作成する (マスター データ サービス)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]で、ユーザーに属性値として日付を入力させる場合、日付属性を作成します。  
  
> [!NOTE]  
>  属性は DateTime という名前ですが、時間の値はサポートされていません。  
  
## <a name="prerequisites"></a>Prerequisites  
 この手順を実行するには  
  
-   **[システム管理]** 機能領域にアクセスする権限が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「[Administrators &#40;Master Data Services&#41; (管理者 &#40;マスター データ サービス&#41;)](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
-   属性を作成するエンティティが存在する必要があります。 詳細については、「[エンティティを作成する (マスター データ サービス)](../master-data-services/create-an-entity-master-data-services.md)」を参照してください。  
  
### <a name="to-create-a-date-attribute"></a>日付属性を作成するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[システム管理]** をクリックします。  
  
2.  **[モデルの管理]** ページでグリッドからモデルを選択し、 **[エンティティ]** をクリックします。  
  
3.  **[エンティティの管理]** ページで、属性を作成するエンティティの行を選択します。  
  
4.  **[属性]** をクリックします。  
  
5.  **[属性の管理]** ページで、次のいずれかの操作を行い、 **[追加]** をクリックします。  
  
    -   属性の対象がリーフ メンバーの場合、 **[メンバーの種類]** ボックスの一覧から **[リーフ]** を選択します。  
  
    -   属性の対象が統合メンバーの場合、 **[メンバーの種類]** ボックスの一覧から **[統合]** を選択します。  
  
    -   属性の対象がコレクションの場合、 **[メンバーの種類]** ボックスの一覧から **[コレクション]** を選択します。  
  
6.  **[名前]** ボックスに属性の名前を入力します。 属性名として使用できない単語の一覧については、「[予約語 (マスター データ サービス)](../master-data-services/reserved-words-master-data-services.md)」を参照してください。  
  
7.  (省略可能) 表示名を入力し、 **[説明]** ボックスに説明を入力します。  
  
8.  **[ピクセル幅の表示]** ボックスに、 **[エクスプローラー]** グリッドに表示する属性列の幅を入力します。  
  
9. **[属性の種類]** リストから、 **[自由形式]** を選択します。  
  
10. **[データ型]** ボックスの一覧の **[DateTime]** をクリックします。  
  
11. **[定型入力]** ボックスの一覧から日付の形式を選択します。  
  
12. 必要に応じて、 **[変更の追跡を有効化]** を選択して、属性のグループに対する変更を追跡します。 詳細については、「[変更の追跡グループに属性を追加する方法 (マスター データ サービス)](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)」を参照してください。  
  
13. **[保存]** をクリックします。  
  
## <a name="to-display-the-time-portion-of-a-datetime-value"></a>datetime 値の時刻部分を表示するには  
 ユーザー インターフェイスに datetime 値の時刻部分を表示するには、属性に対する適切な入力マスクを選択する必要があります。 Datetime 属性にそのための組み込みのマスクは存在しませんが、時刻を表示するための新しいマスクを独自に追加することはできます。 そのためには、組み込みのマスクが格納されている MDS データベースの mdm.tblList テーブルに行を追加します。 この行には、次の値が存在する必要があります。  
  
|||  
|-|-|  
|ListCode|lstInputMask|  
|ListName|[定型入力]|  
|Seq|19|  
|List Option|dd/MM/yyyy hh:mm:ss tt|  
|Option ID|19|  
|可視|@shouldalert|  
|Group_ID|3|  
  
 上記の値を mdm.tblList テーブルの行に入力すると、[定型入力] リスト ボックスで "dd/MM/yyyy hh:mm:ss tt" マスクを選べるようになります。 これで、エンティティの datetime 属性列に日付と時刻を表示するためのマスクを MDS エクスプローラーで選択できます。  
  
 [定型入力] は、カスタムの .NET DateTime 書式設定文字列です。 詳しくは、「 [カスタム日時書式指定文字列](https://msdn.microsoft.com/library/8kb3ddd4\(v=vs.110\).aspx)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [属性 (マスター データ サービス)](../master-data-services/attributes-master-data-services.md)   
 [属性名とデータ型を変更する (マスター データ サービス)](../master-data-services/change-an-attribute-name-and-data-type-master-data-services.md)   
 [ドメイン ベースの属性を作成する (マスター データ サービス)](../master-data-services/create-a-domain-based-attribute-master-data-services.md)   
 [ファイル属性を作成する (マスター データ サービス)](../master-data-services/create-a-file-attribute-master-data-services.md)  
  
  
