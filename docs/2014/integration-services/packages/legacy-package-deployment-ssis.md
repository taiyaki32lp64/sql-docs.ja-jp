---
title: パッケージの配置 (SSIS) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, deploying
- deploying packages [Integration Services]
- SQL Server Integration Services packages, deploying
- deploying packages [Integration Services], about deploying packages
- packages [Integration Services], deploying
- SSIS packages, deploying
ms.assetid: 0f5fc7be-e37e-4ecd-ba99-697c8ae3436f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c912d4417842bc332262549cc604b97eaa50a44d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62767092"
---
# <a name="package-deployment-ssis"></a>パッケージの配置 (SSIS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、開発コンピューターから実稼働サーバーまたは他のコンピューターへのパッケージの配置を簡素化するツールとウィザードが含まれています。  
  
 パッケージ配置プロセスは、次の 4 段階で行います。  
  
1.  最初の手順は省略可能です。この手順では、実行時にパッケージのプロパティ要素を更新するパッケージ構成を作成します。 この構成は、パッケージを配置する際に自動的に適用されます。  
  
2.  2 番目の手順は、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトをビルドして、パッケージ配置ユーティリティを作成することです。 プロジェクトの配置ユーティリティには、配置するパッケージが含まれます。  
  
3.  3 番目の手順は、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトのビルド時に作成された配置フォルダーをターゲット コンピューターにコピーすることです。  
  
4.  4 番目の手順は、ターゲット コンピューターでパッケージ インストール ウィザードを実行し、ファイル システムまたは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにパッケージをインストールすることです。  
  
## <a name="related-tasks"></a>Related Tasks  
 配置ユーティリティを作成する方法については、「 [Create a Deployment Utility](../create-a-deployment-utility.md)」 (配置ユーティリティの作成) を参照してください。  
  
 配置ユーティリティを使用してパッケージを配置する方法については、「 [配置ユーティリティを使用してパッケージを配置する](../deploy-packages-by-using-the-deployment-utility.md)」を参照してください。  
  
 パッケージ構成を作成する方法の詳細については、「 [パッケージ構成を作成する](../create-package-configurations.md)」を参照してください。  
  
  
