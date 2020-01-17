---
title: リレーショナル データ ソース (SSAS テーブル) からのインポート |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 043201cc-fbef-4ed0-bde8-dc5e3a3e8bea
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 61fb30ea21ea810eab8d30a3a040fac4a1bd2128
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66080531"
---
# <a name="import-from-a-relational-data-source-ssas-tabular"></a>リレーショナル データ ソースからのインポート (SSAS テーブル)
  テーブルのインポート ウィザードを使用して、さまざまなリレーショナル データベースからデータをインポートできます。 このウィザードは、 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]の **[モデル]** メニューで使用できます。 データ ソースに接続するには、適切なプロバイダーがコンピューターにインストールされている必要があります。 サポートされているデータ ソースおよびプロバイダーの詳細については、「 [サポートされているデータ ソース (SSAS テーブル)](tabular-models/data-sources-supported-ssas-tabular.md)」を参照してください。  
  
 テーブルのインポート ウィザードでは、次のデータ ソースからのデータのインポートがサポートされています。  
  
 **リレーショナル データベース**  
  
-   Microsoft SQL Server データベース  
  
-   Microsoft SQL Azure  
  
-   Microsoft Access データベース  
  
-   Microsoft SQL Server 並列データ ウェアハウス  
  
-   Oracle  
  
-   Teradata  
  
-   Sybase  
  
-   Informix  
  
-   IBM DB2  
  
-   OLE DB/ODBC  
  
 **多次元ソース**  
  
-   Microsoft SQL Server Analysis Services キューブ  
  
 テーブルのインポート ウィザードでは、 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] ブックをデータ ソースとするデータのインポートはサポートされません。  
  
### <a name="to-import-data-from-a-database"></a>データベースからのデータをインポートするには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で **[モデル]** メニューをクリックし、 **[データ ソースからのインポート]** をクリックします。  
  
2.  **[データ ソースへの接続]** ページで接続するデータベースの種類を選択し、 **[次へ]** をクリックします。  
  
3.  テーブルのインポート ウィザードの手順に従って操作します。 後続のページでは、 **[テーブルとビューの選択]** ページを使用するか、または **[SQL クエリの指定]** ページで SQL クエリを作成することにより、特定のテーブルおよびビューの選択や、フィルターの適用を行うことができます。  
  
## <a name="see-also"></a>参照  
 [データのインポート (SSAS テーブル)](import-data-ssas-tabular.md)   
 [サポートされているデータ ソース (SSAS テーブル)](tabular-models/data-sources-supported-ssas-tabular.md)  
  
  
