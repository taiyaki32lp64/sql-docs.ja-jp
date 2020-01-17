---
title: クラスターにおける Integration Services (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 0216266d-d866-4ea2-bbeb-955965f4d7c2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b70dbab14424335fe210f5a9b1ddbdbda4f90deb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62889305"
---
# <a name="integration-services-ssis-in-a-cluster"></a>クラスターにおける Integration Services (SSIS)
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] をクラスター化することはお勧めしません。[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは、クラスター化されるサービスまたはクラスター対応サービスではなく、クラスター ノード間のフェールオーバーはサポートしません。 したがって、クラスター環境では、クラスターの各ノードで [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] をインストールし、スタンドアロン サービスとして起動する必要があります。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスはクラスター化されるサービスではありませんが、クラスターの各ノードに個別に [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] をインストールした後、クラスター リソースとして動作するように手動で構成することができます。  
  
 ただし、クラスター化されたハードウェア環境を構築する目的が高可用性を実現することにある場合は、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスをクラスター リソースとして構成しなくても、この目的を達成できます。  クラスター内の他のノードからクラスター内の任意のノード上でパッケージを管理するには、クラスター内の各ノードで [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスの構成ファイルを変更します。 パッケージが格納されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の使用可能なすべてのインスタンスを指し示すように、それぞれの構成ファイルを変更します。 この方法を使用すると、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスをクラスター リソースとして構成したときに発生する可能性のある問題を回避できるうえ、ほとんどの顧客から求められる高可用性を実現できます。 構成ファイルの変更方法の詳細については、「[Integration Services サービスの構成 (SSIS サービス)](integration-services-service-ssis-service.md)」を参照してください。  
  
 クラスター環境でサービスをどのように構成するかに関して詳しい情報に基づく決断を行うには、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスの役割を理解することがきわめて重要です。 詳細については、「[Integration Services サービス (SSIS サービス)](integration-services-service-ssis-service.md)」を参照してください。  
  
## <a name="understanding-the-disadvantages-of-configuring-integration-services-as-a-cluster-resource"></a>Integration Services をクラスター リソースとして構成する場合の欠点について  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスをクラスター リソースとして構成する場合、次のような潜在的な欠点があります。  
  
-   フェールオーバーが発生したときに、実行中のパッケージが再起動されません。 チェックポイントからパッケージを再開することで、パッケージのエラーから回復できます。 サービスをクラスター リソースとして構成しなくても、チェックポイントからパッケージを再開できます。 詳細については、「 [チェックポイントを使用してパッケージを再開する](../packages/restart-packages-by-using-checkpoints.md)」を参照してください。  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] とは異なるリソース グループに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]サービスを構成した場合、クライアント コンピューターから [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を使用して msdb データベースに格納されているパッケージを管理することはできません。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは、このダブルホップ シナリオで資格情報を委任することはできません。  
  
-   クラスター内に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスを含む複数の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] リソース グループがある場合、フェールオーバーにより予期しない結果が生じる可能性があります。 次のシナリオについて考えてみます。 グループ 1 は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスと [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスを含み、ノード A 上で実行されています。グループ 2 は、同様に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスと [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスを含み、ノード B 上で実行されています。次に、グループ 2 からノード A へのフェールオーバーが発生します。ここで、ノード A 上で [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスの別のインスタンスを起動しようとした場合、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは単一インスタンス サービスなので、その試みは失敗します。 ノード A へのフェールオーバーを試行している [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスが同様に失敗するかどうかは、グループ 2 における [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスの構成に依存します。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスがリソース グループ内の他のサービスに影響を与えるように構成されている場合、フェールオーバーを試行している [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスは失敗します。なぜなら、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスが失敗しているからです。 サービスがリソース グループ内の他のサービスに影響を与えないように構成されている場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスはノード A にフェールオーバーできます。リソース グループ内の他のサービスに影響を与えないようにグループ 2 の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスが構成されていない限り、フェールオーバーを試行している [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスが失敗すると、フェールオーバーを試行している [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスも失敗する可能性があります。  
  
## <a name="related-tasks"></a>Related Tasks  
 クラスター内で Integration Services サービスを構成する手順については、「 [クラスター リソースとして Integration Services サービスを構成する](../configure-the-integration-services-service-as-a-cluster-resource.md)」を参照してください。  
  
  
