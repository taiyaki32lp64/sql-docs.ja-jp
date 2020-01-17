---
title: 変更セット
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: f227c49a-ed46-4e0f-8992-83093456cf94
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 6d8c277796f743b31dfb5df349352bb6c7470421
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728621"
---
# <a name="changesets-master-data-services"></a>変更セット (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] では、エンティティに対する保留中の変更を変更セットに保存する機能をサポートします。 この機能には、2 つの使用シナリオがあります。  
  
-   **"承認が必要" がエンティティ管理者によって有効にされる場合の変更**  
  
     エンティティ管理者が、指定されたエンティティへの変更がコミットされる前に承認が必要と指定した場合、エンティティへの変更は、新しい変更セットまたは既存の変更セットに保存されてからのみ、承認のために送信することができます。  詳細については、「[承認が必要 (マスター データ サービス)](../master-data-services/approval-required-master-data-services.md)」を参照してください。  
  
     このワークフローを実行します。  
  
    1.  変更セットを作成します。 変更セットは、[開く] の状態です。 「 [Create a Changeset &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md)  
  
    2.  変更セットを適用し、いくつかの変更を変更セットに加えます。 「 [Apply and Update a Changeset &#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)  
  
    3.  承認のために、変更セットをエンティティ管理者に送信します。 変更セットは、[保留] の状態です。 「 [Commit or Submit a Changeset &#40;Master Data Services&#41;](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)  
  
    4.  エンティティ管理者は、変更セットが承認待ちをしている電子メール通知を受け取ります。 エンティティ管理者が変更セットを承認した場合、変更セットは [承認済み] の状態になります。 「 [Approve or Reject a Changeset &#40;Master Data Services&#41;](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
    5.  承認された変更セットは、自動的にコミットされます。 変更が正常にコミットされると、変更セットはコミット (committed) 状態になります。  
  
-   **ローカル ユーザーの変更**  
  
     後で使用または取得できるように、ローカルの変更を保存する必要がある場合は、変更セットを使用して保存できます。  
  
     このワークフローを実行します。  
  
    1.  変更セットを作成します。 変更セットは、[開く] の状態です。 「 [Create a Changeset &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md)  
  
    2.  変更セットを適用し、いくつかの変更を変更セットに加えます。 「 [Apply and Update a Changeset &#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)  
  
    3.  準備ができたら、変更セットをコミットします。 「 [Commit or Submit a Changeset &#40;Master Data Services&#41;](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)  
  
## <a name="see-also"></a>参照  
 [変更セットを作成する (マスター データ サービス)](../master-data-services/create-a-changeset-master-data-services.md)   
 [変更セットの適用および更新 (マスター データ サービス)](../master-data-services/apply-and-update-a-changeset-master-data-services.md)   
 [変更セットのコミットまたは送信 (マスター データ サービス)](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)   
 [変更セットの承認または拒否 (マスター データ サービス)](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)   
 [変更セットの管理 (マスター データ サービス)](../master-data-services/manage-changesets-master-data-services.md)  
  
  
