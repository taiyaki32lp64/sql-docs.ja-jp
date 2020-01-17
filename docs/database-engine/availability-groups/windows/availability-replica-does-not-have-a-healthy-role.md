---
title: 可用性グループのレプリカに正常なロールがない
description: Always On 可用性グループ内のレプリカに正常なロールがない理由を特定します。
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.agdashboard.arp1rolehealthy.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: ebb2c9f4-2097-4688-b4fb-8f0571047317
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 91b73682ffd7d626592193c5b729896ec3d593a2
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75241771"
---
# <a name="availability-replica-does-not-have-a-healthy-role-for-an-always-on-availability-group"></a>Always On 可用性グループの可用性レプリカに正常なロールがない
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>はじめに  
  
|||  
|-|-|  
|**ポリシー名**|可用性レプリカのロールの状態|  
|**問題点**|可用性レプリカに正常なロールがありません。|  
|**カテゴリ**|**重大**|  
|**ファセット**|可用性レプリカ|  
  
## <a name="description"></a>[説明]  
 このポリシーは、可用性レプリカのロールの状態をチェックします。 可用性レプリカのロールがプライマリでもセカンダリでもない場合、ポリシーは異常な状態です。 それ以外の場合、ポリシーは正常な状態です。  
  
> [!NOTE]  
>  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]のこのリリース向けに、TechNet Wiki の「 [可用性レプリカに正常なロールがない](https://go.microsoft.com/fwlink/p/?LinkId=220856) 」に、考えられるエラーの原因および解決方法に関する情報が紹介されています。  
  
## <a name="possible-causes"></a>考えられる原因  
 この可用性レプリカのロールが正常ではありません。 このレプリカにはプライマリ ロールもセカンダリ ロールも割り当てられていません。  
  
## <a name="possible-solution-information_still_to_come"></a>考えられる解決方法:Information_still_to_come  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn ダッシュボードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
