---
title: '[メンテナンス プラン] ([サーバー]) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.maint.maintplanproperties.server.f1
- sql12.swb.maint.servers.f1
ms.assetid: ac24d1a8-dd2f-4162-b804-c0df1fc1e61d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 989b2992407c4a3825d42106d848598a723a41c5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63187240"
---
# <a name="maintenance-plan-servers"></a>[メンテナンス プラン] \([サーバー])
  **[サーバー]** ダイアログ ボックスでは、メンテナンス プランを実行するサーバーを選択します。  
  
 1 台のマスター サーバーと 1 台以上のターゲット サーバーで構成されたマルチサーバー環境は、マルチサーバー メンテナンス プランを作成するように構成する必要があります。 マルチサーバー メンテナンス プランでは、ローカル サーバーをマスター サーバーとして構成する必要があります。 マルチサーバー環境では、" **(local)** " マスター サーバーと対応するすべてのターゲット サーバーがこのダイアログ ボックスに表示されます。 ローカル サーバーに対して 1 つの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブが作成されます。 このジョブが有効かどうかは、" **(local)** " サーバーを選択するかどうかによって決まります。 ターゲット サーバーを選択すると、マルチサーバー ジョブが作成され、選択した各ターゲット サーバーにダウンロードされます。 ターゲット サーバーを選択しない場合、マルチサーバー ジョブは削除されます。  
  
## <a name="see-also"></a>参照  
 [メンテナンス プラン](maintenance-plans.md)   
 [マルチサーバー環境の作成](../../ssms/agent/create-a-multiserver-environment.md)   
 [マスター サーバーの作成](../../ssms/agent/make-a-master-server.md)   
 [対象サーバーの作成](../../ssms/agent/make-a-target-server.md)  
  
  
