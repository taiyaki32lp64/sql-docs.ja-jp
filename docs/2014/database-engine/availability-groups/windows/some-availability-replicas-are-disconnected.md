---
title: いくつかの可用性レプリカが切断されている | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.agp7allconnected.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: aea808be-6f0f-40c2-9aa2-a2a435ec6443
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b7393fe6d415f8b68758d75fafba91c9ab0a420c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62788417"
---
# <a name="some-availability-replicas-are-disconnected"></a>いくつかの可用性レプリカが切断されている
    
## <a name="introduction"></a>概要  
  
|||  
|-|-|  
|**ポリシー名**|可用性レプリカの接続状態|  
|**問題**|一部の可用性レプリカの接続が解除されます。|  
|**カテゴリ**|**警告**|  
|**ファセット**|可用性グループ|  
  
## <a name="description"></a>説明  
 このポリシーは、すべての可用性レプリカの接続状態をロール アップし、DISCONENCTED 状態の可用性レプリカがないか確認します。 DISCONNECTED の可用性レプリカが存在する場合、ポリシーは異常な状態です。 それ以外の場合、ポリシーは正常な状態です。  
  
> [!NOTE]  
>  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]のこのリリース向けに、TechNet Wiki の「 [Some availability replicas are disconnected (いくつかの可用性レプリカが切断されている)](https://go.microsoft.com/fwlink/p/?LinkId=220855) 」に、考えられるエラーの原因および解決方法に関する情報が紹介されています。  
  
## <a name="possible-causes"></a>考えられる原因  
 プライマリ レプリカに接続されていないセカンダリ レプリカがこの可用性グループに少なくとも 1 つ存在します。 接続状態は DISCONNECTED です。  
  
## <a name="possible-solution"></a>考えられる解決方法  
 可用性レプリカのポリシーの状態を検索条件として、DISCONNECTED 状態の可用性レプリカを探し、問題を解決してください。  
  
## <a name="see-also"></a>関連項目  
 [AlwaysOn 可用性グループの概要&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn ダッシュボードの使用 &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
