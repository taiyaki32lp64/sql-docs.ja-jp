---
title: '[マスター データのインフォソースの作成] | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: b52a9a89-8380-4a02-8a83-dcfb46ae860e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1fb9be98dbbdf2935fe79c6f579be7ab0e357624
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293197"
---
# <a name="create-infosource-for-master-data"></a>[マスター データのインフォソースの作成]

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  SAP Netweaver BW システムでマスター データ用の新しいインフォソースを作成するには、 **[マスター データのインフォソースの作成]** ダイアログ ボックスを使用します。  
  
 **[マスター データのインフォソースの作成]** ダイアログ ボックスは、 **[SAP BW 変換先エディター]** の **[接続マネージャー]** ページから開くことができます。 SAP BW 変換先の詳細については、「 [SAP BW Destination](../../integration-services/data-flow/sap-bw-destination.md)」を参照してください。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW に関するドキュメントでは、SAP Netweaver BW 環境について理解していることを前提としています。 SAP Netweaver BW の詳細または SAP Netweaver BW オブジェクトやプロセスを構成する方法については、SAP のマニュアルを参照してください。  
  
 **[マスター データのインフォソースの作成] ダイアログ ボックスを開くには**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、SAP BW 変換先が含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを開きます。  
  
2.  **[データ フロー]** タブで、SAP BW 変換先をダブルクリックします。  
  
3.  **[SAP BW 変換先エディター]** で、 **[接続マネージャー]** をクリックして **[接続マネージャー]** ページを開きます。  
  
4.  **[接続マネージャー]** ページの **[SAP BW オブジェクトの作成]** で、 **[インフォソース]** を選択し、 **[作成]** をクリックします。  
  
5.  **[インフォソースの作成]** ダイアログ ボックスで、 **[マスター データ]** を選択して **[OK]** をクリックします。  
  
## <a name="options"></a>オプション  
 **インフォオブジェクトの名前**  
 新しいインフォソースの基にするインフォオブジェクトの名前を入力します。  
  
 **参照**  
 インフォオブジェクトを参照します。 このオプションは、インフォオブジェクトを選択できる **[インフォオブジェクトの参照]** ダイアログ ボックスを開きます。 このダイアログ ボックスの詳細については、「 [インフォオブジェクトの参照](../../integration-services/data-flow/look-up-infoobject.md)」を参照してください。  
  
 インフォオブジェクトを選択すると、選択したインフォオブジェクトの名前が **[インフォオブジェクトの名前]** ボックスに設定されます。  
  
 **[新規作成]**  
 新しいインフォオブジェクトを作成します。 このオプションでは、新しいインフォオブジェクトを作成できる **[新しいインフォオブジェクトの作成]** ダイアログ ボックスを開きます。 このダイアログ ボックスの詳細については、「 [[新しいインフォオブジェクトの作成]](../../integration-services/data-flow/create-new-infoobject.md)」を参照してください。  
  
 インフォオブジェクトを作成すると、新しいインフォオブジェクトの名前が **[インフォオブジェクトの名前]** ボックスに設定されます。  
  
 **簡単な説明**  
 新しいインフォソースの短い説明を入力します。  
  
 **長い説明**  
 新しいインフォソースの長い説明を入力します。  
  
 **転送元システム**  
 新しいインフォソースに関連付ける転送元システムを選択します。  
  
 **アプリケーション**  
 新しいインフォソースに関連付けるアプリケーションの名前を入力します。  
  
 **属性**  
 マスター データが複数の属性で構成されることを示します。  
  
 **テキスト**  
 マスター データが複数の属性で構成されることを示します。  
  
 **保存と有効化**  
 新しいインフォソースを保存してアクティブ化します。  
  
## <a name="see-also"></a>参照  
 [[インフォソースの作成]](../../integration-services/data-flow/create-infosource.md)   
 [Microsoft Connector for SAP BW の F1 ヘルプ](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
