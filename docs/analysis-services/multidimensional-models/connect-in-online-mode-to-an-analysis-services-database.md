---
title: "Analysis Services データベースをオンライン モードで接続 |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Analysis Services, connecting
ms.assetid: 33041234-7106-404f-a289-8e904f32aff2
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 626d0643a170f96850c6c274d64694e86e4663a3
ms.contentlocale: ja-jp
ms.lasthandoff: 09/01/2017

---
# <a name="connect-in-online-mode-to-an-analysis-services-database"></a>Analysis Services データベースへのオンライン モードでの接続
  既存の [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースに直接接続すると、そのデータベース内のオブジェクトを直接変更できます。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースに直接接続すると、オブジェクトに対する変更処理が直ちに行われ、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトは [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]内に作成されません。  
  
### <a name="to-connect-directly-to-an-analysis-services-database-by-using-sql-server-data-tools"></a>SQL Server データ ツールを使用して Analysis Services データベースに直接接続するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]を開きます。  
  
2.  **[ファイル]** メニューの **[開く]** をポイントし、 **[Analysis Services データベース]**をクリックします。  
  
3.  **[既存のデータベースに接続する]**を選択します。  
  
4.  サーバー名とデータベース名を指定します。  
  
     データベース名は直接入力することも、サーバーをクエリして、サーバー上の既存のデータベースを表示してから選択することもできます。  
  
5.  **[OK]**をクリックします。  
  
     [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベース内のオブジェクトを直接編集できるようになりました。  
  
## <a name="see-also"></a>参照  
 [開発段階における Analysis Services プロジェクトおよびデータベースの操作](../../analysis-services/multidimensional-models/work-with-analysis-services-projects-and-databases-in-development.md)   
 [SQL Server Data Tools &#40; を使用して多次元モデルを作成します。SSDT &#41;](../../analysis-services/multidimensional-models/creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)  
  
  