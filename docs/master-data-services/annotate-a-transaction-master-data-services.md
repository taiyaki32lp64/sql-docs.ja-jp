---
title: トランザクションの注釈を設定する
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- annotations [Master Data Services], for transactions
ms.assetid: f5a6b2ca-56de-4e42-9da8-fba0ac3e8d92
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 17474c603e437dd0cb2dcfbedf5e444ba50ba3ae
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728790"
---
# <a name="annotate-a-transaction-master-data-services"></a>トランザクションの注釈を設定する (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  履歴を参照する目的でトランザクションの詳細をサポートする場合、[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] でトランザクションの注釈を設定します。  
  
> [!NOTE]  
>  注釈は削除できません。  
  
## <a name="prerequisites"></a>Prerequisites  
  
-   作成したトランザクションの注釈を設定するためには、 **[エクスプローラー]** 機能領域へのアクセス権限と、注釈を設定するモデル オブジェクトに対する **更新** 権限が最低限必要です。  
  
-   すべてのユーザーのトランザクションの注釈を設定するためには、 **[バージョン管理]** 機能領域へのアクセス権限を持っているモデル管理者である必要があります。 詳細については、「[Administrators &#40;Master Data Services&#41; (管理者 &#40;マスター データ サービス&#41;)](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
### <a name="to-annotate-a-transaction-in-explorer"></a>[エクスプローラー] でトランザクションの注釈を設定するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] のホーム ページで、 **[モデル]** ボックスの一覧からモデルを選択します。  
  
2.  **[バージョン]** ボックスの一覧からバージョンを選択します。  
  
3.  **[エクスプローラー]** をクリックします。  
  
4.  メニュー バーの **[エンティティ]** をポイントして、注釈を設定するトランザクションを持つメンバーを含むエンティティの名前をクリックします。  
  
5.  グリッドで、メンバーの行をクリックします。  
  
6.  **[トランザクションの表示]** をクリックします。  
  
7.  **[トランザクションの表示]** ダイアログ ボックスで、注釈を設定するトランザクションをクリックします。  
  
8.  ダイアログ ボックスの下部にあるボックスに、注釈を入力します。  
  
9. **[注釈の追加]** をクリックします。 **[注釈]** ペインに注釈が表示されます。  
  
### <a name="to-annotate-a-transaction-in-version-management-administrators-only"></a>[バージョン管理] でトランザクションに注釈を設定する (管理者のみ)  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] ホーム ページで、 **[バージョン管理]** をクリックします。  
  
2.  メニュー バーの **[トランザクション]** をクリックします。  
  
3.  **[トランザクション]** ペインで、注釈を設定するトランザクションのグリッド内の行をクリックします。  
  
4.  **[トランザクションの注釈]** ペインの **[注釈]** ボックスに注釈を入力します。  
  
5.  クリックして **OK**です。  
  
## <a name="see-also"></a>参照  
 [注釈 (マスター データ サービス)](../master-data-services/annotations-master-data-services.md)   
 [トランザクション (マスター データ サービス)](../master-data-services/transactions-master-data-services.md)  
  
  
