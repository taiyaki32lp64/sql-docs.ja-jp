---
title: ドキュメントし、Analysis Services データベースをスクリプト |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- XML for Analysis, scripts
- XMLA, scripts
- scripts [Analysis Services], databases
- documenting databases
- databases [Analysis Services], documenting
- databases [Analysis Services], scripts
ms.assetid: 125044e2-8d36-4733-8743-8bb68ff9aa4e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9284073781a91b21d588684b9071e6179a815613
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66075116"
---
# <a name="document-and-script-an-analysis-services-database"></a>Analysis Services データベースのドキュメントとスクリプトの作成
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースを配置した後、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、データベースのメタデータまたはデータベースに含まれているオブジェクトのメタデータを XML for Analysis (XMLA) スクリプトとして出力できます。 このスクリプトは、新しい **[XMLA クエリ エディター]** ウィンドウ、ファイル、またはクリップボードに出力できます。 XMLA の詳細については、次を参照してください。 [Analysis Services スクリプト言語&#40;ASSL&#41;参照](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)します。  
  
 生成された XMLA スクリプトでは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] スクリプト言語 (ASSL) の要素を使用して、スクリプトに含まれるオブジェクトを定義します。 CREATE スクリプトを生成した場合、結果として得られる XMLA スクリプトには、インスタンスで **データベース構造全体を作成するための XMLA** Create [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] コマンドおよび ASSL 要素が含まれます。 ALTER スクリプトを生成した場合、結果として得られる XMLA スクリプトには、既存の **データベースの構造をスクリプト作成時点のデータベースの状態に復元するための XMLA** Alter [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] コマンドおよび ASSL 要素が含まれます。  
  
 生成された XMLA スクリプトは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースから以下のようなさまざまな用途に使用できます。  
  
-   すべてのデータベース オブジェクトおよび権限を再作成するためのバックアップ スクリプトを維持できます。  
  
-   データベース開発コードを作成または更新できます。  
  
-   既存のスキーマからテスト環境または開発環境を作成できます。  
  
## <a name="see-also"></a>参照  
 [Analysis Services データベースの変更または削除](modify-or-delete-an-analysis-services-database.md)   
 [Alter 要素 (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla)   
 [Create 要素 (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla)  
  
  
