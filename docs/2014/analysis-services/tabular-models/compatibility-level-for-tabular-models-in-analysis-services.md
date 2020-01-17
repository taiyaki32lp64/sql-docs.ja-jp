---
title: 互換性レベル (SSAS テーブル SP1) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.versioncompat.f1
ms.assetid: 8943d78d-4a73-4be8-ad14-3d428f5abd06
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 57a1e67db8bcbf17dc964f7341df25a396c36ad0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66067599"
---
# <a name="compatibility-level-ssas-tabular-sp1"></a>互換性レベル (SSAS テーブル SP1)
  指定できる*互換性レベル*、表形式モデル データベースを展開して既存のアップグレード時に、既存のテーブル モデル プロジェクトをアップグレードするときに、新しい表形式モデル プロジェクトを作成するときに、または PowerPivot ブックをインポートするときにします。  
  
## <a name="compatibility-level"></a>互換性レベル  
 通常は、実稼働コンピューターにインストールする前に、開発用コンピューターとテスト用コンピューターに新しいバージョンとサービス パックをインストールします。 このような場合は、新しいテーブル モデル プロジェクトと実稼働環境に既に配置されているテーブル モデル プロジェクトの両方に対する互換性レベルの設定について理解することが重要です。  
  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] の Analysis Services インスタンスは、次の互換性レベル (データベース バージョン) をサポートします。  
  
-   SQL Server 2012 (1100)  
  
-   SQL Server 2012 SP1 (1103)  
  
-   SQL Server 2014 (1103)  
  
### <a name="set-compatibility-level-when-creating-a-new-tabular-model-project"></a>新しいテーブル モデル プロジェクトを作成するときに互換性レベルを設定する  
 SQL Server Data Tools (SSDT) で新しい表形式モデル プロジェクトを作成するときに、**新しい表形式プロジェクト オプション**ダイアログで互換性レベルを指定することができます。 作成した新しいプロジェクトの配置先として、[!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 以降の Analysis Services インスタンス、または SQL Server 2012 Analysis Services インスタンス (Service Pack 1 なし) を選択できます。  
  
 **[今後、このメッセージを表示しない]** オプションを選択することで、既定の互換性レベルを指定することもできます。 以降、すべてのプロジェクトで、指定した互換性レベルが使用されます。 既定の互換性レベルは、SSDT の [オプション] で変更できます。  
  
### <a name="upgrade-an-existing-tabular-model-project-to-1103-compatibility-level"></a>既存のテーブル モデル プロジェクトを 1103 互換性レベルにアップグレードする  
 SSDT でインストールする前に作成された表形式モデル プロジェクトをアップグレードする[!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]以降を使用して、データベースのバージョンを 1103 互換性がある、**互換性レベル**モデル内のプロパティ**プロパティ**ウィンドウ。 テーブル モデル プロジェクトをアップグレードするには、SSDT をインストールするコンピューターに [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 以降がインストールされ、ワークスペース データベースが存在する Analysis Services インスタンス上にも [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 以降がインストールされている必要があります。 以前のバージョンにダウングレードすることはできません。  
  
### <a name="upgrade-a-deployed-tabular-model-database-to-1103-compatibility-level"></a>配置済みテーブル モデル データベースを 1103 互換性レベルにアップグレードする  
 使用して既存の配置済みテーブル モデル データベースへのデータベース バージョン 1103 互換性のある SQL Server Management Studio (SSMS) をアップグレードすることができます、**互換性レベル**プロパティ**データベース プロパティ**. アップグレードするには、SQL Server Analysis Services インスタンスがインストールされるコンピューターに [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 以降がインストールされている必要があります。 配置済みのテーブル モデル データベースを以前のバージョンのインスタンスにダウングレードすることはできません。  
  
### <a name="import-from-powerpivot"></a>PowerPivot からのインポート  
 新しいテーブル モデル プロジェクトを PowerPivot からインポートすることで作成する場合は、互換性レベルを既定の互換性レベルにアップグレードする (SSDT で構成済みの場合) か、PowerPivot ワークブックに既に指定されている互換性のままにするかを指定できます。  
  
### <a name="check-compatibility-level-for-a-tabular-model-database-in-ssms"></a>SSMS のテーブル モデル データベースの互換性レベルを確認する  
 SSMS でのテーブル モデル データベースの互換性レベルを確認するには表示することによって、**互換性レベル**プロパティ (で新しい[!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]) で**データベースのプロパティ**します。  
  
### <a name="check-supported-compatibility-level-for-an-analysis-services-instance-in-ssms"></a>Analysis Services インスタンスでサポートされる互換性レベルを SSMS で確認する  
 SSMS でサポートされる互換性レベルを確認するには表示することによって、**サポートされる互換性レベル**プロパティを**情報**ページ (で新しい[!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]) で**分析サービス プロパティ**します。 サポートされる互換性レベル 1103 は、SQL Server SP1 以降がインストールされていることを示します。 サポートされる互換性レベルは変更できません。  
  
  
