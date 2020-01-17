---
title: 可用性データベースのデータ同期状態が正常でない
description: Always On 可用性グループのデータベースのデータ同期状態が正常でない理由の考えられる原因を特定します。
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.agdashboard.arp3datasynchealthy.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 4fd003e7-808e-4b0e-b28a-47d9f2616f06
author: MashaMSFT
ms.author: mathoma
manager: erikre
ms.openlocfilehash: ff7b069ebde75185b0e500bc7052edc6e99fc927
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265349"
---
# <a name="data-synchronization-state-of-availability-database-is-not-healthy-for-an-always-on-availability-group"></a>Always On 可用性グループの可用性データベースのデータ同期状態が正常でない
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>概要  
  
|||  
|-|-|  
|**ポリシー名**|可用性データベースのデータ同期状態|  
|**問題点**|可用性データベースのデータ同期状態が正常ではありません。|  
|**カテゴリ**|**警告**|  
|**ファセット**|可用性データベース|  
  
## <a name="description"></a>[説明]  
 このポリシーは、可用性レプリカ内のすべての可用性データベース ("データベース レプリカ" とも呼ばれます) のデータ同期状態を集計します。 いずれかのデータベース レプリカが予想されるデータ同期状態ではない場合、ポリシーは通常とは異なる状態です。 それ以外の場合、ポリシーは正常な状態です。  
  
> [!NOTE]  
>  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]のこのリリース向けに、TechNet Wiki の「 [一部の可用性データベースのデータ同期状態が正常でない](https://go.microsoft.com/fwlink/p/?LinkId=220858) 」に、考えられるエラーの原因および解決方法に関する情報が紹介されています。  
  
## <a name="possible-causes"></a>考えられる原因  
 この可用性データベースのデータ同期状態が正常ではありません。 非同期コミット可用性レプリカでは、各可用性データベースは SYNCHRONIZING 状態である必要があります。 同期コミット レプリカでは、各可用性データベースは SYNCHRONIZED 状態である必要があります。  
  
## <a name="possible-solution"></a>考えられる解決方法  
 データベース レプリカ ポリシーを使用して通常とは異なるデータ同期状態のデータベース レプリカを見つけ、データベース レプリカの問題を解決します。  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn ダッシュボードの使用 &#40;SQL Server Management Studio&#41;](~/database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  


