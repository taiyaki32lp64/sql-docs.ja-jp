---
title: "要求のログ |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 165d3833-0493-490c-9f63-8a134a7fafb8
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 754f96b5e43b26d59bb1e42be6dd2af008c28dd2
ms.contentlocale: ja-jp
ms.lasthandoff: 08/03/2017

---
# <a name="request-log"></a>[要求のログ]
  サンプル データの SAP Netweaver BW システムに対する要求中にログに記録されたイベントを表示するには、 **[要求のログ]** ダイアログ ボックスを使用します。 この情報は、SAP BW 変換元の構成をトラブルシューティングする場合に便利です。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW の SAP BW 変換元コンポーネントの詳細については、「 [SAP BW 転送元](../../integration-services/data-flow/sap-bw-source.md)」を参照してください。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW に関するドキュメントでは、SAP Netweaver BW 環境について理解していることを前提としています。 SAP Netweaver BW の詳細または SAP Netweaver BW オブジェクトやプロセスを構成する方法については、SAP のマニュアルを参照してください。  
  
> [!IMPORTANT]  
>  SAP Netweaver BW からデータを抽出するには、追加の SAP のライセンスが必要です。 これらの要件を確認するには、SAP にお問い合わせください。  
  
 **要求のログのダイアログ ボックスを開く**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、SAP BW 変換元が含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを開きます。  
  
2.  **[データ フロー]** タブで、SAP BW 変換元をダブルクリックします。  
  
3.  **[SAP BW 変換元エディター]**で、 **[接続マネージャー]** をクリックして **[接続マネージャー]** ページを開きます。  
  
4.  SAP BW 変換元を構成した後、 **[要求のログ]** ダイアログ ボックスでイベントをプレビューするには **[プレビュー]** をクリックします。  
  
    > [!NOTE]  
    >  **[プレビュー]** をクリックすると、 **[プレビュー]** ダイアログ ボックスが表示されます。 このダイアログ ボックスの詳細については、「 [プレビュー](../../integration-services/data-flow/preview.md)」を参照してください。  
  
## <a name="options"></a>オプション  
 **時間**  
 イベントが記録された時刻を表示します。  
  
 **型**  
 記録されたイベントの種類を表示します。 次の表は、使用可能なイベントの種類を示しています。  
  
|値|Description|  
|-----------|-----------------|  
|S|成功メッセージ|  
|E|エラー メッセージ|  
|W|警告メッセージ。|  
|I|情報メッセージです。|  
|A|操作が中止されました。|  
  
 **メッセージ**  
 記録されたイベントに関連付けられたメッセージ テキストを表示します。  
  
## <a name="see-also"></a>参照  
 [SAP BW ソース エディター &#40;[接続マネージャー] ページ&#41;](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md)   
 [Microsoft Connector for SAP BW の F1 ヘルプ](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  