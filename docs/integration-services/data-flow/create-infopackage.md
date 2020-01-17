---
title: インフォパッケージの作成 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 9cd4a848-409f-4681-a390-1c49a2aadbd7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 25f1497b7801c7891681324b12fa9a5eda4eb842
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293210"
---
# <a name="create-infopackage"></a>インフォパッケージの作成

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  SAP Netweaver BW システムで新しいインフォパッケージを作成するには、 **[インフォパッケージの作成]** ダイアログ ボックスを使用します。  
  
 **[インフォパッケージの作成]** ダイアログ ボックスは、 **[SAP BW 変換先エディター]** の **[接続マネージャー]** ページから開くことができます。 SAP BW 変換先の詳細については、「 [SAP BW Destination](../../integration-services/data-flow/sap-bw-destination.md)」を参照してください。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW に関するドキュメントでは、SAP Netweaver BW 環境について理解していることを前提としています。 SAP Netweaver BW の詳細または SAP Netweaver BW オブジェクトやプロセスを構成する方法については、SAP のマニュアルを参照してください。  
  
 **[インフォパッケージの作成] ダイアログ ボックスを開くには**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、SAP BW 変換先が含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを開きます。  
  
2.  **[データ フロー]** タブで、SAP BW 変換先をダブルクリックします。  
  
3.  **[SAP BW 変換先エディター]** で、 **[接続マネージャー]** をクリックして **[接続マネージャー]** ページを開きます。  
  
4.  **[接続マネージャー]** ページの **[SAP BW オブジェクトの作成]** で、 **[インフォパッケージ]** を選択し、 **[作成]** をクリックします。  
  
## <a name="options"></a>オプション  
 **インフォソース**  
 新しいインフォパッケージの基にするインフォソースの名前を入力します。  
  
 **簡単な説明**  
 新しいインフォパッケージの説明を入力します。  
  
 **転送元システム**  
 インフォパッケージに関連付けるソース システムを選択します。  
  
 **属性**  
 インフォパッケージが属性データを読み込むことを示します。  
  
 **テキスト**  
 インフォパッケージがテキスト データを読み込むことを示します。  
  
 **トランザクション**  
 インフォパッケージがトランザクション データを読み込むことを示します。  
  
 **保存と有効化**  
 新しいインフォパッケージを保存してアクティブ化します。  
  
## <a name="see-also"></a>参照  
 [Microsoft Connector for SAP BW の F1 ヘルプ](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
