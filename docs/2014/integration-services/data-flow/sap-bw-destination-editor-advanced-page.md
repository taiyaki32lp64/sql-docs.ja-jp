---
title: '[SAP BW 変換先エディター] ([詳細設定] ページ) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 862957db-bbc6-4dda-bc0e-591457f1baa7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5396a6a94e1d5c4bfde39153081f3c4137a2c922
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62901037"
---
# <a name="sap-bw-destination-editor-advanced-page"></a>[SAP BW 変換先エディター] ([詳細設定] ページ)
  パッケージのサイズやタイムアウトの情報などの詳細を設定するには、**[SAP BW 変換先エディター]** の **[詳細設定]** ページを使用します。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW の SAP BW 変換先の詳細については、「 [SAP BW 転送先](sap-bw-destination.md)」を参照してください。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW に関するドキュメントでは、SAP Netweaver BW 環境について理解していることを前提としています。 SAP Netweaver BW の詳細または SAP Netweaver BW オブジェクトやプロセスを構成する方法については、SAP のマニュアルを参照してください。  
  
 **[詳細設定] ページを開くには**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、SAP BW 変換先が含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを開きます。  
  
2.  **[データ フロー]** タブで、SAP BW 変換先をダブルクリックします。  
  
3.  **[SAP BW 変換先エディター]** で、 **[詳細設定]** をクリックして **[詳細設定]** ページを開きます。  
  
## <a name="options"></a>および  
  
> [!NOTE]  
>  変換先を構成するために必要な値がわからない場合は、SAP 管理者に確認してください。  
  
 **パッケージのサイズ**  
 一度に転送するデータの行数を指定します。 このパラメーターの最適な値は、SAP Netweaver BW システムおよび発生する可能性のあるデータの追加処理によって異なります。 通常は、2,000 ～ 20,000 の値のパフォーマンスが最適です。  
  
 **プロセス チェーンをトリガー**  
 (省略可能) データの読み込みが完了した後にトリガーするプロセス チェーンの名前を指定します。  
  
 **インフォパッケージ待機のタイムアウト**  
 インフォパッケージの終了を待機する必要がある最大秒数を指定します。  
  
 **データ転送の完了を待機する**  
 SAP Netweaver BW システムがデータの読み込みを完了するまで、変換先が待機する必要があるかどうかを指定します。  
  
 **インフォパッケージを開始しない - 待機のみ**  
 変換先がインフォパッケージを開始せず、SAP Netweaver BW システムがデータの読み込みを開始した通知だけを待機することを指定します。  
  
## <a name="see-also"></a>参照  
 [SAP BW 変換先エディター &#40;[接続マネージャー] ページ&#41;](sap-bw-destination-editor-connection-manager-page.md)   
 [SAP BW 変換先エディター &#40;[マッピング] ページ&#41;](sap-bw-destination-editor-mappings-page.md)   
 [SAP BW 変換先エディター &#40;[エラー出力] ページ&#41;](sap-bw-destination-editor-error-output-page.md)   
 [Microsoft Connector 1.1 for SAP BW の F1 ヘルプ](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
