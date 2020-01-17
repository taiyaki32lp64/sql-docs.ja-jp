---
title: 変更の追跡グループに属性を追加する (マスター データ サービス) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- change tracking groups [Master Data Services]
- attributes [Master Data Services], change tracking groups
- change tracking groups [Master Data Services], adding attributes
ms.assetid: e153eb5f-70ca-4c6f-89d8-1f937ed3917d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 8e700942f9cebc08241cf4e159dceedc7d515a94
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65480124"
---
# <a name="add-attributes-to-a-change-tracking-group-master-data-services"></a>変更の追跡グループに属性を追加する (マスター データ サービス)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]で属性の値に対する変更を追跡する場合、変更の追跡グループに属性を追加します。  
  
> [!NOTE]  
>  変更の追跡グループに属性を追加した後に属性の値が変更されると、属性は [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースで変更済みとしてフラグが付けられます。 変更に基づいてアクションを実行するビジネス ルールを作成します。  
  
## <a name="prerequisites"></a>前提条件  
 この手順を実行するには  
  
-   **[システム管理]** 機能領域にアクセスする権限が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「 [管理者 &#40;マスター データ サービス&#41;](administrators-master-data-services.md)にアクセスすることなくグループに対してユーザーの追加または削除を行うことができます。  
  
-   変更の追跡グループに追加する属性が存在する必要があります。 詳細については、「[テキスト属性を作成する (マスター データ サービス)](../../2014/master-data-services/create-a-text-attribute-master-data-services.md)」を参照してください。  
  
### <a name="to-add-attributes-to-a-change-tracking-group"></a>属性を変更の追跡グループに追加するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[システム管理]** をクリックします。  
  
2.  **モデル エクスプ ローラー**  ページで、ポイントして、メニュー バーから**管理** をクリック**エンティティ**します。  
  
3.  **[エンティティのメンテナンス]** ページの **[モデル]** ボックスの一覧からモデルを選択します。  
  
4.  属性値を追跡するエンティティの行を選択します。  
  
5.  **[選択したエンティティの編集]** をクリックします。  
  
6.  **[エンティティの編集]** ページで、次の手順を実行します。  
  
    -   リーフ メンバーの属性がの場合、**属性のリーフ**ウィンドウで、属性を選択し、をクリックして**リーフ属性の編集**します。  
  
    -   統合メンバーの属性がの場合、**統合属性**ウィンドウで、属性を選択し、をクリックして**統合属性の編集**します。  
  
    -   コレクションの属性がの場合、**コレクション属性**ウィンドウで、属性を選択し、をクリックして**コレクション属性の編集**します。  
  
7.  **[変更の追跡の有効化]** チェック ボックスをオンにします。  
  
8.  **[変更の追跡グループ]** ボックスにグループの番号を入力します。  
  
9. **[属性の保存]** をクリックします。  
  
10. **[エンティティのメンテナンス]** ページで **[エンティティの保存]** をクリックします。  
  
11. グループに含めるすべての属性に対して、この手順を繰り返します。 グループ内の各属性に対して同じ変更の追跡グループの番号を使用します。  
  
## <a name="next-steps"></a>次の手順  
  
-   [属性値の変更に基づいてアクションを開始する (マスター データ サービス)](../../2014/master-data-services/initiate-actions-based-on-attribute-value-changes-master-data-services.md)  
  
## <a name="see-also"></a>参照  
 [テキスト属性を作成する (マスター データ サービス)](../../2014/master-data-services/create-a-text-attribute-master-data-services.md)   
 [ドメイン ベースの属性を作成する (マスター データ サービス)](../../2014/master-data-services/create-a-domain-based-attribute-master-data-services.md)  
  
  
