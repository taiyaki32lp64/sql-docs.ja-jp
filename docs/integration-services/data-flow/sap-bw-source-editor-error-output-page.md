---
title: '[SAP BW 変換元エディター] ([エラー出力] ページ) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sapbwsource.erroroutput.f1
ms.assetid: b6e23b0c-949a-46d1-8424-4dc3d9035e79
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9973a785efd0e3327ac7fe1e12360bd202601f1e
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71291824"
---
# <a name="sap-bw-source-editor-error-output-page"></a>[SAP BW 変換元エディター] ([エラー出力] ページ)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **[SAP BW 変換元エディター]** の **[エラー出力]** ページを使用すると、エラー処理オプションを選択したり、エラー出力列のプロパティを設定したりできます。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW の SAP BW 変換元コンポーネントの詳細については、「 [SAP BW Source](../../integration-services/data-flow/sap-bw-source.md)」(SAP BW 変換元) をご覧ください。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW に関するドキュメントでは、SAP Netweaver BW 環境について理解していることを前提としています。 SAP Netweaver BW の詳細または SAP Netweaver BW オブジェクトやプロセスを構成する方法については、SAP のマニュアルを参照してください。  
  
> [!IMPORTANT]  
>  SAP Netweaver BW からデータを抽出するには、追加の SAP のライセンスが必要です。 これらの要件を確認するには、SAP にお問い合わせください。  
  
 **[エラー出力] ページを開くには**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、SAP BW 変換元が含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを開きます。  
  
2.  **[データ フロー]** タブで、SAP BW 変換元をダブルクリックします。  
  
3.  **[SAP BW 変換元エディター]** で、 **[エラー出力]** をクリックして **[エラー出力]** ページを開きます。  
  
## <a name="options"></a>オプション  
  
> [!NOTE]  
>  変換元を構成するために必要な値がわからない場合は、SAP 管理者に確認してください。  
  
 **入力または出力**  
 データ ソースの名前を表示します。  
  
 **列**  
 **[SAP BW 変換元エディター]** ダイアログ ボックスの **[列]** ページで選択した外部 (ソース) 列を表示します。 このダイアログ ボックスの詳細については、「 [SAP BW 変換元エディター &#40;[列] ページ&#41;](../../integration-services/data-flow/sap-bw-source-editor-columns-page.md)」(SAP BW 変換元) をご覧ください。  
  
 **Error**  
 SAP BW 変換元コンポーネントが、エラーが発生した場合に障害を無視するか、行をリダイレクトするか、コンポーネントを失敗させるかを指定します。  
  
 **切り捨て**  
 SAP BW 変換元コンポーネントが、切り捨てが発生した場合に障害を無視するか、行をリダイレクトするか、コンポーネントを失敗させるかを指定します。  
  
 **[説明]**  
 エラーの説明を表示します。  
  
 **[選択したセルに設定する値]**  
 SAP BW 変換元コンポーネントが、エラーまたは切り捨てが発生した場合に、選択したすべてのセルに対して障害を無視するか、行をリダイレクトするか、コンポーネントを失敗させるかを指定します。  
  
 **[適用]**  
 選択したセルにエラー処理オプションを適用します。  
  
## <a name="see-also"></a>参照  
 [SAP BW 変換元エディター &#40;[接続マネージャー] ページ&#41;](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md)   
 [SAP BW 変換元エディター &#40;[列] ページ&#41;](../../integration-services/data-flow/sap-bw-source-editor-columns-page.md)   
 [SAP BW 変換元エディター &#40;[詳細設定] ページ&#41;](../../integration-services/data-flow/sap-bw-source-editor-advanced-page.md)   
 [Microsoft Connector for SAP BW の F1 ヘルプ](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
