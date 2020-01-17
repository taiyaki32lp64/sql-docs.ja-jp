---
title: ソリューション エクスプ ローラー (SSAS 多次元) でのデータ ソースの削除 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.deleteobjects.f1
helpviewer_keywords:
- data sources [Analysis Services], deleting
- deleting data sources
- removing data sources
ms.assetid: b45441ef-f909-4736-98b9-cc80d0acac99
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1e3b6dc676c11444c8dd45d1874f77942316a462
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66075499"
---
# <a name="delete-a-data-source-in-solution-explorer-ssas-multidimensional"></a>ソリューション エクスプローラーでのデータ ソースの削除 (SSAS 多次元)
  データ ソース オブジェクトを削除して、Analysis Services 多次元モデル プロジェクトから完全に消去することができます。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]では、データ ソースに基づいてデータ ソース ビューが作成されます。さらに、そのデータ ソース ビューを使用して、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のプロジェクトまたはデータベースのディメンション、キューブ、マイニング構造が定義されます。 したがって、データ ソースを削除すると、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクト内の他の [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] オブジェクトが無効になる場合があります。 オブジェクトを削除する前に提供される依存オブジェクトの一覧を、常に確認する必要があります。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によってオンライン モードで開かれている [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] データベースから、他のオブジェクトが依存しているデータ ソースを削除することはできません。 データ ソースを削除する前に、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベース内でそのデータ ソースに依存しているすべてのオブジェクトを削除する必要があります。 オンライン モードの詳細については、「 [Analysis Services データベースへのオンライン モードでの接続](connect-in-online-mode-to-an-analysis-services-database.md)」を参照してください。  
  
### <a name="to-delete-a-data-source"></a>データ ソースを削除するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]でプロジェクトを開くか、データ ソースを削除するデータベースに接続します。  
  
2.  **ソリューション エクスプローラー**で **[データ ソース]** フォルダーを展開します。  
  
3.  データ ソースを右クリックし、 **[削除]** をクリックします。 **[オブジェクトの削除]**  ダイアログ ボックスが表示され、データ ソースを削除すると無効になるオブジェクトが示されます。 **[OK]** をクリックしてデータ ソースを削除する前に、この一覧を慎重に確認します。  
  
4.  プロジェクトを保存します。  
  
     [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトからデータ ソースを削除した後で、変更されたプロジェクトを保存する必要があります。そうしないと、次回プロジェクトを開くときにエラーが表示されます。これは、プロジェクトで、削除されたデータ ソースを読み込もうとするときに、その基になる XML ファイルがないためです。  
  
## <a name="see-also"></a>関連項目  
 [多次元モデルのデータ ソース](data-sources-in-multidimensional-models.md)   
 [サポートされるデータ ソース&#40;SSAS 多次元&#41;](supported-data-sources-ssas-multidimensional.md)  
  
  
