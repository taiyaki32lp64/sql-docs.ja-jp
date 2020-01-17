---
title: Analysis Services のサーバー プロパティの構成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- SSAS, configuration properties
- Analysis Services, configuration properties
- SQL Server Analysis Services, configuration properties
- configuration options [Analysis Services]
- server properties [Analysis Services]
- properties [Analysis Services], configuration
- properties [Analysis Services]
ms.assetid: 274b89cd-14ed-4666-bc13-eedf1de51e18
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 31c05bbc1be8376144eb191ff28a9cdc6eebdd8a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66068898"
---
# <a name="configure-server-properties-in-analysis-services"></a>Analysis Services のサーバーのプロパティの構成
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の管理者は、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンス用に既定のサーバー構成プロパティを変更できます。 各インスタンスには、同じサーバーの他のインスタンスとは別に設定できる固有の構成プロパティがあります。  
  
 サーバー プロパティを設定するには、SQL Server Management Studio を使用するか、特定のインスタンスの msmdsrv.ini ファイルを編集します。  
  
 このトピックには、次のセクションが含まれます。  
  
 [サーバー (インスタンス) のプロパティを構成します。](#bkmk_config)  
  
 [サーバー プロパティ リファレンス](#bkmk_ref)  
  
##  <a name="bkmk_config"></a> サーバー (インスタンス) のプロパティを構成します。  
 SQL Server Management Studio のプロパティ ページには、利用可能なプロパティのサブセットが含まれ、変更する可能性の高いプロパティのみが表示されます。 プロパティの完全なセットは msmdsrv.ini ファイルにあります。  
  
> [!NOTE]  
>  このトピックには、[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] の配置構成プロパティに関する情報は含まれていません。 展開構成の詳細については、次を参照してください。[ソリューションの配置に関する構成設定を指定する](../multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)します。  
  
#### <a name="view-or-set-configuration-properties-in-management-studio"></a>Management Studio での構成プロパティの表示または設定  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のインスタンスに接続します。  
  
     オブジェクト エクスプローラーで、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスを右クリックし、 **[プロパティ]** をクリックします。 [全般] ページが表示され、より使用頻度の高いプロパティが表示されます。  
  
2.  その他のプロパティを表示するには、ページ下部にある **[すべての詳細プロパティを表示する]** チェック ボックスをオンにします。  
  
     サーバー プロパティの変更は、テーブル モードおよび多次元モードのサーバーについてのみサポートされます。 マイクロソフトの製品サポート エンジニアから別途指示された場合を除き、[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] をインストールした場合は、必ず既定値を使用してください。  
  
     運用上またはパフォーマンス上の問題をサーバーのプロパティを通じて解消する方法については、「 [SQL Server 2008 R2 Analysis Services 操作ガイド](https://go.microsoft.com/fwlink/?LinkID=225539)」を参照してください。  
  
     サーバーのプロパティについては、Microsoft ホワイト ペーパー「 [SQL Server 2005 Analysis Services (SSAS) サーバー プロパティ](https://go.microsoft.com/fwlink/?LinkID=199102)」も参照してください。サーバーのプロパティの多くは、過去数回のリリースにわたり変更されていません。  
  
    > [!NOTE]  
    >  一部のプロパティの設定は、msmdrsrv.ini ファイルでのみ行うことができます。 詳細プロパティを表示しても設定する対象のプロパティが含まれていない場合は、msmdsrv.ini ファイルを直接編集する必要があります。  
  
#### <a name="view-or-edit-configuration-properties-in-the-msmdsrvini-file"></a>msmdsrv.ini ファイルの構成プロパティの表示または編集  
  
1.  開始する前に、 **DataDir** msmdsrv.ini ファイルを含む、Analysis Services プログラム ファイルの場所を確認の Management Studio の [全般プロパティ] ページのプロパティ。 プログラム ファイルの場所を確認することで、確実に、目的のファイルに変更を加えることができます。  
  
    > [!NOTE]  
    >  既定のインストールでは、ファイルは \Program Files\Microsoft SQL Server\MSAS12.MSSQLSERVER\OLAP\Config フォルダーに格納されます。  
  
2.  元のファイルに戻す必要がある場合は、ファイルのバックアップを作成します。  
  
3.  テキスト エディターを使用して、msmdsrv.ini ファイルを表示または編集します。  
  
4.  ファイルを保存した後で、サービスを再起動する必要があります。  
  
##  <a name="bkmk_ref"></a> サーバー プロパティ リファレンス  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の構成プロパティは、システムを微調整するために重要です。 たとえば、クエリ ログ動作を必要条件に合わせるために、関連するプロパティを設定できます。  
  
 次のトピックでは、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のさまざまな構成プロパティについて説明します。  
  
|トピック|説明|  
|-----------|-----------------|  
|[全般プロパティ](general-properties.md)|全般プロパティには、基本プロパティと詳細プロパティの両方があり、データ ディレクトリ、バックアップ ディレクトリ、およびサーバーの他の動作を定義するプロパティが含まれます。|  
|[データ マイニング プロパティ](data-mining-properties.md)|データ マイニング プロパティでは、どのデータ マイニング アルゴリズムを有効または無効にするかを制御します。 既定では、すべてのアルゴリズムが有効になっています。|  
|DSO|DSO は現在サポートされません。 DSO のプロパティは無視されます。|  
|[機能プロパティ](feature-properties.md)|機能プロパティは、製品の機能に関連しており、そのほとんどが詳細プロパティです。サーバー インスタンス間のリンクを制御するプロパティが含まれます。|  
|[Filestore プロパティ](filestore-properties.md)|ファイル ストア プロパティは、高度な用途のみを対象としています。 高度なメモリ管理設定が含まれます。|  
|[ロック マネージャーのプロパティ](lock-manager-properties.md)|ロック マネージャー プロパティでは、ロックおよびタイムアウトに関連するサーバーの動作を定義します。 これらのほとんどのプロパティは、高度な用途のみを対象としています。|  
|[ログのプロパティ](log-properties.md)|ログ プロパティでは、サーバー上でイベントがログ記録される条件、場所、および方法を制御します。 これには、エラー ログ、例外ログ、フライト レコーダー、クエリ ログ、およびトレースが含まれます。|  
|[メモリのプロパティ](memory-properties.md)|メモリ プロパティでは、サーバーでメモリが使用される方法を制御します。 主に高度な用途を対象としています。|  
|[ネットワーク プロパティ](network-properties.md)|ネットワーク プロパティでは、ネットワークに関連するサーバーの動作を制御します。圧縮およびバイナリ XML を制御するプロパティが含まれます。 これらのほとんどのプロパティは、高度な用途のみを対象としています。|  
|[OLAP のプロパティ](olap-properties.md)|OLAP プロパティでは、キューブおよびディメンションの処理、レイジー処理、データのキャッシュ、およびクエリの動作を制御します。 基本プロパティと詳細プロパティの両方が含まれます。|  
|[セキュリティのプロパティ](security-properties.md)|セキュリティ セクションには、アクセス権を定義する基本プロパティと詳細プロパティの両方が含まれています。 管理者およびユーザーに関連する設定が含まれます。|  
|[スレッド プール プロパティ](thread-pool-properties.md)|スレッド プール プロパティでは、サーバーによって作成されるスレッドの数を制御します。 これらは主に詳細プロパティです。|  
  
## <a name="see-also"></a>参照  
 [Analysis Services インスタンス管理](../instances/analysis-services-instance-management.md)   
 [ソリューションの配置に関する構成設定の指定](../multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)  
  
  
