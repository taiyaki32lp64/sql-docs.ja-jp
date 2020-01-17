---
title: 高可用性ソリューション (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- high availability [SQL Server], solutions
- Database Engine [SQL Server], availability
- database availability [SQL Server]
- availability [SQL Server]
- server availability [SQL Server]
ms.assetid: b2eda634-0f8e-4703-801b-7ba895544ff5
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 43727e0c7795fbd1f2f0c6a56693c2f06fdf4536
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63193044"
---
# <a name="high-availability-solutions-sql-server"></a>高可用性ソリューション (SQL Server)
  このトピックでは、サーバーやデータベースの可用性を向上する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の高可用性ソリューションをいくつか紹介します。 高可用性ソリューションは、ハードウェアやソフトウェアで問題が発生した場合でもその影響が現れないようにし、アプリケーションの可用性を維持しながら、ユーザーに影響するダウンタイムを最小限に抑えます。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のどのエディションで特定の高可用性ソリューションがサポートされているかについては、「[SQL Server 2014 の各エディションでサポートされる機能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)」の「高可用性 (AlwaysOn)」のセクションを参照してください。  
(#RecommendedSolutions)  
  
##  <a name="TermsAndDefinitions"></a> SQL Server の高可用性ソリューションの概要  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、サーバーやデータベースの高可用性を実現するために複数の方法が用意されています。 高可用性を実現するには以下の方法があります。  
  
 AlwaysOn フェールオーバー クラスター インスタンス  
 一部として、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] AlwaysOn 製品、AlwaysOn フェールオーバー クラスター インスタンスは、レベル、サーバー インスタンスでの冗長性によるローカル高可用性を提供する Windows Server フェールオーバー クラスタ リング (WSFC) の機能を活用して*フェールオーバー クラスター インスタンス*(FCI)。 FCI は、Windows Server フェールオーバー クラスタリング (WSFC) ノード全体、場合によっては複数のサブネットにインストールされる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の単一インスタンスです。 FCI は、ネットワーク上では 1 台のコンピューターで実行されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスのように見えますが、現在のノードが使用できなくなった場合には、1 つの WSFC ノードから別の WSFC ノードにフェールオーバーする機能を備えています。  
  
 詳細については、「[Always On フェールオーバー クラスター インスタンス (SQL Server)](windows/always-on-failover-cluster-instances-sql-server.md)」を参照してください。  
  
 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]  
 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]は、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] で導入された、エンタープライズ レベルの高可用性およびディザスター リカバリー ソリューションです。このソリューションによって、1 つ以上のユーザー データベースの可用性が最大限に高まります。 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] を使用するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスが Windows Server フェールオーバー クラスタリング (WSFC) ノードに存在している必要があります。 詳細については、次を参照してください。 [AlwaysOn 可用性グループ (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)します。  
  
> [!NOTE]  
>  FCI は、[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]を活用して、データベース レベルでのリモートのディザスター リカバリーを実現します。 詳細については、「[フェールオーバー クラスタリングと AlwaysOn 可用性グループ #40;SQL Server&#41;](../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)」を参照してください。  
  
 データベース ミラーリング  
 > [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] を使用することをお勧めします。  
  
 データベース ミラーリングは、ほぼ瞬時のフェールオーバーをサポートすることによりデータベースの可用性を向上させるソリューションです。 データベース ミラーリングを使用して、運用データベース (別称 *プリンシパル データベース*) と、それに対応する 1 つのスタンバイ データベース (別称 *ミラー データベース*) を管理できます。 詳細については、「[データベース ミラーリング &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)」を参照してください。  
  
 ログ配布  
 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] およびデータベース ミラーリングと同様、ログ配布はデータベース レベルで機能します。 ログ配布を使用して、1 つの運用データベース (*プライマリ データベース*) に対応する 1 つ以上のウォーム スタンバイ データベース (*セカンダリ データベース*) を管理できます。 ログ配布の詳細については、「[ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)」を参照してください。  
  
##  <a name="RecommendedSolutions"></a> SQL Server を使用してデータを保護するための推奨されるソリューション  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 環境にデータ保護を確立するための推奨事項は次のとおりです。  
  
-   データ保護、サードパーティ共有ディスク ソリューション (SAN) を通じて、AlwaysOn フェールオーバー クラスター インスタンスを使用することをお勧めします。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を通じたデータの保護には、 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]を使用することをお勧めします。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をサポートしないエディションの [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]を実行している場合は、ログ配布をお勧めします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のどのエディションで[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]がサポートされているかについては、「[SQL Server 2014 の各エディションでサポートされる機能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)」の「高可用性 (AlwaysOn)」のセクションを参照してください。  
  
## <a name="see-also"></a>参照  
 [Windows Server フェールオーバー クラスタリング &#40;WSFC&#41; と SQL Server](windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [データベース ミラーリング:相互運用性と共存 &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-interoperability-and-coexistence-sql-server.md)   
 [SQL Server 2014 データベース エンジンの非推奨の機能](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)  
  
  
