---
title: SAP BW 変換先エディター ([接続マネージャー] ページ) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sapbwdestination.connection.f1
ms.assetid: 04ae38f8-5287-45a3-826a-8aac5dd15a91
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 66365c942bc3f996d834f0217f29bd82cc911457
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298107"
---
# <a name="sap-bw-destination-editor-connection-manager-page"></a>[SAP BW 変換先エディター] ([接続マネージャー] ページ)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **[SAP BW 変換先エディター]** の **[接続マネージャー]** ページを使用すると、SAP BW 変換先が使用する SAP BW 接続マネージャーを選択できます。 このページでは、SAP Netweaver BW システムにデータを読み込むためのパラメーターも選択します。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW の SAP BW 変換先の詳細については、「 [SAP BW 転送先](../../integration-services/data-flow/sap-bw-destination.md)」を参照してください。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW に関するドキュメントでは、SAP Netweaver BW 環境について理解していることを前提としています。 SAP Netweaver BW の詳細または SAP Netweaver BW オブジェクトやプロセスを構成する方法については、SAP のマニュアルを参照してください。  
  
 **[接続マネージャー] ページを開くには**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、SAP BW 変換先が含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを開きます。  
  
2.  **[データ フロー]** タブで、SAP BW 変換先をダブルクリックします。  
  
3.  **[SAP BW 変換先エディター]** で、 **[接続マネージャー]** をクリックして **[接続マネージャー]** ページを開きます。  
  
## <a name="options"></a>オプション  
  
> [!NOTE]  
>  変換先を構成するために必要な値がわからない場合は、SAP 管理者に確認してください。  
  
 **SAP BW 接続マネージャー**  
 既存の接続マネージャーを一覧から選択するか、 **[新規作成]** をクリックして新しい接続を作成します。  
  
 **[新規作成]**  
 **[SAP BW 接続マネージャー]** ダイアログ ボックスを使用して、新しい接続マネージャーを作成します。  
  
 **テスト読み込み**  
 選択した設定とゼロ行を読み込む設定を使用して、読み込みプロセスのテストを実行します。  
  
### <a name="infopackageinfosource-options"></a>インフォパッケージ/インフォソースのオプション  
 これらの値は、あらかじめ調べて入力する必要はありません。 **[参照]** ボタンを使用して、適切なインフォパッケージを探して選択します。 インフォパッケージを選択すると、これらのオプションに対する適切な値が入力されます。  
  
 **インフォパッケージ**  
 インフォパッケージの名前を入力します。  
  
 **インフォソース**  
 インフォソースの名前を入力します。  
  
 **Type**  
 インフォソースの種類を識別する 1 文字を入力します。 指定できる 1 文字の値の一覧を次の表に示します。  
  
|値|[説明]|  
|-----------|-----------------|  
|**D**|トランザクション データ|  
|**M**|マスター データ|  
|**T**|テキスト|  
|**H**|Hierarchy データ|  
  
 **論理システム**  
 インフォパッケージに関連付けられている論理システムの名前を入力します。  
  
 **[参照]**  
 **[インフォパッケージの参照]** ダイアログ ボックスを使用して、インフォパッケージを参照します。 このダイアログ ボックスの詳細については、「 [インフォパッケージの参照](../../integration-services/data-flow/look-up-infopackage.md)」を参照してください。  
  
### <a name="rfc-destination-options"></a>RFC 転送先に関するオプション  
 これらの値は、あらかじめ調べて入力する必要はありません。 **[参照]** ボタンを使用して、適切な RFC 転送先を探して選択します。 RFC 転送先を選択すると、これらのオプションに対する適切な値が入力されます。  
  
 **ゲートウェイ ホスト**  
 ゲートウェイ ホストのサーバー名または IP アドレスを入力します。 通常、IP アドレスの名前は、SAP アプリケーション サーバーの名前と同じです。  
  
 **ゲートウェイ サービス**  
 **NN**がシステム数である、 **sapgwNN** という形式でゲートウェイ サービスの名前を入力します。  
  
 **プログラム ID**  
 RFC 転送先に関連付けられているプログラム ID を入力します。  
  
 **[参照]**  
 **[RFC 転送先の参照]** ダイアログ ボックスを使用して、RFC 転送先を参照します。 このダイアログ ボックスの詳細については、「 [RFC 転送先の参照](../../integration-services/data-flow/look-up-rfc-destination.md)」を参照してください。  
  
### <a name="create-sap-bw-objects-options"></a>SAP BW オブジェクトの作成のオプション  
 **オブジェクトの種類を選択**  
 SAP Netweaver BW オブジェクトの種類を選択します。 以下のいずれかの種類を選択できます。  
  
-   インフォオブジェクト  
  
-   インフォキューブ  
  
-   インフォソース  
  
-   インフォパッケージ  
  
 **作成**  
 選択した種類の SAP Netweaver BW オブジェクトを作成します。  
  
|[オブジェクトの種類]|結果|  
|-----------------|------------|  
|**インフォオブジェクト**|**[新しいインフォオブジェクトの作成]** ダイアログ ボックスを使用して、新しいインフォオブジェクトを作成します。 このダイアログ ボックスの詳細については、「 [新しいインフォオブジェクトの作成](../../integration-services/data-flow/create-new-infoobject.md)」を参照してください。|  
|**インフォキューブ**|**[トランザクション データのインフォキューブの作成]** ダイアログ ボックスを使用して、新しいインフォキューブを作成します。 このダイアログ ボックスの詳細については、「 [トランザクション データのインフォキューブの作成](../../integration-services/data-flow/create-infocube-for-transaction-data.md)」を参照してください。|  
|**インフォソース**|**[インフォソースの作成]** ダイアログ ボックスを使用してから、 **[トランザクション データのインフォソースの作成]** または **[マスター データのインフォソースの作成]** ダイアログ ボックスを使用して、新しいインフォソースを作成します。 これらのダイアログ ボックスに関する詳細については、「 [インフォソースの作成](../../integration-services/data-flow/create-infosource.md)」、「 [トランザクション データのインフォソースの作成](../../integration-services/data-flow/create-infosource-for-transaction-data.md) 」、「 [マスター データのインフォソースの作成](../../integration-services/data-flow/create-infosource-for-master-data.md)」を参照してください。|  
|**インフォパッケージ**|**[インフォパッケージの作成]** ダイアログ ボックスを使用して、新しいインフォパッケージを作成します。 このダイアログ ボックスの詳細については、「 [インフォパッケージの作成](../../integration-services/data-flow/create-infopackage.md)」を参照してください。|  
  
## <a name="see-also"></a>参照  
 [SAP BW 変換先エディター ([マッピング] ページ)](../../integration-services/data-flow/sap-bw-destination-editor-mappings-page.md)   
 [SAP BW 変換先エディター ([エラー出力] ページ)](../../integration-services/data-flow/sap-bw-destination-editor-error-output-page.md)   
 [SAP BW 変換先エディター &#40;[詳細設定] ページ&#41;](../../integration-services/data-flow/sap-bw-destination-editor-advanced-page.md)   
 [Microsoft Connector for SAP BW の F1 ヘルプ](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
