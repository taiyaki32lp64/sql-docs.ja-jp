---
title: ドメイン ベースの属性を作成する (マスター データ サービス) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- domain-based attributes [Master Data Services], creating
- creating domain-based attributes [Master Data Services]
- attributes [Master Data Services], creating domain-based attributes
ms.assetid: 11c31c9f-e6cc-47b7-b76a-d691f84c93c6
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: f0760ef2d2a29540b126235d6328af1fbfad39ce
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65483427"
---
# <a name="create-a-domain-based-attribute-master-data-services"></a>ドメイン ベースの属性を作成する (マスター データ サービス)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]でドメイン ベースの属性を作成して、属性の値にエンティティのメンバーを設定します。  
  
## <a name="prerequisites"></a>前提条件  
 この手順を実行するには  
  
-   **[システム管理]** 機能領域にアクセスする権限が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「 [管理者 &#40;マスター データ サービス&#41;](administrators-master-data-services.md)にアクセスすることなくグループに対してユーザーの追加または削除を行うことができます。  
  
-   属性値のソースとして使用する 1 つのエンティティが存在する必要があります。 たとえば、Color エンティティに基づくドメイン ベースの属性を作成するには、最初に Color エンティティを作成する必要があります。 詳細については、「[エンティティを作成する (マスター データ サービス)](../../2014/master-data-services/create-an-entity-master-data-services.md)」を参照してください。  
  
-   属性を作成するエンティティが存在する必要があります。 詳細については、「[エンティティを作成する (マスター データ サービス)](../../2014/master-data-services/create-an-entity-master-data-services.md)」を参照してください。  
  
### <a name="to-create-a-domain-based-attribute"></a>ドメイン ベースの属性を作成するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[システム管理]** をクリックします。  
  
2.  **[モデル ビュー]** ページのメニュー バーから **[管理]** をポイントして **[エンティティ]** をクリックします。  
  
3.  **[エンティティのメンテナンス]** ページの **[モデル]** ボックスの一覧からモデルを選択します。  
  
4.  属性を作成するエンティティの行を選択します。  
  
5.  **[選択したエンティティの編集]** をクリックします。  
  
6.  **[エンティティの編集]** ページで、次の手順を実行します。  
  
    -   リーフ メンバーの属性の場合は、 **[リーフ メンバー属性]** ペインで **[リーフ属性の追加]** をクリックします。  
  
    -   統合メンバーの属性の場合は、 **[統合メンバー属性]** ペインで **[統合属性の追加]** をクリックします。  
  
    -   コレクションの属性の場合は、 **[コレクション属性]** ペインで **[コレクション属性の追加]** をクリックします。  
  
7.  **属性の追加**] ページで、[、**ドメイン ベース**オプション。  
  
8.  **[名前]** ボックスに属性の名前を入力します。 この名前は、属性値のソースとして使用するエンティティの名前と同じである必要はありません。  
  
9. **[ピクセル幅の表示]** ボックスに、 **[エクスプローラー]** グリッドに表示する属性列の幅を入力します。  
  
10. **エンティティ**一覧で、属性値の設定に使用するエンティティを選択します。  
  
11. 任意。 **[変更の追跡を有効化]** を選択して、属性のグループに対する変更を追跡します。 詳細については、「[変更の追跡グループに属性を追加する方法 (マスター データ サービス)](../../2014/master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)」を参照してください。  
  
12. **[属性の保存]** をクリックします。  
  
13. **[エンティティのメンテナンス]** ページで **[エンティティの保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [ドメインベースの属性 (マスター データ サービス)](../../2014/master-data-services/domain-based-attributes-master-data-services.md)   
 [派生階層を作成する (マスター データ サービス)](../../2014/master-data-services/create-a-derived-hierarchy-master-data-services.md)   
 [属性名を変更&#40;マスター データ サービス&#41;](change-an-attribute-name-and-data-type-master-data-services.md)   
 [属性を削除する (マスター データ サービス)](../../2014/master-data-services/delete-an-attribute-master-data-services.md)  
  
  
