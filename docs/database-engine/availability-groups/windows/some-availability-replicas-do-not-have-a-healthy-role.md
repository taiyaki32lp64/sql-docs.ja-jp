---
title: いくつかの可用性レプリカが、正常なロールを持っていません | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.agdashboard.agp6allroleshealthy.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 7ec5b337-7201-4a66-a541-7560f8b18784
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ce157b3d188f7841df4f7dc626928029219c3088
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68014075"
---
# <a name="some-availability-replicas-do-not-have-a-healthy-role"></a>いくつかの可用性レプリカが、正常なロールを持っていません
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>概要  
  
|||  
|-|-|  
|**ポリシー名**|可用性レプリカのロールの状態|  
|**問題点**|一部の可用性レプリカに正常なロールがありません。|  
|**カテゴリ**|**警告**|  
|**ファセット**|可用性グループ|  
  
## <a name="description"></a>[説明]  
 このポリシーは、すべての可用性レプリカの接続状態をロール アップし、正常なロールに属していない可用性レプリカがないか確認します。 可用性レプリカがプライマリでもセカンダリでもない場合、ポリシーは通常とは異なる状態です。 それ以外の場合、ポリシーは正常な状態です。  
  
> [!NOTE]  
>  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]のこのリリース向けに、TechNet Wiki の「 [一部の可用性レプリカに正常なロールがない](https://go.microsoft.com/fwlink/p/?LinkId=220854) 」に、考えられるエラーの原因および解決方法に関する情報が紹介されています。  
  
## <a name="possible-causes"></a>考えられる原因  
 現在プライマリとセカンダリのいずれのロールも持たない可用性レプリカがこの可用性グループに少なくとも 1 つ存在します。  
  
## <a name="possible-solution"></a>考えられる解決方法  
 可用性レプリカのポリシーの状態を検索条件として、プライマリ ロールにもセカンダリ ロールにも該当しない可用性レプリカを探し、問題を解決してください。  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn ダッシュボードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
