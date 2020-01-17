---
title: 管理者
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- administrators [Master Data Services], about administrators
- administrators [Master Data Services]
- models [Master Data Services], administrators
ms.assetid: d330aa4e-6ade-4b09-b376-1b15d6c78f7d
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 056975a05f697851d1fc0eac773c917c1f22b738
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729793"
---
# <a name="administrators-master-data-services"></a>管理者 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  この記事では、[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] の管理者の種類 (モデル管理者、エンティティ管理者、およびスーパー ユーザー) について説明します。  
  
## <a name="model-administrators"></a>モデル管理者  
 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]では、モデル管理者は、 **[モデルオブジェクト]** タブの最上位のモデルオブジェクトに割り当てられた**管理**者権限を持つユーザーです。ユーザーが特定のモデルに対する管理者権限を持っている場合、モデルの子オブジェクト (モデルオブジェクトとメンバーの両方の権限) に対する他の権限は、モデルの**管理者**権限によってより前者され、実質的に無視されます。  
  
-   ユーザーに **[エクスプローラー]** 機能領域へのアクセス権がある場合、ユーザーはこのデータ領域のすべてのマスター データを追加、削除、および更新できます。  
  
-   ユーザーに他の機能領域へのアクセス権がある場合、その機能領域で利用できるすべての管理タスクを実行できます。  
  
 各モデルには複数の管理者を含めることができます。 各ユーザーは、1 つまたは複数のモデルのモデル管理者になることができ、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] の配置内のすべてのモデルのモデル管理者になることもできます。  
  
 ユーザーをモデル管理者として構成するには、 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] を使用するかプログラムで構成します。 詳細については、「[モデル管理者を作成する (マスター データ サービス)](../master-data-services/create-a-model-administrator-master-data-services.md)」を参照してください。  
  
## <a name="entity-administrators"></a>エンティティ管理者  
 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]では、エンティティ管理者は、[モデルオブジェクト] タブのエンティティオブジェクトに割り当てられた管理者権限を持つユーザーです。ユーザーがエンティティに対する管理者権限を持っている場合、そのエンティティの子オブジェクトに対する他の権限 (モデルオブジェクトとメンバーの両方の権限) は、管理者権限によって置き換えられ、無視されます。  
  
-   ユーザーに **[エクスプローラー]** 機能領域へのアクセス権がある場合、ユーザーはこのデータ領域のすべてのマスター データを追加、削除、および更新できます。  
  
-   エンティティの変更に管理者の承認が必要な場合、エンティティ管理者は変更セットを確認してから、承認または拒否することができます。  
  
 各エンティティには複数の管理者を含めることができます。 各ユーザーは、1 つ、複数、またはすべてのエンティティのエンティティ管理者になることができます。  
  
 ユーザーをエンティティ管理者として構成するには、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] を使用するかプログラムで構成します。 詳細については、「[エンティティ管理者を作成する (マスター データ サービス)](../master-data-services/create-an-entity-administrator-master-data-services.md)」を参照してください。  
  
## <a name="master-data-services-super-user"></a>マスター データ サービスのスーパー ユーザー  
 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]では、スーパー ユーザー機能領域にユーザー権限を割り当てることができます。 スーパー ユーザー機能領域に対する権限を持つユーザーは、実質的にすべてのモデルに対する管理者権限を持ち、その他のすべての機能領域に対する権限を持ちます。 機能領域に対する権限については、「[機能領域権限について (マスター データ サービス)](../master-data-services/functional-area-permissions-master-data-services.md)」を参照してください。  
  
 既定のスーパー ユーザーは、**データベースの作成ウィザード (マスター データ サービス構成マネージャー)** を使用して [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースを作成するときに、[[管理者アカウント]](../master-data-services/create-database-wizard-master-data-services-configuration-manager.md) に指定されます。  
  
 スーパー ユーザーは、次の操作を行うことができます。  
  
-   すべての機能領域にアクセスする。  
  
-   **[エクスプローラー]** 機能領域で、全モデルのすべてのマスター データを追加、削除、および更新する。  
  
 複数のユーザーまたはユーザー グループにスーパー ユーザーの権限を割り当てることができます。  
  
## <a name="comparing-administrator-types"></a>管理者の種類の比較  
  
|管理者の種類|[説明]|  
|------------------------|-----------------|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] スーパー ユーザー|[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] で割り当てられている権限は、管理者のアクセス権に影響を与えません。<br /><br /> 明示的に割り当てられている機能領域権限、またはグループから継承した権限に基づいてスーパー ユーザーになる場合があります。<br /><br /> すべてのモデルに対するあらゆる権限が自動的に付与されます。<br /><br /> すべての機能領域に対するアクセス権が自動的に付与されます。|  
|モデル管理者|明示的に割り当てられている管理者権限、またはグループから継承した権限に基づいてモデル管理者になる場合があります。<br /><br /> アクセス権が付与された機能領域だけにアクセスできます。<br /><br /> 特定のモデルのすべてのオブジェクトおよびメンバーに対するあらゆる権限が自動的に付与されます。|  
|エンティティ管理者|明示的に割り当てられている管理者権限、またはグループから継承した権限に基づいてエンティティ管理者になる場合があります。<br /><br /> アクセス権が付与された機能領域だけにアクセスできます。<br /><br /> 特定のエンティティのすべてのオブジェクトおよびメンバーに対するあらゆる権限が自動的に付与されます。<br /><br /> エンティティの変更に承認が必要な場合、保留中の変更セットを承認できます。|  
  
## <a name="external-resources"></a>外部リソース  
 msdn.com のブログ投稿「 [Security Improvements (セキュリティの向上)](https://go.microsoft.com/fwlink/p/?LinkId=615376)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [モデル管理者を作成する (マスター データ サービス)](../master-data-services/create-a-model-administrator-master-data-services.md)   
 [マスター データ サービス データベースの作成](../master-data-services/install-windows/create-a-master-data-services-database.md)   
 [通知 (マスター データ サービス)](../master-data-services/notifications-master-data-services.md)  
  
  
