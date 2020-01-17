---
title: '[SAP BW 変換元エディター] ([詳細設定] ページ) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sapbwsource.advanced.f1
ms.assetid: 44f3c991-9e8f-4126-a9a2-2d9da779fb11
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a8eaed6e70ad457f33dc9587e3004e433da43ae1
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298086"
---
# <a name="sap-bw-source-editor-advanced-page"></a>[SAP BW 変換元エディター] ([詳細設定] ページ)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  文字列の変換規則とタイムアウト期間を指定し、特定の要求 ID の状態をリセットするには、 **[SAP BW 変換元エディター]** の **[詳細設定]** ページを使用します。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW の SAP BW 変換元コンポーネントの詳細については、「 [SAP BW 転送元](../../integration-services/data-flow/sap-bw-source.md)」を参照してください。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW に関するドキュメントでは、SAP Netweaver BW 環境について理解していることを前提としています。 SAP Netweaver BW の詳細または SAP Netweaver BW オブジェクトやプロセスを構成する方法については、SAP のマニュアルを参照してください。  
  
> [!IMPORTANT]  
>  SAP Netweaver BW からデータを抽出するには、追加の SAP のライセンスが必要です。 これらの要件を確認するには、SAP にお問い合わせください。  
  
 **[接続マネージャー] ページを開くには**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、SAP BW 変換元が含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを開きます。  
  
2.  **[データ フロー]** タブで、SAP BW 変換元をダブルクリックします。  
  
3.  **[SAP BW 変換元エディター]** で、 **[詳細設定]** をクリックして **[詳細設定]** ページを開きます。  
  
## <a name="options"></a>オプション  
  
> [!NOTE]  
>  変換元を構成するために必要な値がわからない場合は、SAP 管理者に確認してください。  
  
 **文字列変換**  
 文字列変換に適用するルールを指定します。  
  
|オプション|[説明]|  
|------------|-----------------|  
|**自動文字列変換**|SAP Netweaver BW システムが Unicode システムの場合に、 **nvarchar** にすべての文字列を変換します。 それ以外の場合は **varchar**にすべての文字列を変換します。|  
|**文字列を varchar に変換**|**varchar**にすべての文字列を変換します。|  
|**文字列を nvarchar に変換**|**nvarchar**にすべての文字列を変換します。|  
  
 **タイムアウト (秒)**  
 ソースが待機する最大秒数を指定します。  
  
> [!NOTE]  
>  このオプションは、エディターの **[接続マネージャー]** ページの **[実行モード]** の値として **[W - 通知を待機]** を選択した場合にのみ有効です。 詳細については、「 [SAP BW ソース エディター ([接続マネージャー] ページ)](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md)」を参照してください。  
  
 **要求 ID**  
 **[リセット]** をクリックしたときに状態を "G - Green" にリセットする要求 ID を指定します。  
  
 **[リセット]**  
 確認後に、指定した要求 ID の状態を "G - Green" リセットできます。 これは、問題が発生し、SAP Netweaver BW システムが要求に黄色または赤の状態フラグを設定した便利です。  
  
## <a name="see-also"></a>参照  
 [SAP BW 変換元エディター &#40;[接続マネージャー] ページ&#41;](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md)   
 [SAP BW ソース エディター ([列] ページ)](../../integration-services/data-flow/sap-bw-source-editor-columns-page.md)   
 [SAP BW ソース エディター ([エラー出力] ページ)](../../integration-services/data-flow/sap-bw-source-editor-error-output-page.md)   
 [Microsoft Connector for SAP BW の F1 ヘルプ](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
