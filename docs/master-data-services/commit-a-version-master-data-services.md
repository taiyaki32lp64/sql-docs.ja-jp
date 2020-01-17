---
title: バージョンをコミットする
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- committing versions [Master Data Services]
- versions [Master Data Services], committing
ms.assetid: 6b967a39-b333-4b84-9e5f-4fb07e156826
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 0fa359de1daa844fbcce073b0c67efdd5f721b37
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728593"
---
# <a name="commit-a-version-master-data-services"></a>バージョンをコミットする (マスター データ サービス)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]でモデルのバージョンをコミットして、モデルのメンバーおよびメンバーの属性に対する変更を防止します。 コミットしたバージョンはロック解除できません。  
  
## <a name="prerequisites"></a>前提条件  
 この手順を実行するには  
  
-   **[バージョン管理]** 機能領域にアクセスする権限が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「[Administrators &#40;Master Data Services&#41; (管理者 &#40;マスター データ サービス&#41;)](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
-   バージョンのステータスは、 **[ロック済み]** である必要があります。 詳細については、「 [バージョンをロックする (マスター データ サービス)](../master-data-services/lock-a-version-master-data-services.md)」を参照してください。  
  
-   すべてのメンバーが正常に検証されている必要があります。  
  
-   [バージョン管理] 機能領域にアクセスする権限が必要です。 詳細については、「[機能領域権限 (マスター データ サービス)](../master-data-services/functional-area-permissions-master-data-services.md)」を参照してください。  
  
### <a name="to-commit-a-version"></a>バージョンをコミットするには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[バージョン管理]** をクリックします。  
  
2.  **[バージョンの管理]** ページのメニュー バーの **[バージョンの検証]** をクリックします。  
  
3.  **[バージョンの検証]** ページで、コミットするモデルおよびバージョンを選択します。  
  
4.  **[コミット]** をクリックします。  
  
5.  確認のダイアログ ボックスで **[OK]** をクリックします。  
  
## <a name="next-steps"></a>次の手順  
  
-   [バージョン フラグを作成する (マスター データ サービス)](../master-data-services/create-a-version-flag-master-data-services.md)  
  
-   [バージョンにフラグを割り当てる (マスター データ サービス)](../master-data-services/assign-a-flag-to-a-version-master-data-services.md)  
  
-   [バージョンをコピーする (マスター データ サービス)](../master-data-services/copy-a-version-master-data-services.md)  
  
## <a name="see-also"></a>参照  
 [バージョン (マスター データ サービス)](../master-data-services/versions-master-data-services.md)  
  
  
