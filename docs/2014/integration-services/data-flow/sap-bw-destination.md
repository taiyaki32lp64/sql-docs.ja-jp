---
title: SAP BW 転送先 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a612ed91-b89b-4173-a0b1-0bce381e1e28
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1cac8403327ecf3888439290554f059bb00bce2c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770870"
---
# <a name="sap-bw-destination"></a>SAP BW 転送先
  SAP BW 変換先は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW の変換先コンポーネントです。 SAP BW 変換先は、SAP Netweaver BW Version 7 システムに [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージのデータ フローのデータを読み込みます。  
  
 変換先は 1 つの入力と 1 つのエラー出力をとります。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW に関するドキュメントでは、SAP Netweaver BW 環境について理解していることを前提としています。 SAP Netweaver BW の詳細または SAP Netweaver BW オブジェクトやプロセスを構成する方法については、SAP のマニュアルを参照してください。  
  
 SAP BW 変換先を使用するには、次の作業を行う必要があります。  
  
-   [SAP Netweaver BW オブジェクトを準備する](#bkmk_Prepare_Objects)  
  
-   [SAP Netweaver BW システムに接続する](#bkmk_Connect_Database)  
  
-   [SAP BW 変換先の構成](#bkmk_Configure_Destination)  
  
##  <a name="bkmk_Prepare_Objects"></a> 変換先に必要な SAP Netweaver BW オブジェクトの準備  
 SAP BW 変換先を使用する前に、特定のオブジェクトを SAP Netweaver BW システムに含める必要があります。 これらのオブジェクトがまだ存在しない場合は、これらの手順に従って SAP Netweaver BW システムで作成および構成する必要があります。  
  
> [!NOTE]  
>  これらのオブジェクトと構成手順の詳細については、SAP Netweaver BW のマニュアルを参照してください。  
  
1.  新しいデータ ソースを作成します。  
  
    1.  種類として **["サード パーティ/ステージング BAPI"]** を選択します。  
  
    2.  **[対象のシステムを使用している通信の種類]** の **[非 Unicode (非アクティブな MDMP の設定)]** を選択します。  
  
    3.  適切なプログラム ID を割り当てます。  
  
2.  インフォソースにソース システムを割り当てます。  
  
3.  インフォパッケージを作成します。  
  
     インフォパッケージは、SAP BW 変換先に必要な最も重要なオブジェクトです。  
  
 また、SAP Netweaver BW システムにデータの読み込みをサポートするために必要な、追加のインフォオブジェクト、インフォキューブ、インフォソース、およびインフォパッケージを作成できます。  
  
##  <a name="bkmk_Connect_Database"></a> SAP Netweaver BW システムへの接続  
 SAP Netweaver BW Version 7 システムに接続するため、SAP BW 変換先は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW パッケージの一部である SAP BW 接続マネージャーを使用します。 SAP BW 接続マネージャーは、SAP BW 変換先が使用できる唯一の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 接続マネージャーです。  
  
 SAP BW 接続マネージャーの詳細については、「 [SAP BW Connection Manager](../connection-manager/sap-bw-connection-manager.md)」を参照してください。  
  
##  <a name="bkmk_Configure_Destination"></a> SAP BW 変換先の構成  
 SAP BW 変換先は、次の方法で構成できます。  
  
-   データの読み込みに使用するインフォパッケージを探して参照します。  
  
-   インフォパッケージの適切なインフォオブジェクトへのデータ フロー内の各列をマップします。  
  
-   `PackageSize` プロパティを構成して、一度に転送するデータの行数を指定します。  
  
-   データの読み込みが SAP Netweaver BW システムで完了するまで待機することを選択します。  
  
-   インフォパッケージを開始せず、SAP Netweaver BW システムがデータの読み込みを開始した通知を待機することを指定します。  
  
-   必要に応じて、データの読み込みが完了した後に別のプロセス チェーンを発生させます。  
  
-   必要に応じて、変換先に必要な SAP Netweaver BW オブジェクトを作成します。 これには、インフォオブジェクト、インフォキューブ、インフォソース、およびインフォパッケージの作成も含まれます。  
  
-   選択したオプションで、データの読み込みをテストします。  
  
 変換先が呼び出す RFC 関数のログを有効にすることもできます (このログは、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージで有効にできる、省略可能なログとは異なります)。変換先が使用する SAP BW 接続マネージャーを構成する際に、RFC 関数呼び出しのログ記録を有効にします。 SAP BW 接続マネージャーを構成する方法の詳細については、「 [SAP BW Connection Manager](../connection-manager/sap-bw-connection-manager.md)」を参照してください。  
  
 変換先を構成するために必要な値がわからない場合は、SAP 管理者に確認してください。  
  
 SAP BW 接続マネージャー、変換元、変換先の構成および使用方法の詳細については、ホワイト ペーパー「 [SAP BI 7.0 を使用した SQL Server 2008 Integration Services](https://go.microsoft.com/fwlink/?LinkID=137090)」を参照してください。 このホワイト ペーパーには、SAP BW で必要なオブジェクトの構成方法についても説明されています。  
  
### <a name="using-the-ssis-designer-to-configure-the-destination"></a>SSIS デザイナーを使用して変換先を構成する  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できる SAP BW 変換先のプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [SAP BW 変換先エディター &#40;[接続マネージャー] ページ&#41;](sap-bw-destination-editor-connection-manager-page.md)  
  
-   [SAP BW 変換先エディター ([マッピング] ページ)](sap-bw-destination-editor-mappings-page.md)  
  
-   [SAP BW 変換先エディター ([エラー出力] ページ)](sap-bw-destination-editor-error-output-page.md)  
  
-   [SAP BW 変換先エディター &#40;[詳細設定] ページ&#41;](sap-bw-destination-editor-advanced-page.md)  
  
 SAP BW 変換先を構成するときに、SAP Netweaver BW オブジェクトを参照または作成するためにさまざまなダイアログ ボックスを使用できます。 これらのダイアログ ボックスの詳細については、次のトピックのいずれかを参照してください。  
  
-   [[インフォパッケージの参照]](look-up-infopackage.md)  
  
-   [新しいインフォオブジェクトの作成](create-new-infoobject.md)  
  
-   [トランザクション データのインフォキューブの作成](create-infocube-for-transaction-data.md)  
  
-   [インフォオブジェクトの参照](look-up-infoobject.md)  
  
-   [インフォソースの作成](create-infosource.md)  
  
-   [トランザクション データのインフォソースの作成](create-infosource-for-transaction-data.md)  
  
-   [マスター データのインフォソースの作成](create-infosource-for-master-data.md)  
  
-   [インフォパッケージの作成](create-infopackage.md)  
  
## <a name="see-also"></a>関連項目  
 [Microsoft Connector 1.1 for SAP BW のコンポーネント](../microsoft-connector-for-sap-bw-components.md)  
  
  
