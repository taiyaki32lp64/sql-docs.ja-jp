---
title: 配置ウィザードを使用したモデル ソリューションの配置 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services Deployment Wizard
- deploying [Analysis Services], Analysis Services Deployment Wizard
- Analysis Services deployments, Analysis Services Deployment Wizard
- Analysis Services Deployment Wizard, about Analysis Services Deployment Wizard
ms.assetid: ff711e8e-971c-43ba-b479-effc034af4a4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e18b1786201be9ba671bc08fe7b24ba2207469e9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66075377"
---
# <a name="deploy-model-solutions-using-the-deployment-wizard"></a>Deploy Model Solutions Using the Deployment Wizard
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 配置ウィザードでは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトから生成された XML 出力ファイルを入力ファイルとして使用します。 このような入力ファイルは簡単に変更して、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトの配置をカスタマイズできます。 生成された配置スクリプトは直ちに実行することも、今後の配置のために保存することもできます。  
  
 配置を行うには、ここで説明するウィザードを使用します。 配置を自動化したり、同期機能を使用したりすることもできます。 配置するデータベースが大きい場合は、配置先のシステムでパーティションを使用することを検討してください。 分析管理オブジェクト (AMO) を使用してパーティションの作成および設定を自動化することもできます。  
  
> [!IMPORTANT]  
>  XML 出力ファイルおよび配置スクリプトには、データ ソースへの接続文字列内または権限借用の目的で指定されたユーザー ID またはパスワードは含まれません。 このシナリオの処理ではユーザー ID およびパスワードが必要であるため、この情報を手動で追加します。 配置の際に処理を行わない場合は、この接続および権限借用のための情報を必要に応じて配置後に追加できます。 配置の際に処理を行う場合は、この情報をウィザードで入力するか、保存した配置スクリプトに追加することができます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 次のトピックでは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 配置ウィザードの操作方法、入力ファイル、および配置スクリプトについて説明します。  
  
|トピック|説明|  
|-----------|-----------------|  
|[Analysis Services 配置ウィザードの実行](running-the-analysis-services-deployment-wizard.md)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 配置ウィザードを実行するさまざまな方法について説明します。|  
|[配置スクリプトを作成するための入力ファイルについて](deployment-script-files-input-used-to-create-deployment-script.md)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 配置ウィザードによって入力値として使用されるファイルと、その各ファイルに含まれる内容について説明し、各入力ファイル内の値の変更方法について説明するトピックへのリンクを提供します。|  
|[Analysis Services 配置スクリプトについて](understanding-the-analysis-services-deployment-script.md)|配置スクリプトの内容とスクリプトの実行方法について説明します。|  
  
## <a name="see-also"></a>参照  
 [XMLA を使用したモデル ソリューションの配置](deploy-model-solutions-using-xmla.md)   
 [Analysis Services データベースの同期](synchronize-analysis-services-databases.md)   
 [配置スクリプトを作成するための入力ファイルについて](deployment-script-files-input-used-to-create-deployment-script.md)   
 [配置ユーティリティを使用したモデル ソリューションの配置](deploy-model-solutions-with-the-deployment-utility.md)  
  
  
