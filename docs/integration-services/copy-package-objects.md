---
title: パッケージ オブジェクトをコピーする | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- control flow [Integration Services], copying objects
- copying package objects [Integration Services]
- data flow [Integration Services], copying objects
- connection managers [Integration Services], copying
ms.assetid: 99b85e5c-d6bd-4e7c-afe4-51f6ce151c2f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4636dde3123cc3742a7dde57fa2a468583e2f2bd
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293600"
---
# <a name="copy-package-objects"></a>パッケージ オブジェクトをコピーする

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  このトピックでは、制御フロー アイテム、データ フロー アイテム、および接続マネージャーをパッケージ内またはパッケージ間でコピーする方法について説明します。  
  
### <a name="to-copy-control-and-data-flow-items"></a>制御フロー アイテムおよびデータ フロー アイテムをコピーするには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、作業対象とするパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、コピー元とコピー先のパッケージをダブルクリックします。  
  
3.  [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーで、コピーするアイテムを含むパッケージのタブをクリックし、 **[制御フロー]** タブ、 **[データ フロー]** タブ、または **[イベント ハンドラー]** タブをクリックします。  
  
4.  コピーする制御フロー アイテムまたはデータ フロー アイテムを選択します。 アイテムは、Shift キーを押しながらアイテムをクリックして 1 つずつ選択することも、選択する複数のアイテムをポインターでドラッグしてグループとして選択することもできます。  
  
    > [!IMPORTANT]  
    >  アイテムを連結する優先順位制約およびパスは、連結する 2 つのアイテムを選択しても自動的には選択されません。 順序付けられたワークフロー (制御フローやデータ フローの一部) をコピーするには、必ず優先順位制約およびパスもコピーします。  
  
5.  選択したアイテムを右クリックし、 **[コピー]** をクリックします。  
  
6.  アイテムを別のパッケージにコピーする場合は、コピー先のパッケージをクリックし、アイテムの種類に適したタブをクリックします。  
  
    > [!IMPORTANT]  
    >  データ フロー タスクが 1 つもパッケージに含まれていない場合は、データ フローをパッケージにコピーできません。  
  
7.  右クリックして **[貼り付け]** をクリックします。  
  
### <a name="to-copy-connection-managers"></a>接続マネージャーをコピーするには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、作業対象とするパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックします。  
  
3.  [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーの **[制御フロー]** タブ、 **[データ フロー]** タブ、または **[イベント ハンドラー]** タブをクリックします。  
  
4.  **[接続マネージャー]** 領域で、接続マネージャーを右クリックし、 **[コピー]** をクリックします。 接続マネージャーは、一度に 1 つしかコピーできません。  
  
5.  アイテムを別のパッケージにコピーしている場合は、コピー先のパッケージをクリックし、 **[制御フロー]** タブ、 **[データ フロー]** タブ、または **[イベント ハンドラー]** タブをクリックします。  
  
6.  **[接続マネージャー]** 領域を右クリックして、 **[貼り付け]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [[制御フロー]](../integration-services/control-flow/control-flow.md)   
 [[データ フロー]](../integration-services/data-flow/data-flow.md)   
 [Integration Services &#40;SSIS&#41; の接続](../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [プロジェクト アイテムをコピーする](https://msdn.microsoft.com/library/1606c54d-20f9-49f3-a4ef-caad83a772aa)  
  
  
