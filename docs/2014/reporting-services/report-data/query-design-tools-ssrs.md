---
title: レポートデザイナー SQL Server Data Tools のクエリデザインツール (SSRS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- graphical query designer [Reporting Services]
- MDX query designer [Reporting Services]
- text-based query designer [Reporting Services]
- DMX [Reporting Services]
- query designers [Reporting Services]
- generic query designer See text-based query designer
- Reporting Services, query designers
- semantic queries [Reporting Services]
- Report Model Query Designer
ms.assetid: a8139a9d-4aeb-4e64-96f3-564edf60479f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 65294483b65b0df44e7a4b01899319697e441fa1
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68891009"
---
# <a name="query-design-tools-in-report-designer-sql-server-data-tools-ssrs"></a>SQL Server データ ツールのレポート デザイナーのクエリ デザイン ツール (SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には、レポート デザイナーのデータセット クエリを作成するために使用できる、さまざまなクエリ デザイン ツールが用意されています。 処理するデータ ソースの種類によって、特定のクエリ デザイナーが使用できるかどうかが決まります。 さらに、ビジュアル モードで作業するか、クエリ言語で直接作業するか選択可能なモードがあるクエリ デザイナーもあります。 このトピックでは、各ツールを紹介し、それぞれがサポートするデータ ソースの種類を説明します。 ここでは、次のツールについて説明します。  
  
-   [テキストベースのクエリ デザイナー](#Textbased)  
  
-   [グラフィカル クエリ デザイナー](#Graphical)  
  
-   [レポート モデル クエリ デザイナー](#Model)  
  
-   [MDX クエリ デザイナー](#MDX)  
  
-   [DMX クエリ デザイナー](#DMX)  
  
-   [SapNetWeaver BI クエリ デザイナー](#SAPBW)  
  
-   [Hyperion Essbase クエリ デザイナー](#Hyperion)  
  
 レポート サーバー プロジェクト テンプレートまたはレポート サーバー ウィザード プロジェクト テンプレートを使用する場合、クエリ デザイン ツールはすべて [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] のデータ デザイン環境で実行されます。 クエリ デザイナーを使った作業の詳細については、「 [Reporting Services クエリ デザイナー](../reporting-services-query-designers.md)」を参照してください。  
  
##  <a name="Textbased"></a> テキストベースのクエリ デザイナー  
 テキスト ベースのクエリ デザイナーは、サポートされているほとんどのリレーショナル データ ソース ( [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]、Oracle、Teradata、OLE DB、XML、ODBC など) に対して、既定のクエリ作成ツールです。 グラフィカル クエリ デザイナーとは異なり、このクエリ デザイン ツールはクエリ作成時にはクエリ構文を検証しません。 次の図は、テキスト ベースのクエリ デザイナーを示しています。  
  
 ![リレーショナル データのクエリに使用する汎用クエリ デザイナー](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqd-dsaw-sql-generic.gif "リレーショナル データのクエリに使用する汎用クエリ デザイナー")  
  
 複雑なクエリの作成、ストアド プロシージャの使用、XML データのクエリ、および動的クエリの記述には、テキスト ベースのクエリ デザイナーを使用することをお勧めします。 データ ソースに応じて、ツール バーの **[テキストとして編集]** ボタンを切り替えることにより、グラフィカル クエリ デザイナーとテキスト ベースのクエリ デザイナーとを切り替えることができます。 詳細については、「 [テキストベースのクエリ デザイナーのユーザー インターフェイス](../text-based-query-designer-user-interface.md)」を参照してください。  
  
##  <a name="Graphical"></a> グラフィカル クエリ デザイナー  
 グラフィカル クエリ デザイナーは、リレーショナル データベースに対して実行される [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリを作成または修正する場合に使用します。 このクエリ デザイン ツールは、いくつかの [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 製品と、他の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コンポーネントで使用されています。 データ ソースの種類に応じて、Text モード、StoredProcedure モード、および TableDirect モードがサポートされます。 次の図は、グラフィカル クエリ デザイナーを示しています。  
  
 ![SQL クエリのグラフィカル クエリ デザイナー](../media/rsqd-dsaw-sql.gif "SQL クエリのグラフィカル クエリ デザイナー")  
  
 ツール バーの **[テキストとして編集]** ボタンをクリックして、グラフィカル クエリ デザイナーとテキスト ベースのクエリ デザイナーとを切り替えることができます。 詳細については、「 [グラフィカル クエリ デザイナーのユーザー インターフェイス](graphical-query-designer-user-interface.md)」を参照してください。  
  
##  <a name="Model"></a> レポート モデル クエリ デザイナー  
 レポート モデル クエリ デザイナーは、レポート サーバーにパブリッシュされた SMDL レポート モデルに対して実行されるクエリを作成または変更するために使用します。 モデルに対して実行されるレポートは、クリックスルー データ探索をサポートしています。 クエリは実行時にデータ探索のパスを決定します。 次の図は、レポート モデル クエリ デザイナーを示しています。  
  
 ![セマンティック モデル クエリ デザイナーの UI](../media/rsqd-dsawmodel-smql.gif "セマンティック モデル クエリ デザイナーの UI")  
  
 レポート モデル クエリ デザイナーを使用するには、パブリッシュされたモデルを指すデータ ソースを定義する必要があります。 データ ソースのデータセットを定義する際、レポート モデル クエリ デザイナーでデータセット クエリを開くことができます。 レポート モデル クエリ デザイナーは、グラフィカル モードまたはテキスト ベース モードで使用できます。 ツール バーの **[テキストとして編集]** ボタンをクリックして、グラフィカル クエリ デザイナーとテキスト ベースのクエリ デザイナーとを切り替えることができます。 詳細については、「 [レポート モデル クエリ デザイナーのユーザー インターフェイス](report-model-query-designer-user-interface.md)」を参照してください。  
  
##  <a name="MDX"></a> MDX クエリ デザイナー  
 Multidimensional Expression (MDX) クエリ デザイナーは、多次元キューブを持った [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] データ ソースに対して実行されるクエリを作成または修正する場合に使用します。 次の図は、クエリおよびフィルターを定義した後の MDX クエリ デザイナーを示しています。  
  
 ![Analysis Services MDX クエリ デザイナー、デザイン ビュー](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqd-dsawas-mdx-designmode.gif "Analysis Services MDX クエリ デザイナー、デザイン ビュー")  
  
 MDX クエリ デザイナーを使用するには、有効かつ処理済みの利用可能な Analysis Services キューブを持ったデータ ソースを定義する必要があります。 データ ソースのデータセットを定義する際、MDX クエリ デザイナーでクエリを開くことができます。 必要に応じて、ツール バーの MDX ボタンと DMX ボタンを使用し、MDX モードと DMX モードとを切り替えることができます。 詳細については、「 [Analysis Services の MDX クエリ デザイナーのユーザー インターフェイス](analysis-services-mdx-query-designer-user-interface.md)」を参照してください。  
  
##  <a name="DMX"></a> DMX クエリ デザイナー  
 データ マイニング予測式 (DMX) クエリ デザイナーは、マイニング モデルを持つ [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] データ ソースに対して実行されるクエリを作成または修正する場合に使用します。 次の図は、モデルおよび入力テーブルを選択した後の DMX クエリ デザイナーを示しています。  
  
 ![Analysis Services DMX クエリ デザイナー、デザイン ビュー](../media/rsqd-dsawas-dmx-designmode.gif "Analysis Services DMX クエリ デザイナー、デザイン ビュー")  
  
 DMX クエリ デザイナーを使用するには、データ マイニング モデルを利用できる有効なデータ ソースを定義する必要があります。 データ ソースのデータセットを定義する際、DMX クエリ デザイナーでクエリを開くことができます。 必要に応じて、ツール バーの MDX ボタンと DMX ボタンを使用し、MDX モードと DMX モードとを切り替えることができます。 モデルを選択した後、レポートにデータを提供するデータ マイニング予測クエリを作成できます。 詳細については、「 [Analysis Services の DMX クエリ デザイナーのユーザー インターフェイス](analysis-services-dmx-query-designer-user-interface.md)」を参照してください。  
  
##  <a name="SAPBW"></a> Sap NetWeaver BI クエリ デザイナー  
 [!INCLUDE[SAP_DPE_BW_1](../../../includes/sap-dpe-bw-1-md.md)] クエリ デザイナーは、 [!INCLUDE[SAP_DPE_BW_1](../../../includes/sap-dpe-bw-1-md.md)] データベースからデータを取得する場合に使用します。 このクエリ デザイナーを使用するには、少なくとも 1 つの InfoCube、MultiProvider、または Web 対応クエリが定義されている [!INCLUDE[SAP_DPE_BW_1](../../../includes/sap-dpe-bw-1-md.md)] データ ソースが必要です。 次の図は、 [!INCLUDE[SAP_DPE_BW_1](../../../includes/sap-dpe-bw-1-md.md)] クエリ デザイナーを示しています。  
  
 ![デザイン モードで MDX を使用するクエリ デザイナー](../media/rsqd-dssapbw-mdx-designmode.gif "デザイン モードで MDX を使用するクエリ デザイナー")  
  
##  <a name="Hyperion"></a> Hyperion Essbase クエリ デザイナー  
 [!INCLUDE[extEssbase](../../../includes/extessbase-md.md)] クエリ デザイナーは、 [!INCLUDE[extEssbase](../../../includes/extessbase-md.md)] データベースおよびアプリケーションからデータを取得する場合に使用します。 次の図は、 [!INCLUDE[extEssbase](../../../includes/extessbase-md.md)] クエリ デザイナーを示しています。  
  
 ![Hyperion Essbase データ ソースのクエリ デザイナー](../media/rsqd-dshyperionessbase-mdx-designmode.gif "Hyperion Essbase データ ソースのクエリ デザイナー")  
  
 このクエリ デザイナーを使用するには、少なくとも 1 つのデータベースを持つ [!INCLUDE[extEssbase](../../../includes/extessbase-md.md)] データ ソースが必要です。 詳細については、「 [SAP NetWeaver BI Query Designer のユーザー インターフェイス](sap-netweaver-bi-query-designer-user-interface.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [Reporting Services ツール](../tools/reporting-services-tools.md)   
 [レポート&#40;レポートビルダーと SSRS にデータを追加する&#41;](report-datasets-ssrs.md)   
 [Reporting Services のデータ接続、データソース、および接続文字列](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Reporting Services チュートリアル &#40;SSRS&#41;](../reporting-services-tutorials-ssrs.md)   
 [Reporting Services でサポートされるデータ ソース (SSRS)](../create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [埋め込みデータ ソースまたは共有データ ソースを作成する (SSRS)](../create-an-embedded-or-shared-data-source-ssrs.md)  
  
  
