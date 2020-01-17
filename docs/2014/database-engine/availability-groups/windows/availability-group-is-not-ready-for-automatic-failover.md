---
title: 可用性グループの自動フェールオーバーの準備ができていない | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.agp3autofailover.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 28261014-342c-442a-bd89-6d04b8d4e8b7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a9a7bdca770bccaac50da1ac6a7688eabd335e20
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62791866"
---
# <a name="availability-group-is-not-ready-for-automatic-failover"></a>可用性グループの自動フェールオーバーの準備ができていない
    
## <a name="introduction"></a>概要  
  
|||  
|-|-|  
|**ポリシー名**|可用性グループの自動フェールオーバーの準備|  
|**問題**|可用性グループで自動フェールオーバーの準備ができていません。|  
|**カテゴリ**|**重大**|  
|**ファセット**|可用性グループ|  
  
## <a name="description"></a>説明  
 このポリシーは、フェールオーバーの準備が整っているセカンダリ レプリカが 1 つ以上可用性グループに存在するかどうかを確認します。 プライマリ レプリカのフェールオーバー モードが自動モードである一方で、可用性グループのセカンダリ レプリカのいずれもフェールオーバーの準備ができていない場合、ポリシーは通常とは異なる状態で、アラートが発生します。  
  
 自動フェールオーバーの準備が整っているセカンダリ レプリカが 1 つ以上存在する場合、ポリシーは正常な状態です。  
  
> [!NOTE]  
>  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]のこのリリース向けに、TechNet Wiki の「 [可用性グループの自動フェールオーバーの準備ができていない](https://go.microsoft.com/fwlink/p/?LinkId=220851) 」に、考えられるエラーの原因および解決方法に関する情報が紹介されています。  
  
## <a name="possible-causes"></a>考えられる原因  
 可用性グループの自動フェールオーバーの準備ができていません。 プライマリ レプリカは自動フェールオーバー用に構成されていますが、セカンダリ レプリカは自動フェールオーバーの準備ができていません。 自動フェールオーバー用に構成されているセカンダリ レプリカが使用できないか、そのデータ同期状態が現在 SYNCHRONIZED になっていない可能性があります。  
  
## <a name="possible-solutions"></a>考えられる解決策  
 この問題に対して考えられる解決策を次に示します。  
  
-   自動フェールオーバーとして 1 つ以上のセカンダリ レプリカが構成されていることを確認します。 自動フェールオーバーとして構成されたセカンダリ レプリカが存在しない場合は、同期コミットが設定された自動フェールオーバー ターゲットとなるようにセカンダリ レプリカの構成を更新します。  
  
-   ポリシーを使用して、データが同期状態にあり、自動フェールオーバー ターゲットが SYNCHRONIZED 状態であることを確認した後、可用性レプリカの問題を解決します。  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn ダッシュボードの使用 &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
