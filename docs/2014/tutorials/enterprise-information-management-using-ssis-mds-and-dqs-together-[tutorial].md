---
title: SSIS、MDS、および [チュートリアル] の DQS の組み合わせを使用した Enterprise Information Management |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ba09b504-3007-4cb7-8ef8-f01adbf51646
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 47bb74bf5fd35696481a88c4ccc30a8733f257a2
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70153563"
---
# <a name="enterprise-information-management-using-ssis-mds-and-dqs-together-tutorial"></a>SSIS、MDS、DQS の組み合わせを使用した Enterprise Information Management [チュートリアル]
  企業の情報管理には、一般に、企業の枠を超えたデータ統合、データのクレンジング、データ照合による重複項目の削除、データの標準化、データの拡充、法的およびコンプライアンス条件に対するデータの準拠、および必要なすべてのセキュリティ設定によるデータの集中管理などの作業が含まれます。  
  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] では、効果的な Enterprise Information Management (EIM) ソリューションに必要なすべてのコンポーネントが 1 つの製品で提供しています。 EIM ソリューションの構築に役立つ主なコンポーネントは次のとおりです。  
  
-   SQL Server Integration Services  
  
-   SQL Server Data Quality Services  
  
-   SQL Server マスター データ サービス  
  
 SQL Server Integration Services (SSIS) では、ビジネス ワークフロー、データ ウェアハウス、またはマスター データ管理をサポートする包括的な抽出、変換、および読み込み (ETL) のさまざまなソースからデータを統合するための強力な拡張可能プラットフォームを用意しています。 SSIS の概要と一般的な使用方法については、「 [Integration Services の概要](https://msdn.microsoft.com/library/ms141263\(SQL.105\).aspx)」を参照してください。  
  
 SQL Server Data Quality Services (DQS) ではデータのクレンジング、照合、標準化、および拡充が可能なため、ビジネス インテリジェンス、データ ウェアハウス、およびトランザクション処理ワークロードに対して信頼できる情報を提供できます。 DQS のビジネスニーズと DQS が必要に答える方法については、「 [Data Quality Services の概要](https://msdn.microsoft.com/library/ff877917.aspx)」を参照してください。  
  
 SQL Server マスター データ サービス (MDS) の中央データ ハブは、情報の整合性とデータの一貫性がアプリケーション間で変化していないかどうかを確認します。 MDS の重要な機能の簡単な説明については、「[マスターデータサービスの概要](../master-data-services/master-data-services-overview-mds.md)」を参照してください。  
  
 これらの Microsoft EIM テクノロジを使用して EIM ソリューションを実装し、エンタープライズ情報管理 (EIM) を監視[するための包括的なガイダンスについては、「 [EIM Technologies を使用したマスターデータのクレンジングと照合](https://msdn.microsoft.com/library/hh403491.aspx)」ホワイトペーパーを参照してください。:SSIS、DQS、および MDS](https://go.microsoft.com/fwlink/?LinkId=258672)ビデオを統合して、EIM シナリオのすばらしいデモを実現します。  
  
 このチュートリアルでは、SSIS、MDS、および DQS を組み合わせて、Enterprise Information Management (EIM) ソリューションのサンプルを実装する方法について学習します。 まず、DQS を使用してデータ (メタデータ) についてのナレッジを含むナレッジ ベースを作成し、ナレッジ ベースを使用して Excel ファイル内のデータをクレンジングして、データ内の重複項目を特定および削除するようにデータを照合します。 次に、Excel 用の MDS アドインを使用して、クレンジングおよび照合済みのデータを MDS にアップロードします。 次に、SSIS ソリューションを使用して全体のプロセスを自動化します。 このチュートリアルの SSIS ソリューションでは、Excel ファイルから入力データを読み取りますが、Oracle、Teradata、DB2、Azure SQL Database などのさまざまなソースから読み取ることができます。  
  
## <a name="prerequisites"></a>前提条件  
  
1.  Microsoft SQL Server 2012 に次のコンポーネントがインストールされていること。  
  
    1.  Integration Services (SSIS)  
  
    2.  マスター データ サービス (MDS)  
  
    3.  Data Quality Services (DQS)  
  
    4.  SQL Server Data Tools  
  
         製品のインストールの詳細については、 [SQL Server 2012 のインストールガイド](../database-engine/install-windows/installation-for-sql-server.md)を参照してください。  
  
2.  [マスターデータサービス構成マネージャーを使用して MDS を構成する](https://msdn.microsoft.com/library/ee633884.aspx)  
  
     マスター データ サービス データベースの作成と構成には、構成マネージャーを使用します。 Mds データベースを作成した後、web サイトに mds 用の web アプリケーションを作成し (例[http://localhost/MDS](http://localhost/MDS):)、mds データベースを mds web アプリケーションに関連付けます。 MDS Web アプリケーションを作成するには、コンピューターに IIS がインストールされている必要があります。 MDS データベースと web アプリケーションを構成するための前提条件の詳細については、「 [Web アプリケーションの要件」 (マスターデータサービス)](https://msdn.microsoft.com/library/ee633744.aspx)および「[データベースの要件」 (マスターデータサービス)](https://msdn.microsoft.com/library/ee633767.aspx)を参照してください。  
  
3.  [Data Quality Server インストーラーを使用して DQS をインストールして構成](https://msdn.microsoft.com/library/hh231682.aspx)します。 **[スタート]** 、 **[すべてのプログラム**]、 **[Microsoft SQL Server 2014]** 、 **[Data Quality Services]** 、 **[data quality Server Installer]** の順にクリックします。  
  
4.  Microsoft Excel 2010 (32 ビット推奨)  
  
5.  コンピューターにインストールされている Excel のバージョンに基づいて**Excel 用マスターデータサービスアドイン**(32 ビットまたは64ビット) を[ここ](https://www.microsoft.com/download/details.aspx?id=29064)からインストールします。 コンピューターにインストールされている Excel のバージョンを確認するには、 **excel**を実行し、メニューバーの **[ファイル]** をクリックして、 **[ヘルプ]** をクリックします。右側のウィンドウにバージョンが表示されます。 Excel アドインをインストールする前に、Visual Studio 2010 Tools for Office Runtime をインストールする必要があることに注意してください。  
  
6.  Optional[Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/)でアカウントを作成します。 このチュートリアルのタスクの1つでは、 **Azure Marketplace** (もともとは**データマーケット**) アカウントが必要です。 次のタスクに進む場合は、このタスクをスキップできます。  
  
7.  [Microsoft ダウンロードセンター](https://www.microsoft.com/download/details.aspx?id=50426)から、仕入先 .xls ファイルをダウンロードします。  
  
8.  **64 ビットバージョンの excel**を使用している場合、DQS では、クレンジングまたは照合結果を excel ファイルにエクスポートすることはできません。 これは既知の問題です。 この問題を回避するには、次の手順を実行します。  
  
    1.  **Dqlinstaller-upgrade**を実行します。 SQL Server の既定のインスタンスをインストールした場合、DQSinstaller.exe ファイルは C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn に格納されます。 DQSInstaller.exe ファイルをダブルクリックします。  
  
    2.  **マスターデータサービス構成マネージャー**で、 **[データベースの選択]** をクリックし、既存の **[MDS]** データベース を選択して、 **[アップグレード]** をクリックします。  
  
## <a name="lessons"></a>レッスン  
  
|レッスン|簡単な説明|このレッスンの推定所要時間 (分単位)|  
|------------|-----------------------|------------------------------------------------|  
|[レッスン 1:サプライヤー DQS ナレッジベースの作成](../../2014/tutorials/lesson-1-creating-the-suppliers-dqs-knowledge-base.md)|このレッスンでは、"**業者**" という名前の DQS ナレッジベースを作成します。|60|  
|[レッスン 2:Supplier ナレッジベースを使用した仕入先データのクレンジング](../../2014/tutorials/lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base.md)|このレッスンでは、最初のレッスンで作成した**サプライヤー**ナレッジベースを使用して、DQS プロジェクトを作成して実行し、Excel ファイル内の仕入先データをクレンジングします。|45|  
|[レッスン 3:仕入先リストから重複を削除するためのデータの照合](../../2014/tutorials/lesson-3-matching-data-to-remove-duplicates-from-supplier-list.md)|このレッスンでは、照合アクティビティを実行するための DQS プロジェクトを作成し、クレンジング済みの仕入先一覧から重複項目を特定して削除します。|45|  
|[レッスン 4:MDS に仕入先データを格納する](../../2014/tutorials/lesson-4-storing-supplier-data-in-mds.md)|このレッスンでは、 **Excel 用 MDS アドイン**を使用して、クレンジングおよび一致した仕入先データをマスターデータサービス (MDS) にアップロードします。|45|  
|[レッスン 5: SSIS を使用したクレンジングと照合の自動化](../../2014/tutorials/lesson-5-automating-the-cleansing-and-matching-using-ssis.md)|このレッスンでは、DQS を使用して入力データをクレンジングし、重複項目を削除するためにクレンジングしたデータを照合して、クレンジングおよび照合済みのデータを MDS に自動的に保存する SSIS ソリューションを作成します。|75|  
  
## <a name="next-steps"></a>次の手順  
 チュートリアルを開始するには、最初のレッスンに進んでください。[レッスン 1:サプライヤー DQS ナレッジベース](../../2014/tutorials/lesson-1-creating-the-suppliers-dqs-knowledge-base.md)を作成しています。  
  
  
