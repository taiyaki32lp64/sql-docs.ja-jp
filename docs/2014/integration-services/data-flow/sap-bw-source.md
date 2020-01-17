---
title: SAP BW 変換元 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 749afb64-3567-4dc9-8431-783d650c25db
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 169c35d89075646aa3f4964d0e9d6eda92bc13a2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62901072"
---
# <a name="sap-bw-source"></a>SAP BW 転送元
  SAP BW 変換元は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW の変換元コンポーネントです。 SAP BW 変換元は、SAP Netweaver BW Version 7 システムからデータを抽出し、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージのデータ フローにこのデータを使用可能にします。  
  
 この変換は、1 つの出力と 1 つのエラー出力をとります。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW に関するドキュメントでは、SAP Netweaver BW 環境について理解していることを前提としています。 SAP Netweaver BW の詳細または SAP Netweaver BW オブジェクトやプロセスを構成する方法については、SAP のマニュアルを参照してください。  
  
> [!IMPORTANT]  
>  SAP Netweaver BW からデータを抽出するには、追加の SAP のライセンスが必要です。 これらの要件を確認するには、SAP にお問い合わせください。  
  
 SAP BW 変換元を使用するには、次の作業を行う必要があります。  
  
-   [SAP Netweaver BW オブジェクトを準備する](#bkmk_Prepare_Objects)  
  
-   [SAP Netweaver BW システムに接続する](#bkmk_Connect_Database)  
  
-   [SAP BW 変換元を構成する](#bkmk_Configure_Source)  
  
##  <a name="bkmk_Prepare_Objects"></a> 変換元に必要な SAP Netweaver BW オブジェクトの準備  
 SAP BW 変換元を使用する前に、特定のオブジェクトを SAP Netweaver BW システムに含める必要があります。 これらのオブジェクトがまだ存在しない場合は、これらの手順に従って SAP Netweaver BW システムで作成および構成する必要があります。  
  
> [!NOTE]  
>  これらのオブジェクトと構成手順の詳細については、SAP Netweaver BW のマニュアルを参照してください。  
  
1.  SAP の GUI から SAP Netweaver BW にログインしてトランザクション コード SM59 を入力し、RFC 変換先を作成します。  
  
    1.  **[接続の種類]** の **[TCP/IP]** を選択します。  
  
    2.  **[アクティブ化の種類]** の **[登録済みサーバーのプログラム]** を選択します。  
  
    3.  **[対象のシステムを使用している通信の種類]** の **[非 Unicode (非アクティブな MDMP の設定)]** を選択します。  
  
    4.  適切なプログラム ID を割り当てます。  
  
2.  オープン ハブ転送先を作成します。  
  
    1.  Administrator Workbench (トランザクション コード RSA1) に移動し、左ペインで **[オープン ハブ転送先]** を選択します。  
  
    2.  中央のペインで、InfoArea を右クリックし、 **["オープン ハブ転送先の作成"]** を選択します。  
  
    3.  **[変換先の種類]** で、 **["サード パーティ ツール"]** を選択し、作成済みの RFC 変換先を入力します。  
  
    4.  新しいオープン ハブ転送先を保存してアクティブにします。  
  
3.  データ転送プロセス (DTP) を作成します。  
  
    1.  InfoArea の中央のペインで、作成済みの変換先を右クリックし、 **[データ転送プロセスの作成]** を選択します。  
  
    2.  DTP を構成、保存、およびアクティブ化します。  
  
    3.  メニューで、パーティションをクリックし、 **[移動]** をクリックして、 **[バッチ マネージャーの設定]** をクリックします。  
  
    4.  順次処理用に **[プロセス数]** を 1 に更新します。  
  
4.  プロセス チェーンを作成します。  
  
    1.  プロセス チェーンを構成する場合、 **[メタデータ チェーンまたは API の使用を開始する]** を **[処理の開始]** の **[スケジュール設定のオプション]** として選択し、作成済みの DTP を後続のノードとして追加します。  
  
    2.  プロセス チェーンを保存し、アクティブにします。  
  
     SAP BW 変換元は、データ転送プロセスをアクティブにするプロセス チェーンを呼び出すことができます。  
  
##  <a name="bkmk_Connect_Database"></a> SAP Netweaver BW システムへの接続  
 SAP Netweaver BW Version 7 システムに接続するため、SAP BW 変換元は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW パッケージの一部である SAP BW 接続マネージャーを使用します。 SAP BW 接続マネージャーは、SAP BW 変換元が使用できる唯一の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 接続マネージャーです。  
  
 SAP BW 接続マネージャーの詳細については、「 [SAP BW Connection Manager](../connection-manager/sap-bw-connection-manager.md)」を参照してください。  
  
##  <a name="bkmk_Configure_Source"></a> SAP BW 変換元の構成  
 SAP BW 変換元は、次の方法で構成できます。  
  
-   データを抽出するためのオープン ハブ サービス (OHS) 転送先を探して選択します。  
  
-   データを抽出するため次のいずれかの方法を選択します。  
  
    -   プロセス チェーンをトリガーします。 この場合、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージが抽出プロセスを開始します。  
  
    -   SAP Netweaver BW システムからのデータ抽出開始通知を待ちます。 この場合、SAP Netweaver BW システムが抽出プロセスを開始します。  
  
    -   特定の要求 ID に関連付けられたデータを取得します。 この場合、SAP Netweaver BW システムが内部テーブルにデータを既に抽出済みで、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージはデータを読み取るだけです。  
  
-   データの抽出方法に応じて、次の追加情報を指定します。  
  
    -   **[P - プロセス チェーンをトリガー]** オプションでは、RFC 変換先のゲートウェイ ホスト名、ゲートウェイ サービス名、プログラム ID、およびプロセス チェーンの名前を指定します。  
  
    -   **[W - 通知を待機]** オプションでは、RFC 変換先のゲートウェイ ホスト名、ゲートウェイ サーバー名、およびプログラム ID を指定します。 タイムアウト値も指定できます (秒単位)。 タイムアウトは、変換元が通知を待機する最大時間です。  
  
    -   **[E - 抽出のみ]** オプションでは、要求 ID を指定します。  
  
-   文字列変換のルールを指定します (たとえば、すべての文字列を SAP Netweaver BW システムが Unicode であるかどうかに応じて変換するか、`varchar` または `nvarchar` に変換するかどうか)。  
  
-   選択したオプションを使用して、抽出するデータをプレビューします。  
  
 変換元が呼び出す RFC 関数のログを有効にすることもできます (このログは、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージで有効にできる、省略可能なログとは異なります)。変換元が使用する SAP BW 接続マネージャーを構成する際に、RFC 関数呼び出しのログ記録を有効にします。 SAP BW 接続マネージャーを構成する方法の詳細については、「 [SAP BW Connection Manager](../connection-manager/sap-bw-connection-manager.md)」を参照してください。  
  
 変換元を構成するために必要な値がわからない場合は、SAP 管理者に確認してください。  
  
 SAP BW 接続マネージャー、変換元、変換先の構成および使用方法の詳細については、ホワイト ペーパー「 [SAP BI 7.0 を使用した SQL Server 2008 Integration Services](https://go.microsoft.com/fwlink/?LinkID=137090)」を参照してください。 このホワイト ペーパーには、SAP BW で必要なオブジェクトの構成方法についても説明されています。  
  
### <a name="using-the-ssis-designer-to-configure-the-source"></a>SSIS デザイナーを使用してソースを構成する  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できる SAP BW 変換元のプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [SAP BW ソース エディター ([接続マネージャー] ページ)](sap-bw-source-editor-connection-manager-page.md)  
  
-   [SAP BW ソース エディター ([列] ページ)](sap-bw-source-editor-columns-page.md)  
  
-   [SAP BW ソース エディター ([エラー出力] ページ)](sap-bw-source-editor-error-output-page.md)  
  
-   [SAP BW ソース エディター ([詳細設定] ページ)](sap-bw-source-editor-advanced-page.md)  
  
 SAP BW 変換元を構成するときに、SAP Netweaver BW オブジェクトを参照したり、ソース データをプレビューしたりするためにさまざまなダイアログ ボックスを使用できます。 これらのダイアログ ボックスの詳細については、次のトピックのいずれかを参照してください。  
  
-   [[RFC 転送先の参照]](look-up-rfc-destination.md)  
  
-   [プロセス チェーンの参照](look-up-process-chain.md)  
  
-   [要求のログ](request-log.md)  
  
-   [プレビュー](preview.md)  
  
## <a name="see-also"></a>参照  
 [Microsoft Connector 1.1 for SAP BW のコンポーネント](../microsoft-connector-for-sap-bw-components.md)  
  
  
