---
title: '[トランザクション データのインフォキューブの作成] | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 673cea01-a260-4fce-a1a0-f73839289805
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 07e92734aebb13d04d715a727c8b2bbe2e0dc785
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293267"
---
# <a name="create-infocube-for-transaction-data"></a>[トランザクション データのインフォキューブの作成]

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  SAP Netweaver BW システムでトランザクション データ用の新しいインフォキューブを作成するには、 **[トランザクション データのインフォキューブの作成]** ダイアログ ボックスを使用します。  
  
 **[トランザクション データのインフォキューブの作成]** ダイアログ ボックスは、 **[SAP BW 変換先エディター]** の **[接続マネージャー]** ページから開くことができます。 SAP BW 変換先の詳細については、「 [SAP BW Destination](../../integration-services/data-flow/sap-bw-destination.md)」を参照してください。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW に関するドキュメントでは、SAP Netweaver BW 環境について理解していることを前提としています。 SAP Netweaver BW の詳細または SAP Netweaver BW オブジェクトやプロセスを構成する方法については、SAP のマニュアルを参照してください。  
  
 **[トランザクション データのインフォキューブの作成] ダイアログ ボックスを開くには**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、SAP BW 変換先が含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを開きます。  
  
2.  **[データ フロー]** タブで、SAP BW 変換先をダブルクリックします。  
  
3.  **[SAP BW 変換先エディター]** で、 **[接続マネージャー]** をクリックして **[接続マネージャー]** ページを開きます。  
  
4.  **[接続マネージャー]** ページの **[SAP BW オブジェクトの作成]** で、 **[インフォキューブ]** を選択し、 **[作成]** をクリックします。  
  
## <a name="general-options"></a>[全般] のオプション  
 **インフォキューブの名前**  
 新しいインフォキューブの名前を入力します。  
  
 **長い説明**  
 新しいインフォキューブの説明を入力します。  
  
 **保存とアクティブ化**  
 新しいインフォキューブを保存してアクティブ化します。  
  
## <a name="infocube-transfer-structure-options"></a>[インフォキューブ転送構造] のオプション  
 [インフォキューブ転送構造] セクションでは、データ フローの列をインフォオブジェクトに関連付けることができます。  
  
 **PipelineElement**  
 SAP BW 変換先に接続されているデータ フローの出力の列を表示します。  
  
 **PipelineDataType**  
 データ フロー列のデータ型を表示します。  
  
 **インフォオブジェクト**  
 データ フロー列に関連付けられているインフォオブジェクトの名前を表示します。  
  
 **[種類]**  
 データ フロー列に関連付けられているインフォオブジェクトの種類を表示します。 次の表に、種類として使用できる値の一覧を示します。  
  
|[値]|[説明]|  
|-----------|-----------------|  
|CHA|特性|  
|UNI|単位|  
|KYF|主要データ|  
|TIM|時間の特性|  
  
 **Iobject - 検索**  
 既存のインフォオブジェクトを現在の行のデータ フロー列に関連付けます。 関連付けを行うには、 **[検索]** をクリックし、 **[インフォオブジェクトの参照]** ダイアログ ボックスを使用して既存のインフォオブジェクトを選択します。 このダイアログ ボックスの詳細については、「 [インフォオブジェクトの参照](../../integration-services/data-flow/look-up-infoobject.md)」を参照してください。  
  
 既存のインフォオブジェクトを選択すると、選択した値が **[インフォオブジェクト]** 列と **[種類]** 列に設定されます。  
  
 **Iobject - 新規**  
 新しいインフォオブジェクトを作成し、現在の行のデータ フロー列に関連付けます。 新しいインフォオブジェクトを作成するには、 **[新規作成]** をクリックし、 **[新しいインフォオブジェクトの作成]** ダイアログ ボックスを使用してインフォオブジェクトを作成します。 このダイアログ ボックスの詳細については、「 [[新しいインフォオブジェクトの作成]](../../integration-services/data-flow/create-new-infoobject.md)」を参照してください。  
  
 新しいインフォオブジェクトを作成すると、新しい値が **[インフォオブジェクト]** 列と **[種類]** 列に設定されます。  
  
 **Iobject - 削除**  
 インフォオブジェクトと現在の行のデータ フロー列との関連付けを削除します。 関連付けを削除するには、 **[削除]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [Microsoft Connector for SAP BW の F1 ヘルプ](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
