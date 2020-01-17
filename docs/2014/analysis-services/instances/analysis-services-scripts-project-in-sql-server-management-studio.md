---
title: Analysis Services の SQL Server Management Studio でのスクリプト プロジェクト |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- scripts [Analysis Services]
- scripts [Analysis Services], projects
- projects [Analysis Services], Analysis Server Scripts project
- projects [Analysis Services], creating
- Analysis Server Scripts project
- items [Analysis Services]
ms.assetid: c4f5a06b-e2e4-4660-a3a8-6fd356742c02
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c0bcc06655333dfef073757218d9a740c1dfb0dd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66080354"
---
# <a name="analysis-services-scripts-project-in-sql-server-management-studio"></a>SQL Server Management Studio での Analysis Services スクリプト プロジェクト
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]では、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] に Analysis Services スクリプト プロジェクトを作成し、開発、管理、およびソース管理の目的のために、関連するスクリプトをグループにまとめることができます。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]に読み込まれているソリューションがない場合は、新しい Analysis Services スクリプト プロジェクトを作成すると自動的に新しいソリューションが作成されます。 ソリューションが SQL Server Management Studio に読み込まれている場合は、既存のソリューションに新しい Analysis Services スクリプト プロジェクトを追加するか、または新しいソリューションで Analysis Services スクリプト プロジェクトを作成できます。  
  
 次の基本的な手順を使用して、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で Analysis Services スクリプト プロジェクトを作成します。  
  
1.  [ファイル] メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。  
  
     **[Analysis Services スクリプト]** プロジェクト テンプレートをクリックし、新しいプロジェクトの名前と場所を指定します。  
  
2.  **[接続]** を右クリックし、ソリューション エクスプローラーの Analysis Services スクリプト プロジェクトの [接続] フォルダーに新しい接続を作成します。  
  
     このフォルダーには [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスへの接続文字列が含まれます。このインスタンスに対して Analysis Services スクリプト プロジェクトに含まれるスクリプトを実行できます。 Analysis Services スクリプト プロジェクトには複数の接続を含めることができ、プロジェクトに含まれているスクリプトをどの接続に対して実行するかを実行時に選択できます。  
  
3.  **[クエリ]** を右クリックし、多次元式 (MDX)、データ マイニング拡張機能 (DMX)、および XML for Analysis (XMLA) スクリプトを、ソリューション エクスプローラーの Analysis Services スクリプト プロジェクトの [スクリプト] フォルダーに作成します。 詳細については、「 [Analysis Services の管理タスクのスクリプト作成](../script-administrative-tasks-in-analysis-services.md)」を参照してください。  
  
4.  プロジェクトを右クリックし、 **[追加]** をポイントします。次に、 **[既存の項目]** をクリックしてプロジェクトの注釈が書かれているテキスト ファイルなどのその他のファイルを、ソリューション エクスプローラーの Analysis Services スクリプト プロジェクトの **[その他]** フォルダーに追加します。 これらのファイルは、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]では無視されます。  
  
## <a name="file-types"></a>ファイルの種類  
 1 つの [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ソリューションで、複数のファイルの種類を使用できます。ファイルの種類は、ソリューションに含まれるプロジェクトおよびそのソリューションの各プロジェクトに含まれるアイテムによって異なります。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でのソリューション用のファイルの種類については、「 [ソリューションとプロジェクトを管理するためのファイル](../../ssms/solution/files-that-manage-solutions-and-projects.md)」を参照してください。 通常、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ソリューションの各プロジェクトのファイルは、ソリューションのフォルダー内でプロジェクト別に異なるフォルダーに保存されます。  
  
 Analysis Services スクリプト プロジェクトのプロジェクト フォルダーには、次の表に示す種類のファイルを格納できます。  
  
|ファイルの種類|説明|  
|---------------|-----------------|  
|Analysis Services スクリプト プロジェクト定義ファイル (.ssmsasproj)|ソリューション エクスプローラーに表示されるフォルダーに関するメタデータ、およびプロジェクトに含まれるファイルをどのフォルダーが表示するかを示す情報が含まれます。<br /><br /> また、プロジェクトに含まれる [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 接続のメタデータ、およびプロジェクトに含まれるスクリプト ファイルに接続を関連付けるメタデータも含まれます。|  
|DMX スクリプト ファイル (.dmx)|プロジェクトに含まれている DMX スクリプトが含まれます。|  
|MDX スクリプト ファイル (.mdx)|プロジェクトに含まれている MDX スクリプトが含まれます。|  
|XMLA スクリプト ファイル (.xmla)|プロジェクトに含まれている XMLA スクリプトが含まれます。|  
  
## <a name="analysis-services-templates"></a>Analysis Services テンプレート  
 新しい MDX、DMX、または XMLA スクリプトを Analysis Services スクリプト プロジェクトに追加する場合は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] テンプレートの参照にテンプレート エクスプローラーを必要に応じて使用してください。このテンプレートは、具体的なアクションの実行方法を例示した事前定義済みのスクリプトまたはステートメントのコレクションです。 テンプレート エクスプローラーには、 **[表示]** メニューからアクセスでき、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、および [!INCLUDE[ssEW](../../includes/ssew-md.md)]のテンプレートが含まれています。 詳細については、「 [SQL Server Management Studio での Analysis Services テンプレートの使用](use-analysis-services-templates-in-sql-server-management-studio.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server データ ツール &#40;SSDT&#41; を使用した多次元モデルの作成](../multidimensional-models/creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)   
 [多次元式 &#40;MDX&#41; リファレンス](/sql/mdx/multidimensional-expressions-mdx-reference)   
 [データ マイニング拡張機能 &#40;DMX&#41; リファレンス](/sql/dmx/data-mining-extensions-dmx-reference)   
 [Analysis Services スクリプト言語&#40;ASSL&#41;リファレンス](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)   
 [Analysis Services スクリプト言語&#40;ASSL&#41;リファレンス](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)  
  
  
