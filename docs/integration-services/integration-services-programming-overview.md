---
title: Integration Services プログラミングの概要 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Integration Services, programming
- architecture [Integration Services]
- assemblies [Integration Services]
- SSIS, programming
- SQL Server Integration Services, programming
- run-time engine [Integration Services]
- packages [Integration Services], programming
- data flow engine [Integration Services]
- languages [Integration Services]
ms.assetid: 262babc6-eea5-4609-bc65-07d64cbcfee9
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f540278d8f27eb091d4818f838d069c82a61159c
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296212"
---
# <a name="integration-services-programming-overview"></a>Integration Services プログラミングの概要

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] のアーキテクチャでは、データの移動と変換がパッケージの制御フローと管理から分離されています。 このアーキテクチャを定義し、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] のプログラムでの自動化および拡張を可能にする、次の 2 種類のエンジンがあります。 1 つはランタイム エンジンで、制御フローとパッケージ管理のインフラストラクチャを実装します。開発者は、このインフラストラクチャによって、実行フローを制御し、ログ記録、イベント ハンドラー、および変数用のオプションを設定できます。 もう 1 つはデータ フロー エンジンで、特殊でパフォーマンスの高いエンジンであり、データの抽出、変換、および読み込みを専門に行います。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] のプログラムの際には、これら 2 つのエンジンに対してプログラムを実行します。  
  
 次の図は、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] のアーキテクチャを示しています。  
  
 ![Integration Services のアーキテクチャ](../integration-services/media/mw-dts-01.gif "Integration Services のアーキテクチャ")  
  
## <a name="integration-services-run-time-engine"></a>Integration Services ランタイム エンジン  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ランタイム エンジンは、実行順序、ログ記録、変数、およびイベント処理を可能にするインフラストラクチャを実装することによって、パッケージの管理と実行を制御します。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ランタイム エンジンをプログラミングすることにより、開発者はパッケージの作成、構成、および実行を自動化し、カスタム タスクやその他の拡張機能を作成できます。  
  
 詳細については、「[スクリプト タスクによるパッケージの拡張](../integration-services/extending-packages-scripting/task/extending-the-package-with-the-script-task.md)」、「[カスタム タスクの開発](../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)」、および「[プログラムによるパッケージの作成](../integration-services/building-packages-programmatically/building-packages-programmatically.md)」を参照してください。  
  
## <a name="integration-services-data-flow-engine"></a>Integration Services データ フロー エンジン  
 データ フロー エンジンは、データ フロー タスクを管理します。データ フロー タスクは特殊でパフォーマンスの高いタスクで、さまざまなソースからのデータの移動および変換を専門に行います。 他のタスクと異なり、データ フロー タスクには、変換元、変換、変換先のいずれかになるデータ フロー コンポーネントと呼ばれるオブジェクトが追加で含まれています。 これらのコンポーネントはタスクの主要な稼働部分で、 データの移動および変換を定義します。 データ フロー エンジンをプログラムすることにより、開発者はデータ フロー タスク内のコンポーネントの作成および構成を自動化し、カスタム コンポーネントを作成できます。  
  
 詳細については、「[スクリプト コンポーネントによるデータ フローの拡張](../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)」、「[カスタム データ フロー コンポーネントの開発](../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)」、および「[プログラムによるパッケージの作成](../integration-services/building-packages-programmatically/building-packages-programmatically.md)」を参照してください。  
  
## <a name="supported-languages"></a>サポートされる言語  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] では、[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] が完全にサポートされています。 開発者は、.NET 準拠の言語から選択して [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] をプログラムできます。 ランタイム エンジンもデータ フロー エンジンも、ネイティブ コードで記述されますが、フル マネージドのオブジェクト モデルを介して使用できます。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージ、カスタム タスク、およびコンポーネントは、[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] または別のコード エディターやテキスト エディターでプログラミングできます。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] には、コーディング、デバッグ、およびテストの反復的なサイクルを簡略化および高速化する多数のツールや機能が開発者向けに用意されています。 また、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] を使用すると、配置も容易になります。 ただし、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] コード プロジェクトのコンパイルと構築に [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] は必要ありません。 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] SDK には、[!INCLUDE[vbprvb](../includes/vbprvb-md.md)] コンパイラと [!INCLUDE[csprcs](../includes/csprcs-md.md)] コンパイラ、および関連ツールが含まれています。  
  
> [!IMPORTANT]  
>  既定では、[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] は [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] と共にインストールされますが、[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] SDK はインストールされません。 SDK がコンピューターにインストールされておらず、SDK ドキュメントがオンライン ブック コレクションにも含まれていない場合、このセクションの SDK コンテンツへのリンクは機能しません。 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] SDK をインストールしたら、「[SQL Server の製品ドキュメントの追加または削除](https://msdn.microsoft.com/library/ef798cc8-87cf-4d60-a7bf-9e061bdd0052)」の手順に従って、SDK ドキュメントをオンライン ブック コレクションと目次に追加できます。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] スクリプト タスクおよびスクリプト コンポーネントでは、[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Tools for Applications (VSTA) を埋め込みスクリプト環境として使用します。 VSTA による [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual Basic および [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual C# のサポート  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] アプリケーション プログラミング インターフェイスは、VBScript などの COM ベースのスクリプト言語と互換性がありません。  
  
## <a name="locating-assemblies"></a>アセンブリの場所  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]では、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] アセンブリが .NET 4 にアップグレードされました。 \<*ドライブ*>:\Windows\Microsoft.NET\assembly に、.NET 4 用の別のグローバル アセンブリ キャッシュが用意されています。 すべての [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] アセンブリは、通常、このパスの GAC_MSIL フォルダーにあります。  
  
 以前のバージョンの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] と同様に、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] のコア機能拡張 .dll ファイルは *\<ドライブ>* :\Program Files\Microsoft SQL Server\100\SDK\Assemblies にあります。  
  
## <a name="commonly-used-assemblies"></a>通常使用されるアセンブリ  
 次の表は、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] を使用する [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] をプログラムするときに頻繁に使用されるアセンブリの一覧です。  
  
|アセンブリ|[説明]|  
|--------------|-----------------|  
|Microsoft.SqlServer.ManagedDTS.dll|マネージド ランタイム エンジンが含まれています。|  
|Microsoft.SqlServer.RuntimeWrapper.dll|ネイティブ ランタイム エンジン用のプライマリ相互運用機能アセンブリ (PIA)、つまりラッパーが含まれています。|  
|Microsoft.SqlServer.PipelineHost.dll|マネージド データ フロー エンジンが含まれています。|  
|Microsoft.SqlServer.PipelineWrapper.dll|ネイティブ データ フロー エンジン用のプライマリ相互運用機能アセンブリ (PIA)、つまりラッパーが含まれています。|  
  
  
