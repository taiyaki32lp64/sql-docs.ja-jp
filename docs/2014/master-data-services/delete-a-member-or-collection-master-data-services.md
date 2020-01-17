---
title: メンバーまたはコレクションを削除する (マスター データ サービス) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- collections [Master Data Services], deleting
- leaf members [Master Data Services], deleting
- deleting members [Master Data Services]
- members [Master Data Services], deleting
- consolidated members [Master Data Services], deleting
ms.assetid: 519130a7-4226-4d71-9124-d2ee0ce7e5bd
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: f3164bca23e709fd434c6ba7850ec21179a076ef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65479712"
---
# <a name="delete-a-member-or-collection-master-data-services"></a>メンバーまたはコレクションを削除する (マスター データ サービス)
  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で、不要になったメンバーまたはコレクションを削除します。 複数のメンバーを一括で削除する場合は、代わりにステージング処理を使用します。 詳細については、次を参照してください。[非アクティブ化またはステージング処理を使用してメンバーの削除&#40;Master Data Services&#41;](add-update-and-delete-data-master-data-services.md)します。  
  
> [!NOTE]  
>  別のメンバーのドメイン ベースの属性値として使用されているメンバーは削除できません。  
  
## <a name="prerequisites"></a>前提条件  
 この手順を実行するには  
  
-   **[エクスプローラー]** 機能領域にアクセスする権限が必要です。  
  
-   メンバーの場合の最小値があります**Update**からメンバーを削除するリーフ モデル オブジェクトに対する権限。  
  
-   コレクションの場合は、削除するリーフ コレクション オブジェクトに対する **更新** 権限が最低限必要です。  
  
### <a name="to-delete-a-member-or-collection"></a>メンバーまたはコレクションを削除するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] のホーム ページで、 **[モデル]** ボックスの一覧からモデルを選択します。  
  
2.  **[バージョン]** ボックスの一覧からバージョンを選択します。  
  
3.  **[エクスプローラー]** をクリックします。  
  
4.  次の操作を実行します。  
  
    -   リーフ メンバーを削除するには、メニュー バーの **[エンティティ]** をポイントして、メンバーを含むエンティティの名前をクリックします。  
  
    -   統合メンバーを削除するには、メニュー バーの **[階層]** をポイントして、メンバーを含む階層の名前をクリックします。 階層内で、メンバーが含まれているノードをクリックします。  
  
    -   コレクションを削除するには、メニュー バーの **[コレクション]** をポイントして、コレクションを含むエンティティの名前をクリックします。  
  
5.  グリッドで、削除するメンバーまたはコレクションの行をクリックします。  
  
6.  **[メンバーの削除]** 、 **[削除]** 、または **[コレクションの削除]** をクリックします。  
  
7.  確認のダイアログ ボックスで **[OK]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [メンバーまたはコレクションを再アクティブ化する (マスター データ サービス)](../../2014/master-data-services/reactivate-a-member-or-collection-master-data-services.md)   
 [メンバー (マスター データ サービス)](../../2014/master-data-services/members-master-data-services.md)   
 [コレクション (マスター データ サービス)](../../2014/master-data-services/collections-master-data-services.md)  
  
  
