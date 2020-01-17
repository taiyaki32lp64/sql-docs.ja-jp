---
title: データ ソース (SSAS 多次元) のサポート |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Analysis Services, data sources
- data sources [Analysis Services], about data sources
- Analysis Services, data sources
- connections [Analysis Services]
- SSAS, data sources
ms.assetid: c97e0f8d-7ddd-4941-8b51-e7832f30fbbe
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5a8cdeb912d1ead21571f1ec7f86e15b0d009514
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66072857"
---
# <a name="data-sources-supported-ssas-multidimensional"></a>データ ソースのサポートの (SSAS 多次元)
  このトピックでは、多次元モデルで使用できるデータ ソースの種類について説明します。  
  
##  <a name="bkmk_supported_ds"></a> サポートされるデータ ソース  
 次の表のデータ ソースからデータを取得できます。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]をインストールする際のセットアップで、各データ ソースに対して挙げられているプロバイダーはインストールされません。 プロバイダーは、他のアプリケーションと共にコンピューターに既にインストールされている場合もあれば、プロバイダーをダウンロードしてインストールしなくてはならない場合もあります。  
  
> [!NOTE]  
>  Oracle OLE DB プロバイダーなどのサード パーティ プロバイダーを使用して、サード パーティ製データベースと接続することもできます。ただし、その場合は、プロバイダーの提供元が使用するデータベースをサポートしていることが条件となります。  
  
|||||  
|-|-|-|-|  
|ソース|バージョン|ファイルの種類|プロバイダー <sup>1</sup>|  
|Access データベース|Microsoft Access 2007、2010、2013|.accdb または .mdb|Microsoft Jet 4.0 OLE DB Provider|  
|SQL Server リレーショナル データベース<sup>5</sup>|Microsoft SQL Server 2005、2008、2008 R2、2012、2014 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] <sup>2</sup>、SQL Server 並列データ ウェアハウス (PDW) <sup>3</sup>|(該当なし)|OLE DB Provider for SQL Server<br /><br /> SQL Server Native Client OLE DB プロバイダー<br /><br /> SQL Server Native 11.0 Client OLE DB プロバイダー<br /><br /> .NET Framework Data Provider for SQL Client|  
|Oracle リレーショナル データベース|Oracle 9i、10g、11g|(該当なし)|Oracle OLE DB プロバイダー<br /><br /> .NET Framework Data Provider for Oracle Client<br /><br /> .NET Framework Data Provider for SQL Server<br /><br /> MSDAORA OLE DB プロバイダー <sup>4</sup><br /><br /> OraOLEDB<br /><br /> MSDASQL|  
|Teradata リレーショナル データベース|Teradata V2R6、V12|(該当なし)|TDOLEDB OLE DB プロバイダー<br /><br /> .Net Data Provider for Teradata|  
|Informix リレーショナル データベース|V11.10|(該当なし)|Informix OLE DB プロバイダー|  
|IBM DB2 リレーショナル データベース|8.1|(該当なし)|DB2OLEDB|  
|Sybase Adaptive Server Enterprise (ASE) リレーショナル データベース|15.0.2|(該当なし)|Sybase OLE DB プロバイダー|  
|その他のリレーショナル データベース|(該当なし)|(該当なし)|OLE DB プロバイダー|  
  
 <sup>1</sup>多次元ソリューションの ODBC データ ソースはサポートされていません。 Analysis Services 自体が接続を処理しますが、MSDASQL ドライバーを使用している場合でも、ソリューションの作成に使用される [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] のデザイナーは ODBC データ ソースには接続できません。 ビジネス要件に ODBC データ ソースが含まれている場合は、代わりに表形式のソリューションを作成することを検討してください。  
  
 <sup>2</sup>詳細については、次を参照してください。[!INCLUDE[ssSDS](../../includes/sssds-md.md)]の[azure.microsoft.com](https://go.microsoft.com/fwlink/?LinkID=157856)します。  
  
 <sup>3</sup>の詳細については[!INCLUDE[ssSDS](../../includes/sssds-md.md)]PDW を参照してください[SQL Server 並列データ ウェアハウス](https://go.microsoft.com/fwlink/?LinkId=150895)します。  
  
 <sup>4</sup>場合によっては、MSDAORA OLE DB プロバイダーを使用して新しいバージョンの Oracle との接続エラーで結果ことができます。 エラーが生じる場合は、Oracle 用に記載されている他のプロバイダーを使用することをお勧めします。  
  
 <sup>5</sup>一部の機能がオンプレミスで実行する SQL Server リレーショナル データベースが必要です。 具体的には、書き戻しと ROLAP ストレージでは、基になるデータ ソースが SQL Server リレーショナル データベースであることが必要です。  
  
## <a name="see-also"></a>参照  
 [サポートされているデータ ソース &#40;SSAS テーブル&#41;](../tabular-models/data-sources-supported-ssas-tabular.md)   
 [多次元モデルのデータ ソース](data-sources-in-multidimensional-models.md)   
 [多次元モデルのデータ ソース ビュー](data-source-views-in-multidimensional-models.md)  
  
  
