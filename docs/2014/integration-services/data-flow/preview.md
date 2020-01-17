---
title: プレビュー | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 551494c4-9e27-4592-9200-c6bf19e80c9a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b0b0f81c5de267d6e85525714d19999920ba9c71
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770968"
---
# <a name="preview"></a>[プレビュー]
  SAP BW 変換元が抽出するデータをプレビューするには、 **[プレビュー]** ダイアログ ボックスを使用します。  
  
> [!IMPORTANT]  
>  **[プレビュー]** オプションは **[SAP BW 変換元エディター]** の **[接続マネージャー]** ページで使用でき、実際にデータを抽出します。 前の抽出以降に変更されたデータのみを抽出するように SAP Netweaver BW を構成している場合、 **[プレビュー]** を選択すると、次の抽出からプレビュー データを除外します。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW の SAP BW 変換元コンポーネントの詳細については、「 [SAP BW 転送元](sap-bw-source.md)」を参照してください。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW に関するドキュメントでは、SAP Netweaver BW 環境について理解していることを前提としています。 SAP Netweaver BW の詳細または SAP Netweaver BW オブジェクトやプロセスを構成する方法については、SAP のマニュアルを参照してください。  
  
> [!IMPORTANT]  
>  SAP Netweaver BW からデータを抽出するには、追加の SAP のライセンスが必要です。 これらの要件を確認するには、SAP にお問い合わせください。  
  
 **[プレビュー] ダイアログ ボックスを開くには**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、SAP BW 変換元が含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを開きます。  
  
2.  **[データ フロー]** タブで、SAP BW 変換元をダブルクリックします。  
  
3.  **[SAP BW 変換元エディター]** で、 **[接続マネージャー]** をクリックして **[接続マネージャー]** ページを開きます。  
  
4.  SAP BW 変換元を構成します。  
  
5.  SAP BW 変換元を構成したら、 **[接続マネージャー]** ページで **[プレビュー]** をクリックし、 **[プレビュー]** ダイアログ ボックスでデータをプレビューします。  
  
    > [!NOTE]  
    >  **[プレビュー]** をクリックすると、 **[要求のログ]** ダイアログ ボックスも表示されます。 このダイアログ ボックスの詳細については、「 [Request Log](request-log.md)」をご覧ください。  
  
## <a name="options"></a>および  
 **[プレビュー]** ダイアログ ボックスには、SAP Netweaver BW システムから要求された行が表示されます。 表示される列は、ソース データで定義された列です。  
  
 このダイアログ ボックスに他のオプションはありません。  
  
## <a name="see-also"></a>参照  
 [SAP BW ソース エディター &#40;[接続マネージャー] ページ&#41;](sap-bw-source-editor-connection-manager-page.md)   
 [Microsoft Connector 1.1 for SAP BW の F1 ヘルプ](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
