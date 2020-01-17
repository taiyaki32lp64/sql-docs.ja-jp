---
title: 日付属性を作成する (マスター データ サービス) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- creating date attributes [Master Data Services]
- attributes [Master Data Services], creating date attributes
ms.assetid: 22a8f1a3-b4f2-4cfa-8495-7daad5ce9d12
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 1284a15e16465962e2ce2c286bfb2897bb297622
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65483348"
---
# <a name="create-a-date-attribute-master-data-services"></a>日付属性を作成する (マスター データ サービス)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]で、ユーザーに属性値として日付を入力させる場合、日付属性を作成します。  
  
> [!NOTE]  
>  属性は DateTime という名前ですが、時間の値はサポートされていません。  
  
## <a name="prerequisites"></a>前提条件  
 この手順を実行するには  
  
-   **[システム管理]** 機能領域にアクセスする権限が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「 [管理者 &#40;マスター データ サービス&#41;](administrators-master-data-services.md)にアクセスすることなくグループに対してユーザーの追加または削除を行うことができます。  
  
-   属性を作成するエンティティが存在する必要があります。 詳細については、「[エンティティを作成する (マスター データ サービス)](../../2014/master-data-services/create-an-entity-master-data-services.md)」を参照してください。  
  
### <a name="to-create-a-date-attribute"></a>日付属性を作成するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[システム管理]** をクリックします。  
  
2.  **[モデル ビュー]** ページのメニュー バーから **[管理]** をポイントして **[エンティティ]** をクリックします。  
  
3.  **[エンティティのメンテナンス]** ページの **[モデル]** ボックスの一覧からモデルを選択します。  
  
4.  属性を作成するエンティティの行を選択します。  
  
5.  **[選択したエンティティの編集]** をクリックします。  
  
6.  **[エンティティの編集]** ページで、次の手順を実行します。  
  
    -   リーフ メンバーの属性の場合は、 **[リーフ メンバー属性]** ペインで **[リーフ属性の追加]** をクリックします。  
  
    -   統合メンバーの属性の場合は、 **[統合メンバー属性]** ペインで **[統合属性の追加]** をクリックします。  
  
    -   コレクションの属性の場合は、 **[コレクション属性]** ペインで **[コレクション属性の追加]** をクリックします。  
  
7.  **[属性の追加]** ページで **[自由形式]** オプションを選択します。  
  
8.  **[名前]** ボックスに属性の名前を入力します。 属性名として使用できない単語の一覧については、「[予約語 (マスター データ サービス)](../../2014/master-data-services/reserved-words-master-data-services.md)」を参照してください。  
  
9. **[ピクセル幅の表示]** ボックスに、 **[エクスプローラー]** グリッドに表示する属性列の幅を入力します。  
  
10. **[データ型]** ボックスの一覧の **[DateTime]** をクリックします。  
  
11. **[定型入力]** ボックスの一覧から日付の形式を選択します。  
  
12. 必要に応じて、 **[変更の追跡を有効化]** を選択して、属性のグループに対する変更を追跡します。 詳細については、「[変更の追跡グループに属性を追加する方法 (マスター データ サービス)](../../2014/master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)」を参照してください。  
  
13. **[属性の保存]** をクリックします。  
  
14. **[エンティティのメンテナンス]** ページで **[エンティティの保存]** をクリックします。  
  
## <a name="to-display-the-time-portion-of-a-datetime-value"></a>datetime 値の時刻部分を表示するには  
 ユーザー インターフェイスに datetime 値の時刻部分を表示するには、属性に対する適切な入力マスクを選択する必要があります。 Datetime 属性にそのための組み込みのマスクは存在しませんが、時刻を表示するための新しいマスクを独自に追加することはできます。 そのためには、組み込みのマスクが格納されている MDS データベースの mdm.tblList テーブルに行を追加します。 この行には、次の値が存在する必要があります。  
  
|||  
|-|-|  
|ListCode|lstInputMask|  
|ListName|[定型入力]|  
|Seq|19|  
|List Option|dd/MM/yyyy hh:mm:ss tt|  
|Option ID|19|  
|可視|1|  
|Group_ID|3|  
  
 上記の値を mdm.tblList テーブルの行に入力すると、[定型入力] リスト ボックスで "dd/MM/yyyy hh:mm:ss tt" マスクを選べるようになります。 これで、エンティティの datetime 属性列に日付と時刻を表示するためのマスクを MDS エクスプローラーで選択できます。  
  
 [定型入力] は、カスタムの .NET DateTime 書式設定文字列です。 詳しくは、「 [カスタム日時書式指定文字列](https://msdn.microsoft.com/library/8kb3ddd4\(v=vs.110\).aspx)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [属性 (マスター データ サービス)](../../2014/master-data-services/attributes-master-data-services.md)   
 [属性名を変更&#40;マスター データ サービス&#41;](change-an-attribute-name-and-data-type-master-data-services.md)   
 [ドメイン ベースの属性を作成する &#40;マスター データ サービス&#41;](../../2014/master-data-services/create-a-domain-based-attribute-master-data-services.md)   
 [ファイル属性を作成する (マスター データ サービス)](../../2014/master-data-services/create-a-file-attribute-master-data-services.md)  
  
  
