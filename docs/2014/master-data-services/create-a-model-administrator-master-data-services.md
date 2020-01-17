---
title: モデル管理者を作成する (マスター データ サービス) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- administrators [Master Data Services], creating
ms.assetid: dae17afc-3b39-490e-b51f-2d8da26d429e
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: bccf908359fa0cb75a8ae0bcfe7a601ccbfd6618
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65483403"
---
# <a name="create-a-model-administrator-master-data-services"></a>モデル管理者を作成する (マスター データ サービス)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]、モデル管理者を作成する場合、グループまたはユーザーに与える**Update** 1 つまたは複数のモデルのすべてのオブジェクトへのアクセスを許可します。  
  
> [!TIP]  
>  管理を簡素化するために、Windows グループまたはローカル グループを作成し、そのグループをモデル管理者として構成します。 また、 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]にアクセスすることなくグループに対してユーザーの追加または削除を行うことができます。  
  
## <a name="prerequisites"></a>前提条件  
 この手順を実行するには  
  
-   **[ユーザー/グループの権限]** 機能領域にアクセスするための権限が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「 [管理者 &#40;マスター データ サービス&#41;](administrators-master-data-services.md)にアクセスすることなくグループに対してユーザーの追加または削除を行うことができます。  
  
### <a name="to-create-a-model-administrator"></a>モデル管理者を作成するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[ユーザー/グループの権限]** をクリックします。  
  
2.  **[ユーザー]** または **[グループ]** ページで、編集するユーザーまたはグループの行を選択します。  
  
3.  **[選択したユーザーの編集]** をクリックします。  
  
4.  **[モデル]** タブをクリックします。  
  
5.  **[モデル]** ボックスの一覧からモデルを選択します (オプション)。  
  
6.  **[編集]** をクリックします。  
  
7.  権限を与えるモデルをクリックします。  
  
8.  メニューから、次のように選択します。 **Update**します。  
  
9. グループまたはユーザーを管理者にする各モデルについて、手順 7 と 8 を実行します。  
  
10. **[保存]** をクリックします。  
  
## <a name="remarks"></a>コメント  
 モデル オブジェクトまたは階層メンバーに他の権限を割り当てないでください。 ユーザーが管理者では不要になったとモデルを表示機能領域で以外の場合は、**エクスプ ローラー**します。  
  
 1 つの例外が発生: 場合は、ユーザーがある**Update**階層に割り当てられた権限**ルート**上、**階層メンバー**  タブで、ユーザーがモデルと見なされますが管理者です。  
  
## <a name="see-also"></a>関連項目  
 [管理者 (マスター データ サービス)](administrators-master-data-services.md)   
 [モデル オブジェクト権限を割り当てる (マスター データ サービス)](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)   
 [階層メンバーの権限を割り当てる (マスター データ サービス)](../../2014/master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [モデル オブジェクト権限 (マスター データ サービス)](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [階層メンバーの権限 (マスター データ サービス)](../../2014/master-data-services/hierarchy-member-permissions-master-data-services.md)  
  
  
