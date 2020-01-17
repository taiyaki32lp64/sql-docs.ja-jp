---
title: パッケージの再デプロイ |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- redeploying packages [Integration Services]
- deploying packages [Integration Services], redeploying
ms.assetid: 86806efb-8cf4-4f9d-9824-1152cb4c495c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 14edf3c34278ce89686a390c5b69662753ae653d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66056478"
---
# <a name="redeployment-of-packages"></a>パッケージの再配置
  プロジェクトの配置後に、パッケージの機能を更新または拡張し、更新したパッケージを含む [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを再配置する必要がある場合があります。 パッケージの再配置プロセスの一環として、配置ユーティリティに含まれている構成プロパティを見直す必要があります。 たとえば、パッケージの再配置後に構成が変更されないようにする場合などがあります。  
  
## <a name="process-for-redeployment"></a>再配置のプロセス  
 パッケージの更新の終了後、プロジェクトを再構築し、ターゲット コンピューターに配置フォルダーをコピーしてから、パッケージ インストール ウィザードを再度実行します。  
  
 プロジェクトのパッケージの一部だけを更新した場合、プロジェクト全体を再配置する必要がないことがあります。 パッケージの一部だけを配置するために、新しい [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを作成して、このプロジェクトに更新したパッケージを追加し、プロジェクトをビルドして配置できます。 パッケージの構成は、パッケージを別のプロジェクトに追加する際に、自動的にパッケージと共にコピーされます。  
  
## <a name="related-tasks"></a>Related Tasks  
 [配置ユーティリティを使用してパッケージを配置する](../../2014/integration-services/deploy-packages-by-using-the-deployment-utility.md)  
  
  
