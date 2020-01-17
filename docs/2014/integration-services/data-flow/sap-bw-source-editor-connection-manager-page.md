---
title: SAP BW 変換元エディター ([接続マネージャー] ページ) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 2a6dc531-85ca-43c5-a65f-3ad3f7d537c4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b630442c1a47bcd4ebabee75b82cff9b8f64d006
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62901113"
---
# <a name="sap-bw-source-editor-connection-manager-page"></a>[SAP BW ソース エディター] ([接続マネージャー] ページ)
  **[SAP BW ソース エディター]** の **[接続マネージャー]** ページを使用すると、SAP BW 変換元の SAP BW 接続マネージャーを選択できます。 このページでは、実行モードと SAP Netweaver BW システムからデータを抽出するためのパラメーターも選択します。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW の SAP BW 変換元コンポーネントの詳細については、「 [SAP BW 転送元](sap-bw-source.md)」を参照してください。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW に関するドキュメントでは、SAP Netweaver BW 環境について理解していることを前提としています。 SAP Netweaver BW の詳細または SAP Netweaver BW オブジェクトやプロセスを構成する方法については、SAP のマニュアルを参照してください。  
  
> [!IMPORTANT]  
>  SAP Netweaver BW からデータを抽出するには、追加の SAP のライセンスが必要です。 これらの要件を確認するには、SAP にお問い合わせください。  
  
 **[接続マネージャー] ページを開くには**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、SAP BW 変換元が含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを開きます。  
  
2.  **[データ フロー]** タブで、SAP BW 変換元をダブルクリックします。  
  
3.  **[SAP BW 変換元エディター]** で、 **[接続マネージャー]** をクリックして **[接続マネージャー]** ページを開きます。  
  
## <a name="static-options"></a>静的オプション  
  
> [!NOTE]  
>  変換元を構成するために必要な値がわからない場合は、SAP 管理者に確認してください。  
  
 **SAP BW 接続マネージャー**  
 既存の接続マネージャーを一覧から選択するか、 **[新規作成]** をクリックして新しい接続を作成します。  
  
 **[新規作成]**  
 **[SAP BW 接続マネージャー]** ダイアログ ボックスを使用して、新しい接続マネージャーを作成します。  
  
 このダイアログ ボックスの詳細については、「 [SAP BW 接続マネージャー エディター](../sap-bw-connection-manager-editor.md)」を参照してください。  
  
 **OHS 転送先**  
 ソースからデータを抽出するためのオープン ハブ サービス (OHS) 転送先を選択します。  
  
 **実行モード**  
 ソースからデータを抽出する方法を指定します。  
  
|オプション|説明|  
|------------|-----------------|  
|**P - プロセス チェーンをトリガー**|プロセス チェーンをトリガーします。 この場合、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージが抽出プロセスを開始します。|  
|**W - 通知を待機**|SAP Netweaver BW システムから、データ抽出の開始する通知を待ちます。 この場合、SAP Netweaver BW システムが抽出プロセスを開始します。|  
|**E - 抽出のみ**|特定の要求 ID に関連付けられたデータを取得します。 この場合、SAP Netweaver BW システムが内部テーブルにデータを既に抽出済みで、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージはデータを読み取るだけです。|  
  
 **プレビュー**  
 結果をプレビューする **[プレビュー]** ダイアログ ボックスを開きます。 詳細については、「 [プレビュー](preview.md)」を参照してください。  
  
> [!IMPORTANT]  
>  **[プレビュー]** オプションは [SAP BW ソース エディター] の **[接続マネージャー]** ページで使用でき、実際にデータを抽出します。 前の抽出以降に変更されたデータのみを抽出するように SAP Netweaver BW を構成している場合、 **[プレビュー]** を選択すると、次の抽出からプレビュー データを除外します。  
  
 **[プレビュー]** をクリックすると、 **[要求のログ]** ダイアログ ボックスも開きます。 サンプル データの SAP Netweaver BW システムに対する要求中にログに記録するイベントを表示するには、このダイアログ ボックスを使用します。 詳細については、「 [要求のログ](request-log.md)」を参照してください。  
  
## <a name="execution-mode-dynamic-options"></a>実行モードの動的オプション  
  
> [!NOTE]  
>  変換元を構成するために必要な値がわからない場合は、SAP 管理者に確認してください。  
  
### <a name="execution-mode--p---trigger-process-chain"></a>実行モードが [P - プロセス チェーンをトリガー] の場合  
  
#### <a name="rfc-destination-options"></a>RFC 転送先に関するオプション  
 これらの値は、あらかじめ調べて入力する必要はありません。 **[参照]** ボタンを使用して、適切な RFC 転送先を探して選択します。 RFC 転送先を選択すると、これらのオプションに対する適切な値が入力されます。  
  
 **ゲートウェイ ホスト**  
 ゲートウェイ ホストのサーバー名または IP アドレスを入力します。 通常、IP アドレスの名前は、SAP アプリケーション サーバーの名前と同じです。  
  
 **ゲートウェイ サービス**  
 `sapgwNN` という形式でゲートウェイ サービスの名前を入力します。`NN` はシステム番号です。  
  
 **プログラム ID**  
 RFC 転送先に関連付けられているプログラム ID を入力します。  
  
 **[参照]**  
 **[RFC 転送先の参照]** ダイアログ ボックスを使用して、RFC 転送先を参照します。 このダイアログ ボックスの詳細については、「 [RFC 転送先の参照](look-up-rfc-destination.md)」を参照してください。  
  
#### <a name="process-chain-options"></a>プロセス チェーンに関するオプション  
 これらの値は、あらかじめ調べて入力する必要はありません。 **[参照]** ボタンを使用して、適切なプロセス チェーンを探して選択します。 プロセス チェーンを選択すると、これらのオプションに対する適切な値が入力されます。  
  
 **プロセス チェーン**  
 ソースがトリガーするプロセス チェーンの名前を入力します。  
  
 **[参照]**  
 **[プロセス チェーンの参照]** ダイアログ ボックスを使用して、プロセス チェーンを参照します。 このダイアログ ボックスの詳細については、「 [プロセス チェーンの参照](look-up-process-chain.md)」を参照してください。  
  
### <a name="execution-mode--w---wait-for-notify"></a>実行モードが [W - 通知を待機] の場合  
  
#### <a name="rfc-destination-options"></a>RFC 転送先に関するオプション  
 これらの値は、あらかじめ調べて入力する必要はありません。 **[参照]** ボタンを使用して、適切な RFC 転送先を探して選択します。 RFC 転送先を選択すると、これらのオプションに対する適切な値が入力されます。  
  
 **ゲートウェイ ホスト**  
 ゲートウェイ ホストのサーバー名または IP アドレスを入力します。 通常、IP アドレスの名前は、SAP アプリケーション サーバーの名前と同じです。  
  
 **ゲートウェイ サービス**  
 `sapgwNN` という形式でゲートウェイ サービスの名前を入力します。`NN` はシステム番号です。  
  
 **プログラム ID**  
 RFC 転送先に関連付けられているプログラム ID を入力します。  
  
 **[参照]**  
 **[RFC 転送先の参照]** ダイアログ ボックスを使用して、RFC 転送先を参照します。 このダイアログ ボックスの詳細については、「 [RFC 転送先の参照](look-up-rfc-destination.md)」を参照してください。  
  
### <a name="execution-mode--e---extract-only"></a>実行モードが [E - 抽出のみ] の場合  
 **要求 ID**  
 抽出に関連付けられている要求 ID を入力します。  
  
## <a name="see-also"></a>参照  
 [SAP BW ソース エディター ([列] ページ)](sap-bw-source-editor-columns-page.md)   
 [SAP BW ソース エディター &#40;[エラー出力] ページ&#41;](sap-bw-source-editor-error-output-page.md)   
 [SAP BW ソース エディター &#40;[詳細設定] ページ&#41;](sap-bw-source-editor-advanced-page.md)   
 [Microsoft Connector 1.1 for SAP BW の F1 ヘルプ](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
