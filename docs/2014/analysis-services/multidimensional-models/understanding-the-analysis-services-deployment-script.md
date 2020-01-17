---
title: サービス配置スクリプトの分析の理解 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services Deployment Wizard, scripts
- deploying [Analysis Services], scripts
- Analysis Services deployments, scripts
- scripts [Analysis Services], deployment
ms.assetid: a63ebee9-9848-48f1-82ad-64ecf2e47019
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a9436d33cdc99cf979509a40f06ceea15c0cd765
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66072657"
---
# <a name="understanding-the-analysis-services-deployment-script"></a>Analysis Services 配置スクリプトについて
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 配置ウィザードによって生成される XMLA 配置スクリプトは、次の 2 つのセクションで構成されています。  
  
-   配置スクリプトの最初の部分には、配置先のデータベースで適切な [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトを作成、変更、または削除するために必要なコマンドが含まれています。 既定では、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトで生成される入力ファイルは、増分配置に基づいています。 そのため、XMLA 配置スクリプトは、変更または削除されたオブジェクトにしか影響しません。  
  
-   配置スクリプトの 2 番目の部分には、配置先サーバー上で作成または変更されたオブジェクトのみを処理するために必要なコマンド (既定の処理のオプション)、または配置先データベースを完全に処理するために必要なコマンドが含まれています。 また、配置スクリプトに処理コマンドを含めないこともできます。  
  
 配置スクリプト全体は、単一のトランザクションまたは複数のトランザクションで実行できます。 スクリプトを複数のトランザクションで実行する場合は、スクリプトの最初の部分が単一のトランザクションとして実行され、各オブジェクトはそれぞれのトランザクションで処理されます。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 配置ウィザードでは、単一の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースへのオブジェクトの配置のみを行います。 サーバー レベルのオブジェクトまたはデータは配置しません。  
  
## <a name="see-also"></a>参照  
 [Analysis Services 配置ウィザードの実行](running-the-analysis-services-deployment-wizard.md)   
 [配置スクリプトを作成するための入力ファイルについて](deployment-script-files-input-used-to-create-deployment-script.md)  
  
  
