---
title: PowerPivot データ更新 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- unattended data refresh [Analysis Services with SharePoint]
- scheduled data refresh [Analysis Services with SharePoint]
- data refresh [Analysis Services with SharePoint]
ms.assetid: ac8358a3-ee71-44c7-8ee6-ac7afe3ebaa4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4ab42604fabaa188a74858038e35a8b90a105df8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66071217"
---
# <a name="powerpivot-data-refresh"></a>PowerPivot のデータ更新
  PowerPivot データを含むブックを作成したら、最初にブックを作成するときに使用したソースから更新情報を取得するクエリまたはコマンドを再実行して、定期的にデータを更新することができます。 このプロセスは `data refresh` と呼ばれます。データ更新は、[!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] で要求時に実行したり、SharePoint ファーム内のアプリケーション サーバーで [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロセスとして実行される定期的な操作として実行したりすることができます。 詳細については、以下をご覧ください。  
  
-   [SharePoint 2010 での PowerPivot データ更新](../powerpivot-data-refresh-with-sharepoint-2010.md)  
  
-   [構成、PowerPivot 自動データ更新アカウント&#40;PowerPivot for SharePoint&#41;](../configure-unattended-data-refresh-account-powerpivot-sharepoint.md)  
  
-   [PowerPivot データ更新用の保存された資格情報の構成&#40;PowerPivot for SharePoint&#41;](../configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)  
  
-   [データ更新のスケジュール&#40;PowerPivot for SharePoint&#41;](../schedule-a-data-refresh-powerpivot-for-sharepoint.md)  
  
-   [データ更新履歴表示&#40;PowerPivot for SharePoint&#41;](view-data-refresh-history-power-pivot-for-sharepoint.md)  
  
> [!NOTE]
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] および SharePoint Server 2013 の Excel Services では、PowerPivot データ モデルのデータ更新に異なるアーキテクチャを使用しています。 SharePoint 2013 でサポートされているアーキテクチャでは、PowerPivot データ モデルを読み込むための主要なコンポーネントとして Excel Services が使用されます。 以前に使用されていたデータ更新のアーキテクチャでは、データ モデルを読み込むために、SharePoint モードで PowerPivot System サービスおよび [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] を実行しているサーバーが使用されていました。 詳細については、以下を参照してください。  
> 
>  -   [SharePoint 2013 での PowerPivot データ更新](power-pivot-data-refresh-with-sharepoint-2013.md)  
> -   [ブックのアップグレードと定期データ更新 &#40;SharePoint 2013&#41;](../instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)  
  
  
