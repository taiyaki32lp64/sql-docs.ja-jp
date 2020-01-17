---
title: XMLA を使用したモデル ソリューションの配置 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- XML scripts [Analysis Services]
- scripts [Analysis Services], deployment
- deploying [Analysis Services], XML scripts
- Analysis Services deployments, XML scripts
ms.assetid: a8cb1837-fcac-4730-bea4-a72cf94d9f7c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 68700aaba6c335bf7fe9686961933eac5c52f8f7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66075372"
---
# <a name="deploy-model-solutions-using-xmla"></a>XMLA を使用したモデル ソリューションの配置
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で、 **[データベースをスクリプト化]** コマンドの **[CREATE]** オプションを使用すると、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベース全体またはデータベースを構成するいずれかのオブジェクトの XML スクリプトを作成できます。 作成したスクリプトは、別のコンピューターで実行し、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースのスキーマ (メタデータ) を再作成できます。 このスクリプトによって、データベース全体が生成されます。スクリプトを使用するときに、既に配置済みのオブジェクトを増分更新するメカニズムはありません。 スクリプトを実行してデータベースを配置したら、新たに作成されたデータベースを処理して、ユーザーが参照できるようにする必要があります。  
  
 **[データベースをスクリプト化]** コマンドの詳細については、「 [Analysis Services データベースのドキュメントとスクリプトの作成](document-and-script-an-analysis-services-database.md)」を参照してください。  
  
## <a name="modifying-object-properties-in-the-xml-script"></a>XML スクリプトのオブジェクト プロパティの変更  
 **[データベースをスクリプト化]** コマンドを使用するとき、データベース オブジェクトの特定のプロパティ (データベース名、データ ソース接続文字列、セキュリティ設定など) を変更することはできません。 これらのプロパティは、スクリプトの生成後にスクリプト内で手動で変更するか、スクリプトの実行後に配置済みのデータベースで変更する必要があります。  
  
> [!IMPORTANT]  
>  XML スクリプトには、データ ソースへの接続文字列内または権限借用の目的で指定されたパスワードは含まれません。 このシナリオの処理ではパスワードが必要であるため、実行前に XML スクリプトに手動でパスワードを追加するか、XML スクリプト実行後にパスワードを追加する必要があります。  
  
## <a name="see-also"></a>参照  
 [Deploy Model Solutions Using the Deployment Wizard](deploy-model-solutions-using-the-deployment-wizard.md)   
 [Analysis Services データベースの同期](synchronize-analysis-services-databases.md)  
  
  
