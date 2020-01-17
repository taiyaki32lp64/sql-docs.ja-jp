---
title: 可用性グループがオフライン
description: Always On 可用性グループがオフラインになっている理由を特定します。
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.agdashboard.agp2online.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 093c5208-bf7a-49f4-a546-72b48197cadf
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d2f9c6101be3dba631a9e0cbebdfedc3444c72d5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67991473"
---
# <a name="always-on-availability-group-is-offline"></a>Always On 可用性グループがオフライン
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>概要  
  
|||  
|-|-|  
|**ポリシー名**|可用性グループのオンライン状態|  
|**問題点**|可用性グループはオフラインです。|  
|**カテゴリ**|**重大**|  
|**ファセット**|可用性グループ|  
  
## <a name="description"></a>[説明]  
 このポリシーは、可用性グループのオンライン状態またはオフライン状態をチェックします。 可用性グループのクラスター リソースがオフライン状態である場合、または可用性グループがプライマリ レプリカを持たない場合、ポリシーは通常とは異なる状態で、アラートが発生します。  
  
 可用性グループのクラスター リソースがオンライン状態で、可用性グループがプライマリ レプリカを持つ場合、ポリシーは正常な状態です。  
  
> [!NOTE]  
>  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]のこのリリース向けに、TechNet Wiki の「 [可用性グループがオフライン](https://go.microsoft.com/fwlink/p/?LinkId=220850) 」に、考えられるエラーの原因および解決方法に関する情報が紹介されています。  
  
## <a name="possible-causes"></a>考えられる原因  
 この問題は、プライマリ レプリカをホストするサーバー インスタンスのエラー、またはオフラインになっている Windows Server フェールオーバー クラスター (WSFC) 可用性グループ リソースによって発生する可能性があります。 可用性グループがオフラインになる原因として、次のような状況が考えられます。  
  
-   可用性グループで自動フェールオーバー モードが構成されていません。 プライマリ レプリカが使用できなくなり、可用性グループ内のすべてのレプリカのロールが "解決中" になります。  
  
    -   プライマリ レプリカ インスタンス サービスがダウンしているか、または応答しません。  
  
    -   可用性グループのクラスターへの接続に問題があります。  
  
-   可用性グループで自動フェールオーバー モードが構成されていますが、正常に完了していません。  
  
    -   自動フェールオーバー中、ターゲット レプリカ上でのプライマリ準備チェックが失敗し、新しいプライマリとなるレプリカがありません。  
  
-   クラスターの可用性グループ リソースがオフラインになりました。  
  
    -   いずれかの依存クラスター リソースで重大な問題が発生し、オフラインになりました。 可用性グループのリソースは、依存リソースがオンラインになるまでオフライン状態です。  
  
    -   クラスターでの重要な問題により、可用性グループ リソースがオフになりました。  
  
-   可用性グループに対する自動、手動、または強制フェールオーバーの実行中です。  
  
## <a name="possible-solutions"></a>考えられる解決策  
 この問題に対して考えられる解決策を次に示します。  
  
-   プライマリ レプリカの SQL Server インスタンスがダウンしている場合は、サーバーを再起動した後、可用性グループが正常な状態であることを確認します。  
  
-   自動フェールオーバーが失敗していると考えられる場合は、レプリカ上のデータベースが以前の既知のプライマリ レプリカと同期されていることを確認した後、プライマリ レプリカにフェールオーバーします。 データベースが同期していない場合は、データの紛失が最小限に収まるレプリカを選択し、フェールオーバー モードに復旧します。  
  
-   SQL Server のインスタンスが正常である一方でクラスターのリソースがオフラインになっている場合は、フェールオーバー クラスター マネージャーを使用して、クラスターの正常性またはサーバー上の他のクラスターの問題を調べます。 フェールオーバー クラスター マネージャーを使用して可用性グループ リソースをオンラインにすることもできます。  
  
-   フェールオーバーが進行中の場合は、フェールオーバーが完了するのを待ちます。  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn ダッシュボードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
