---
title: "ビジネス ルール (マスター データ サービス) に対してバージョンを検証する |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- validating versions [Master Data Services]
- validating versions [Master Data Services], about validating versions
- versions [Master Data Services], validating
- business rules [Master Data Services], applying to all members
ms.assetid: 5aee7901-6d05-41d4-8bbb-c6f26791d1df
caps.latest.revision: 8
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 036659fbe3b6cafd1272180bbd37737062ed0967
ms.contentlocale: ja-jp
ms.lasthandoff: 08/02/2017

---
# <a name="validate-a-version-against-business-rules-master-data-services"></a>ビジネス ルールに対してバージョンを検証する (マスター データ サービス)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] では、ビジネス ルールをモデル バージョンのすべてのメンバーに適用するためにバージョンが検証されます。  
  
 この手順では、 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーションを使用してデータを検証する方法について説明します。 MDS データベースの権限がある場合は、代わりにストアド プロシージャを使用することができます。 詳細については、「 [Validation Stored Procedure &#40;Master Data Services&#41;](../master-data-services/validation-stored-procedure-master-data-services.md)」を参照してください。  
  
> [!NOTE]  
>  バージョンをコミットするには、すべてのメンバーが検証に合格する必要があります。  
  
## <a name="prerequisites"></a>前提条件  
 この手順を実行するには  
  
-   **[バージョン管理]** 機能領域にアクセスする権限が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「[Administrators &#40;Master Data Services&#41; (管理者 &#40;マスター データ サービス&#41;)](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
-   バージョンの状態は、**[未処理]** または **[ロック済み]** である必要があります。  
  
-   **[バージョンの検証]** ページに **[検証成功]**以外の状態のメンバーが存在する必要があります。  
  
### <a name="to-validate-a-version"></a>バージョンを検証するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[バージョン管理]**をクリックします。  
  
2.  **[バージョンの管理]** ページのメニュー バーから **[バージョンの検証]**をクリックします。  
  
3.  **[バージョンの検証]** ページで、検証するモデルおよびバージョンを選択します。  
  
4.  **[検証]**をクリックします。  
  
5.  確認のダイアログ ボックスで **[OK]**をクリックします。  
  
    > [!NOTE]  
    >  バージョンの検証が完了すると、進行状況インジケーターが表示されなくなります。  
  
## <a name="next-steps"></a>次の手順  
  
-   [ロックのバージョンと #40 です。マスター データ サービス &#41;](../master-data-services/lock-a-version-master-data-services.md)  
  
## <a name="see-also"></a>参照  
 [検証状態 & #40 です。マスター データ サービス &#41;](../master-data-services/validation-statuses-master-data-services.md)   
 [検証ストアド プロシージャと #40 です。マスター データ サービス &#41;](../master-data-services/validation-stored-procedure-master-data-services.md)   
 [バージョンと #40 です。マスター データ サービス &#41;](../master-data-services/versions-master-data-services.md)   
 [ビジネス ルール & #40 です。マスター データ サービス &#41;](../master-data-services/business-rules-master-data-services.md)   
 [ビジネス ルール &#40; に対して特定のメンバーを検証します。マスター データ サービス &#41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
  