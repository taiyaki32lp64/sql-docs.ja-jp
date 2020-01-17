---
title: '[メンテナンス プラン] ([サーバー]) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.maint.servers.f1
- sql13.swb.maint.maintplanproperties.server.f1
ms.assetid: ac24d1a8-dd2f-4162-b804-c0df1fc1e61d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: aaad5af180ff1275dc6e95bb1cc5687487a22fb4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68115665"
---
# <a name="maintenance-plan-servers"></a>[メンテナンス プラン] \([サーバー])
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **[サーバー]** ダイアログ ボックスでは、メンテナンス プランを実行するサーバーを選択します。  
  
 1 台のマスター サーバーと 1 台以上のターゲット サーバーで構成されたマルチサーバー環境は、マルチサーバー メンテナンス プランを作成するように構成する必要があります。 マルチサーバー メンテナンス プランでは、ローカル サーバーをマスター サーバーとして構成する必要があります。 マルチサーバー環境では、" **(local)** " マスター サーバーと対応するすべてのターゲット サーバーがこのダイアログ ボックスに表示されます。 ローカル サーバーに対して 1 つの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブが作成されます。 このジョブが有効かどうかは、" **(local)** " サーバーを選択するかどうかによって決まります。 ターゲット サーバーを選択すると、マルチサーバー ジョブが作成され、選択した各ターゲット サーバーにダウンロードされます。 ターゲット サーバーを選択しない場合、マルチサーバー ジョブは削除されます。  
  
## <a name="see-also"></a>参照  
 [メンテナンス プラン](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [マルチサーバー環境の作成](../../ssms/agent/create-a-multiserver-environment.md)   
 [マスター サーバーの作成](../../ssms/agent/make-a-master-server.md)   
 [ターゲット サーバーの作成](../../ssms/agent/make-a-target-server.md)  
  
  
