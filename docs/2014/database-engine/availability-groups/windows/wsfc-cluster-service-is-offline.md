---
title: WSFC クラスター サービスはオフライン | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.agp1WSFCquorum.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: d502548d-ece6-4a42-9ded-2157d33e3d21
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cfab5de4cd3d171d4d8b7515e65b0a9cd117ac16
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62812900"
---
# <a name="wsfc-cluster-service-is-offline"></a>WSFC クラスター サービスはオフライン
    
## <a name="introduction"></a>概要  
  
|||  
|-|-|  
|**ポリシー名**|WSFC クラスターの状態|  
|**問題**|WSFC クラスター サービスはオフラインです。|  
|**カテゴリ**|**重大**|  
|**ファセット**|SQL Server のインスタンス|  
  
## <a name="description"></a>説明  
 このポリシーは、Windows Server フェールオーバー クラスター (WSFC) の状態をチェックします。 WSFC クラスターがオフラインであるか、強制されたクォーラムの状態である場合、ポリシーは異常な状態で、アラートが発生します。 このクラスター内でホストされているすべての可用性グループはオフラインであるか、またはディザスター リカバリー アクションが必要です。  
  
 クラスターの状態が標準のクォーラムである場合、ポリシーは正常な状態です。  
  
> [!NOTE]  
>  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]のこのリリース向けに、TechNet Wiki の「 [WSFC クラスター サービスがオフライン](https://go.microsoft.com/fwlink/p/?LinkId=220849) 」に、考えられるエラーの原因および解決方法に関する情報が紹介されています。  
  
## <a name="possible-causes"></a>考えられる原因  
 この問題は、クラスター サービスの問題や、クラスターのクォーラムの損失によって発生する場合があります。  
  
## <a name="possible-solution"></a>考えられる解決方法  
 クラスター アドミニストレーター ツールを使用して、強制クォーラムまたはディザスター リカバリー ワークフローを実行できます。 強制クォーラムまたはディザスター リカバリーを行っても問題が解決されない場合は、クラスター アドミニストレーターに問題の解決を依頼してください。 詳細については、 [オンライン ブックの「](../../../sql-server/failover-clusters/windows/force-a-wsfc-cluster-to-start-without-a-quorum.md) クォーラムを使用せずに WSFC クラスターを強制的に起動する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [AlwaysOn 可用性グループの概要&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn ダッシュボードの使用 &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
