---
title: インフォソースの作成 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e7db233b-5464-43de-9d26-6dd24c7ac1b7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1556a98ad812c32c514b8e55ab1ece3e6d7a40e4
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293262"
---
# <a name="create-infosource"></a>[インフォソースの作成]

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **[インフォソースの作成]** ダイアログ ボックスを使用すると、新しいインフォソースを作成できます。 新しいインフォソースを作成するには、 **[トランザクション データのインフォソースの作成]** または **[マスター データのインフォソースの作成]** ダイアログ ボックスを使用します。  
  
 **[インフォソースの作成]** ダイアログ ボックスは、 **[SAP BW 変換先エディター]** の **[接続マネージャー]** ページから開くことができます。 SAP BW 変換先の詳細については、「 [SAP BW Destination](../../integration-services/data-flow/sap-bw-destination.md)」を参照してください。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW に関するドキュメントでは、SAP Netweaver BW 環境について理解していることを前提としています。 SAP Netweaver BW の詳細または SAP Netweaver BW オブジェクトやプロセスを構成する方法については、SAP のマニュアルを参照してください。  
  
 **[インフォソースの作成] ダイアログ ボックスを開くには**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、SAP BW 変換先が含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを開きます。  
  
2.  **[データ フロー]** タブで、SAP BW 変換先をダブルクリックします。  
  
3.  **[SAP BW 変換先エディター]** で、 **[接続マネージャー]** をクリックして **[接続マネージャー]** ページを開きます。  
  
4.  **[接続マネージャー]** ページの **[SAP BW オブジェクトの作成]** で、 **[インフォソース]** を選択し、 **[作成]** をクリックします。  
  
## <a name="options"></a>オプション  
 **トランザクション データ**  
 トランザクション データの新しいインフォソースを作成します。  
  
 このオプションを選択した場合、 **[トランザクション データのインフォソースの作成]** ダイアログ ボックスが表示されます。 新しいインフォソースを作成するには、 **[トランザクション データのインフォソースの作成]** ダイアログ ボックスを使用します。 このダイアログ ボックスの詳細については、「 [[トランザクション データのインフォソースの作成]](../../integration-services/data-flow/create-infosource-for-transaction-data.md)」をご覧ください。  
  
 **マスター データ**  
 マスター データの新しいインフォソースを作成します。  
  
 このオプションを選択した場合、 **[マスター データのインフォソースの作成]** ダイアログ ボックスが表示されます。 新しいインフォソースを作成するには、 **[マスター データのインフォソースの作成]** ダイアログ ボックスを使用します。 このダイアログ ボックスの詳細については、「 [[マスター データのインフォソースの作成]](../../integration-services/data-flow/create-infosource-for-master-data.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [Microsoft Connector for SAP BW の F1 ヘルプ](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
