---
title: '[SAP BW 変換先エディター] ([マッピング] ページ) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sapbwdestination.columns.f1
ms.assetid: dfa1f1d6-6b64-4331-bdc5-eaa8b7aa41a1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 31c6ab812081d66980002ed0138f5b1ad63f62b5
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298099"
---
# <a name="sap-bw-destination-editor-mappings-page"></a>[SAP BW 変換先エディター] ([マッピング] ページ)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **[SAP BW 変換先エディター]** ダイアログ ボックスの **[マッピング]** ページを使用すると、入力列を変換先列にマップできます。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW の SAP BW 変換先の詳細については、「 [SAP BW 転送先](../../integration-services/data-flow/sap-bw-destination.md)」を参照してください。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW に関するドキュメントでは、SAP Netweaver BW 環境について理解していることを前提としています。 SAP Netweaver BW の詳細または SAP Netweaver BW オブジェクトやプロセスを構成する方法については、SAP のマニュアルを参照してください。  
  
 **[マッピング] ページを開くには**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、SAP BW 変換先が含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを開きます。  
  
2.  **[データ フロー]** タブで、SAP BW 変換先をダブルクリックします。  
  
3.  **[SAP BW 変換先エディター]** で、 **[マッピング]** をクリックして **[マッピング]** ページを開きます。  
  
## <a name="options"></a>オプション  
  
> [!NOTE]  
>  変換先を構成するために必要な値がわからない場合は、SAP 管理者に確認してください。  
  
 **[SAP BW 変換先エディター]** の **[マッピング]** ページは、次の 2 種類のセクションで構成されています。  
  
-   上側のセクションには、使用できる入力列と変換先列が表示され、これらの 2 種類の列の間のマッピングを作成することができます。  
  
-   下側のセクションは、出力列にマップされた入力列のテーブルです。  
  
### <a name="upper-section-options"></a>上側のセクションのオプション  
 上側のセクションには次のオプションがあります。  
  
 **使用できる入力列**  
 使用できる入力列の一覧を表示します。  
  
 変換先列に入力列をマップするには、 **[使用できる変換先列]** の一覧の列に、 **[使用できる入力列]** の一覧から列をドラッグします。  
  
 **[使用できる入力列]**  
 使用できる変換先列の一覧を表示します。  
  
 変換先列に入力列をマップするには、 **[使用できる変換先列]** の一覧の列に、 **[使用できる入力列]** の一覧から列をドラッグします。  
  
 上側のセクションには、背景を右クリックすると開くことができるコンテキスト メニューがあります。 このコンテキスト メニューでは次のオプションが表示されます。  
  
-   **すべてのマッピングを選択**  
  
-   **選択したマッピングの削除**  
  
-   **一致する名前でアイテムをマップする**  
  
### <a name="lower-section-columns"></a>下側のセクションの列  
 下側のセクションはマッピング テーブルで、次の列があります。  
  
 **入力列**  
 選択した入力列を表示します。  
  
 同じマップ先の列に別の入力列をマップするには、リストで別の入力列を選択します。 マッピングを削除するには、 **[\<無視>]** を選択して、出力から入力列を除外します。  
  
 **変換先列**  
 マップされているかどうかにかかわらず、使用できる変換先列を表示します。  
  
## <a name="see-also"></a>参照  
 [SAP BW 変換先エディター &#40;[接続マネージャー] ページ&#41;](../../integration-services/data-flow/sap-bw-destination-editor-connection-manager-page.md)   
 [SAP BW 変換先エディター &#40;[エラー出力] ページ&#41;](../../integration-services/data-flow/sap-bw-destination-editor-error-output-page.md)   
 [SAP BW 変換先エディター &#40;[詳細設定] ページ&#41;](../../integration-services/data-flow/sap-bw-destination-editor-advanced-page.md)   
 [Microsoft Connector for SAP BW の F1 ヘルプ](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
