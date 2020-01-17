---
title: 多次元データベース (Analysis Services) の名前変更 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- renaming databases
ms.assetid: 15fdaec7-f3e4-44d9-9b78-1a1d78c484e0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 28ec21d4cb0cda01852316c1198bd68df3058ffc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66073148"
---
# <a name="rename-a-multidimensional-database-analysis-services"></a>多次元データベース名の変更 (Analysis Services)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースの名前を変更する方法は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースへの接続方法によって異なります。 既存のデータベースの名前を変更するには、オンライン モードでデータベースに接続する必要があります。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクト内のオブジェクトがインスタンス化されるデータベースの名前を変更するには、プロジェクト モードで接続する必要があります。  
  
### <a name="to-change-the-database-name-in-online-mode"></a>オンライン モードでデータベース名を変更するには  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]を使用して、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースに直接接続します。  
  
2.  ソリューション エクスプローラーでデータベースを右クリックし、 **[データベースの編集]** をクリックします。  
  
3.  **[データベース名]** ボックスでデータベース名を変更します。  
  
4.  ツール バーの **[保存]** または **[すべてを保存]** をクリックし、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** または **[すべてを保存]** をクリックします。あるいは、 **データベース デザイナー** を終了し、メッセージが表示されたら **[保存]** をクリックします。  
  
     [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスのデータベース名が更新され、ソリューション エクスプローラーのデータベース オブジェクトが更新されます。  
  
### <a name="to-change-the-database-name-in-project-mode"></a>プロジェクト モードでデータベース名を変更するには  
  
1.  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトを右クリックし、 **[プロパティ]** をクリックします。  
  
3.  **[プロパティ ページ]** ダイアログ ボックスで、 **[構成プロパティ]** セクションの **[配置]** をクリックします。  
  
4.  **[データベース]** プロパティを新しいデータベース名に変更します。  
  
     次回 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトが配置されるときには、この新しい名前のデータベースにプロジェクトが配置されます。 この名前のデータベースが既に存在する場合は上書きされます。  
  
### <a name="to-change-the-database-name-using-sql-server-management-studio"></a>SQL Server Management Studio を使用してデータベース名を変更するには  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースを右クリックし、Name プロパティを編集します。  
  
## <a name="see-also"></a>参照  
 [Analysis services サーバーのプロパティを構成します。](../server-properties/server-properties-in-analysis-services.md)   
 [多次元データベースのプロパティ設定 (Analysis Services)](set-multidimensional-database-properties-analysis-services.md)   
 [Analysis Services プロジェクトのプロパティの構成 (SSDT)](configure-analysis-services-project-properties-ssdt.md)   
 [Analysis Services プロジェクトの配置 (SSDT)](deploy-analysis-services-projects-ssdt.md)  
  
  
