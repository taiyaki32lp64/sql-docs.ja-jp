---
title: 数値属性を作成する (マスター データ サービス) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [Master Data Services], creating number attributes
- creating number attributes [Master Data Services]
ms.assetid: c0dbb6d8-ba78-485a-a40d-6d5cb7e75d0a
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 484774165ea1997b98fc9dc0919f5be7450dd4c7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65483362"
---
# <a name="create-a-numeric-attribute-master-data-services"></a>数値属性を作成する (マスター データ サービス)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]で、ユーザーにより属性値として数値が入力される場合は、数値属性を作成します。  
  
> [!NOTE]  
>  数値属性には制限があります。 詳細については、「[ドメインベースの属性 (マスター データ サービス)](attributes-master-data-services.md)」を参照してください。  
  
## <a name="prerequisites"></a>前提条件  
 この手順を実行するには  
  
-   **[システム管理]** 機能領域にアクセスする権限が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「 [管理者 &#40;マスター データ サービス&#41;](../../2014/master-data-services/administrators-master-data-services.md)にアクセスすることなくグループに対してユーザーの追加または削除を行うことができます。  
  
-   属性を作成するエンティティが存在する必要があります。 詳細については、「[エンティティを作成する (マスター データ サービス)](../../2014/master-data-services/create-an-entity-master-data-services.md)」を参照してください。  
  
### <a name="to-create-a-numeric-attribute"></a>数値属性を作成するには  
  
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
  
10. **[データ型]** ボックスの一覧から **[Number]** を選択します。  
  
11. **[10 進]** ボックスに、小数点の後に入力できる数字の桁数を入力します。  
  
12. **定型入力**一覧で、負の数値の形式を選択します。  
  
13. 必要に応じて、 **[変更の追跡を有効化]** を選択して、属性のグループに対する変更を追跡します。 詳細については、「 [変更の追跡グループに属性を追加する &#40;マスター データ サービス&#41;](../../2014/master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md) 」を参照してください。  
  
14. **[属性の保存]** をクリックします。  
  
15. **[エンティティのメンテナンス]** ページで **[エンティティの保存]** をクリックします。  
  
## <a name="see-also"></a>関連項目  
 [属性 (マスター データ サービス)](attributes-master-data-services.md)   
 [属性名を変更&#40;マスター データ サービス&#41;](change-an-attribute-name-and-data-type-master-data-services.md)   
 [ドメイン ベースの属性を作成する &#40;マスター データ サービス&#41;](../../2014/master-data-services/create-a-domain-based-attribute-master-data-services.md)   
 [ファイル属性を作成する (マスター データ サービス)](../../2014/master-data-services/create-a-file-attribute-master-data-services.md)  
  
  
