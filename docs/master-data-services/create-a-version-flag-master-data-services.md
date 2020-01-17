---
title: バージョン フラグを作成する
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- creating version flags [Master Data Services]
- version flags [Master Data Services], creating
- versions [Master Data Services], creating flags
ms.assetid: 3067e1e3-05b7-4f11-9206-c612ef4e7e42
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 25c52ac4dc179940f1a3c45fd5200cf3525c56f9
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729558"
---
# <a name="create-a-version-flag-master-data-services"></a>バージョン フラグを作成する (マスター データ サービス)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] で、バージョンに割り当てるバージョン フラグを作成します。 フラグによって、ユーザーまたはサブスクライブ システムが使用する必要があるバージョンを示すことができます。  
  
## <a name="prerequisites"></a>Prerequisites  
 この手順を実行するには  
  
-   **[バージョン管理]** 機能領域にアクセスする権限が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「[Administrators &#40;Master Data Services&#41; (管理者 &#40;マスター データ サービス&#41;)](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
-   [バージョン管理] 機能領域にアクセスする権限が必要です。 詳細については、「[機能領域権限 (マスター データ サービス)](../master-data-services/functional-area-permissions-master-data-services.md)」を参照してください。  
  
### <a name="to-create-a-version-flag"></a>バージョン フラグを作成するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[バージョン管理]** をクリックします。  
  
2.  **[バージョンの管理]** ページのメニュー バーから **[管理]** をポイントして **[フラグ]** をクリックします。  
  
3.  **[バージョン フラグの管理]** ページの **[モデル]** フィールドから、フラグを作成するモデルを選択します。  
  
4.  **[追加]** をクリックします。  
  
5.  **[名前]** ボックスに名前を入力します。  
  
6.  **[説明]** ボックスに説明を入力します。  
  
7.  **[コミット済みのバージョンのみ]** フィールドで **[True]** を選択すると、フラグは **[コミット済み]** の状態のバージョンにのみ割り当てることができます。 **[False]** を選択すると、フラグは任意の状態のバージョンに割り当てることができます。  
  
8.  **[保存]** をクリックします。  
  
## <a name="next-steps"></a>Next Steps  
  
-   [バージョンにフラグを割り当てる (マスター データ サービス)](../master-data-services/assign-a-flag-to-a-version-master-data-services.md)  
  
## <a name="see-also"></a>参照  
 [バージョン (マスター データ サービス)](../master-data-services/versions-master-data-services.md)   
 [バージョン フラグ名を変更する (マスター データ サービス)](../master-data-services/change-a-version-flag-name-master-data-services.md)  
  
  
