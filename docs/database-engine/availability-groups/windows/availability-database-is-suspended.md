---
title: 可用性グループの可用性データベースの中断
description: Always On 可用性グループ内のデータベースが中断されてしまった原因の可能性を特定します。
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.agdashboard.drp1notsuspended.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 6baee70f-848c-4e86-b20d-78875c0f82cb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a7a0a6d1fa10576eab5e515031e8233af95c2d76
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67934913"
---
# <a name="availability-database-is-suspended-for-an-availability-group"></a>可用性グループの可用性データベースの中断
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>概要  
  
|||  
|-|-|  
|**ポリシー名**|可用性データベースの中断状態|  
|**問題点**|可用性データベースが中断されています。|  
|**カテゴリ**|**警告**|  
|**ファセット**|可用性データベース|  
  
## <a name="description"></a>[説明]  
 このポリシーは、セカンダリ データベース ("セカンダリ データベース レプリカ" とも呼ばれます) のデータの移動状態をチェックします。 データの移動が中断された場合、ポリシーは通常とは異なる状態です。 それ以外の場合、ポリシーは正常な状態です。  
  
> [!NOTE]  
>  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]のこのリリース向けに、TechNet Wiki の「 [可用性データベースが中断されている](https://go.microsoft.com/fwlink/p/?LinkId=220860) 」に、考えられるエラーの原因および解決方法に関する情報が紹介されています。  
  
## <a name="possible-causes"></a>考えられる原因  
 この可用性データベースでのデータ同期が中断された原因として、次の原因が考えられます。  
  
-   エラーが原因でシステムによってデータの同期が中断された。  
  
-   メンテナンスのためにデータベース管理者によってデータの同期が中断された。  
  
## <a name="possible-solution"></a>考えられる解決方法  
 データの同期を再開します。 問題が解決しない場合は、イベント ログで可用性グループを調べ、データの移動が中断された原因を分析します。  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn ダッシュボードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
