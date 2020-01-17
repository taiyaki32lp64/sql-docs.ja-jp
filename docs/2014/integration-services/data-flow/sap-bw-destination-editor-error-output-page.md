---
title: '[SAP BW 変換先エディター] ([エラー出力] ページ) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a543d811-0bd2-4890-a0d3-f5fdcd4524b8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 196d7f2bb3a227bd29ccc6fd5d427a59070d525a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770918"
---
# <a name="sap-bw-destination-editor-error-output-page"></a>[SAP BW 変換先エディター] ([エラー出力] ページ)
  **[SAP BW 変換先エディター]** の **[エラー出力]** ページを使用すると、エラー処理オプションを指定できます。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW の SAP BW 変換先の詳細については、「 [SAP BW 転送先](sap-bw-destination.md)」を参照してください。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW に関するドキュメントでは、SAP Netweaver BW 環境について理解していることを前提としています。 SAP Netweaver BW の詳細または SAP Netweaver BW オブジェクトやプロセスを構成する方法については、SAP のマニュアルを参照してください。  
  
 **[エラー出力] ページを開くには**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、SAP BW 変換先が含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを開きます。  
  
2.  **[データ フロー]** タブで、SAP BW 変換先をダブルクリックします。  
  
3.  **[SAP BW 変換先エディター]** で、 **[エラー出力]** をクリックして **[エラー出力]** ページを開きます。  
  
## <a name="options"></a>および  
  
> [!NOTE]  
>  変換先を構成するために必要な値がわからない場合は、SAP 管理者に確認してください。  
  
 **入力または出力**  
 入力の名前を表示します。  
  
 **列**  
 このオプションは使用されません。  
  
 **Error**  
 変換先が、エラーが発生した場合に障害を無視するか、行をリダイレクトするか、コンポーネントを失敗させるかを指定します。  
  
 **切り捨て**  
 このオプションは使用されません。  
  
 **[説明]**  
 操作の説明を表示します。  
  
 **[選択したセルに設定する値]**  
 エラーまたは切り捨てが発生した場合に、選択したすべてのセルに対して変換先が障害を無視するか、行をリダイレクトするか、コンポーネントを失敗させるかを指定します。  
  
 **[適用]**  
 選択したセルにエラー処理オプションを適用します。  
  
## <a name="see-also"></a>参照  
 [SAP BW 変換先エディター &#40;[接続マネージャー] ページ&#41;](sap-bw-destination-editor-connection-manager-page.md)   
 [SAP BW 変換先エディター &#40;[マッピング] ページ&#41;](sap-bw-destination-editor-mappings-page.md)   
 [SAP BW 変換先エディター &#40;[詳細設定] ページ&#41;](sap-bw-destination-editor-advanced-page.md)   
 [Microsoft Connector 1.1 for SAP BW の F1 ヘルプ](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
