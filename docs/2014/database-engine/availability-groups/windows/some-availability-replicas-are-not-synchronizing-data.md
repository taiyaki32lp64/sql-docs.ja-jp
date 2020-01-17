---
title: 一部の可用性レプリカでデータが同期されない | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.agp4synchronizing.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 3db6a569-e942-4321-a0dd-c4ab002087c8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0fb7d422687d0bc956937b30bae261b28edb3931
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62788259"
---
# <a name="some-availability-replicas-are-not-synchronizing-data"></a>一部の可用性レプリカでデータが同期されない
    
## <a name="introduction"></a>概要  
  
|||  
|-|-|  
|**ポリシー名**|可用性レプリカのデータ同期状態|  
|**問題**|一部の可用性レプリカでデータが同期されません。|  
|**カテゴリ**|**警告**|  
|**ファセット**|可用性グループ|  
  
## <a name="description"></a>説明  
 このポリシーは、可用性グループのすべての可用性レプリカのデータ同期状態をロール アップし、可用性レプリカの同期が稼働しているかどうかを確認します。 可用性レプリカのデータ同期状態が NOT SYNCHRONIZING の場合、ポリシーは通常とは異なる状態です。  
  
 可用性レプリカのデータ同期状態が NOT SYNCHRONIZING でない場合、ポリシーは正常な状態です。  
  
> [!NOTE]  
>  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]のこのリリース向けに、TechNet Wiki の「 [一部の可用性レプリカでデータが同期されない](https://go.microsoft.com/fwlink/p/?LinkId=220852) 」に、考えられるエラーの原因および解決方法に関する情報が紹介されています。  
  
## <a name="possible-causes"></a>考えられる原因  
 この可用性グループで、少なくとも 1 つのセカンダリ レプリカが NOT SYNCHRONIZING 同期状態であり、プライマリ レプリカからデータを受け取っていません。  
  
## <a name="possible-solution"></a>考えられる解決方法  
 可用性レプリカのポリシーの状態を検索条件として、NOT SYNCHRONIZING 状態の可用性レプリカを探し、問題を解決してください。  
  
## <a name="see-also"></a>関連項目  
 [AlwaysOn 可用性グループの概要&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn ダッシュボードの使用 &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
