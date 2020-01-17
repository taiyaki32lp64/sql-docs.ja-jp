---
title: 外部データ ソースのデータを追加する (SSRS) | Microsoft Docs
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
reviewer: ''
ms.custom: ''
ms.date: 03/17/2017
ms.openlocfilehash: 003348fc8ba74420909cb3f74026932a42f97a9b
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73593910"
---
# <a name="add-data-from-external-data-sources-ssrs"></a>外部データ ソースのデータを追加する (SSRS)
  外部データ ソースからデータを取得するには、データ接続を使用します。 データ接続情報は、通常は権限の付与と使用する資格情報の指定を担う外部データ ソースの所有者によって提供されます。 データ接続情報は、レポート データ ソースとして保存されます。 データ ソースの種類により、データの取得に使用するデータ拡張機能が決まります。  
  
 データ ソースの種類の詳細については、「 [トピックの内容](#InThisSection)」を参照してください。  
  
##  <a name="DataAccess"></a> データ アクセス テクノロジについて  
 レポート データセットのデータを取得するには、複数のレイヤーにわたるデータ アクセス ソフトウェアが必要です。 以下に、データ アクセス テクノロジによるレポートのしくみを簡単に説明します。  
  
-   **アプリケーションとユーザー インターフェイス** データ ソースの作成、共有データ ソースへの参照の追加、共有データセットの追加、依存先のデータ ソースおよびデータセットを含むレポート パーツの追加などに使用する、レポート ビルダー アプリケーションです。  
  
-   **レポート定義要素** データ ソースとデータセットは、レポート定義の一部です。 レポートをレポート サーバーにパブリッシュすると、共有データ ソースと共有データセットはレポート定義から独立して管理されます。  
  
    -   **データ ソースと共有データ ソース** データ処理拡張機能の種類、接続情報、および認証に関する情報を含む、レポート定義の一部です。  
  
    -   **データセットとフィールド コレクション** クエリ、フィールド コレクション、およびフィールドのデータ型を含む、レポート定義の一部です。  
  
-   **Reporting Services データ拡張機能** レポート ビルダーと共にインストールされる、組み込みのデータ拡張機能です。 データ拡張機能は、認証、サーバー集計値、および複数値パラメーターを処理する機能を提供します。  
  
-   **データ プロバイダー** 外部データ ソースとの接続およびデータの取得を管理するソフトウェアです。 データ プロバイダーは、接続文字列の構文を定義します。 ほとんどのデータ拡張機能は、データ プロバイダー レイヤーの上位に構築されます。  
  
-   **外部データ ソース** データベース、ファイル、キューブ、Web サービスなど、レポート データの取得先です。  
  
> [!NOTE]  
>  レポート サーバーに接続していないときは、レポート ビルダーと共にインストールされたデータ拡張機能を選択できます。 データには、使用しているコンピューターの資格情報を使用して、シングル ユーザーとしてアクセスします。 レポート サーバーに接続しているときは、レポート サーバーにインストールされているデータ拡張機能を選択できます。 データには、レポートを実行する複数のユーザーの 1 人としてアクセスし、レポート サーバー上の資格情報を使用します。 詳細については、「 [レポート データ ソースに関する資格情報と接続情報を指定する](specify-credential-and-connection-information-for-report-data-sources.md)」をご覧ください。  
  
##  <a name="ReportData"></a> レポート データについて  
 簡単に言うと、レポートでは、レポート データセットのデータがレポート ページのデータ領域に表示されます。このデータ領域は、単一のテーブル、グラフ、マトリックス、またはその他の種類のレポート データ領域です。 レポート データセットのデータは、外部データ ソースに読み取り専用アクセスを実行する単一のクエリ コマンドから返された最初の結果セットから取得されます。 各データ領域は、データセットのすべてのデータを表示するために、必要に応じて拡張されます。  
  
 データセットのデータは、必然的に表形式になります。 列は、データセット クエリのフィールドです。 行は、結果セットの行です。 次の一般化されたデータの種類をレポートで使用できます。  
  
-   四角形データ。 すべての行に同じ数の列が含まれる結果セットのデータです。  
  
-   階層データは、フラット化された行セットとしてサポートされます。  
  
    -   データの各行の列数が異なる不規則階層はサポートされません。 データ拡張機能によっては、このことが問題になる場合があります。  
  
    -   多次元データ ソースを利用するデータ拡張機能は、XML for Analysis プロトコルを使用し、データをセル セットとしてではなく、フラット化された行セットとして取得します。  
  
    -   XML データ拡張機能は、XML データをレポートで使用できるように自動的にフラット化します。 XML 要素の最初のインスタンスにすべての属性またはサブ要素が含まれない場合、データはレポート データとして利用できない可能性があります。  
  
-   再帰型データはサポートされます。 再帰型データ階層を含む結果セットは、階層構造に関するすべての情報を四角形の結果セット内に含みます。 たとえば、会社内の上司/部下構造は、2 つの列 (従業員とマネージャー) を含むテーブルで表すことができます。 各マネージャーは、マネージャーがいる従業員でもあります。 最上位のマネージャーは、通常、その従業員にマネージャーがいないことを示す NULL または他の識別子を含みます。  
  
  
##  <a name="DataTypes"></a> データ型の処理  
 データセットを作成すると、フィールドのデータ型は、 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]の共通言語ランタイム (CLR) データ型のサブセットにマップされます。 明示的にマップできないデータ型は、文字列として返されます。 フィールドのデータ型の操作の詳細については、「 [データセット フィールド コレクション &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)」を参照してください。 パラメーターを作成する場合、データ型は、サポートされているレポート定義のデータ型であることが必要です。 データ プロバイダーからレポート パラメーターへデータ型をマップする方法の詳細については、「[式で使用されるデータ型 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)」を参照してください。  
  
  
##  <a name="HowTo"></a> 操作方法に関するトピック  
 データ接続、データ ソース、およびデータセットを操作する手順について説明します。  
  
 [データ接続を追加および確認する (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [共有データセットまたは埋め込みデータセットの作成 (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [データセットへのフィルターの追加 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="InThisSection"></a> トピックの内容  
 次のトピックでは、各組み込みデータ拡張機能について説明します。  
  
|トピック|データ ソースの種類|  
|-----------|----------------------|  
|[SQL Server の接続の種類 &#40;SSRS&#41;](../../reporting-services/report-data/sql-server-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|[MDX のための Analysis Services の接続の種類 &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|  
|[Power Pivot の接続の種類 &#40;SSRS&#41;](../../reporting-services/report-data/power-pivot-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|  
|[SharePoint リストの接続の種類 &#40;SSRS&#41;](../../reporting-services/report-data/sharepoint-list-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] SharePoint リスト|  
|[SQL Azure の接続の種類 &#40;SSRS&#41;](../../reporting-services/report-data/sql-azure-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDS](../../includes/sssds-md.md)]|  
|[SQL Server 並列データ ウェアハウスの接続の種類 &#40;SSRS&#41;](../../reporting-services/report-data/sql-server-parallel-data-warehouse-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDWfull](../../includes/ssdwfull-md.md)]|  
|[SAP NetWeaver BI の接続の種類 &#40;SSRS&#41;](../../reporting-services/report-data/sap-netweaver-bi-connection-type-ssrs.md)|SAP NetWeaver BI|  
|[Hyperion Essbase の接続の種類 &#40;SSRS&#41;](../../reporting-services/report-data/hyperion-essbase-connection-type-ssrs.md)|Hyperion Essbase|  
|[OLE DB の接続の種類 &#40;SSRS&#41;](../../reporting-services/report-data/ole-db-connection-type-ssrs.md)|OLE DB (OLE DB)|  
|[ODBC の接続の種類 &#40;SSRS&#41;](../../reporting-services/report-data/odbc-connection-type-ssrs.md)|ODBC|  
|[XML の接続の種類 &#40;SSRS&#41;](../../reporting-services/report-data/xml-connection-type-ssrs.md)|XML|  
  
##  <a name="Related"></a> 関連項目

 次に示すセクションでは、レポート データの概念が詳細に説明されているほか、データに関連するレポートのパーツを定義、カスタマイズ、および使用する手順が説明されています。  
  
|トピック|[説明]|  
|-----------|-----------------|  
|[レポート データセット &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)|レポートのデータへのアクセスの概要について説明します。|  
|[レポート ビルダーでのデータ接続、データ ソース、および接続文字列](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)|データ接続とデータ ソースについて説明します。|  
|[レポート埋め込みデータセットと共有データセット (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)|埋め込みデータセットと共有データセットについて説明します。|  
|[データセット フィールド コレクション (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)|クエリによって生成されるデータセット フィールド コレクションについて説明します。|  
|[Reporting Services でサポートされるデータ ソース (SSRS)](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)|各データ拡張機能のプラットフォームおよびバージョン サポートに関する詳細な情報です。|  
|[データ処理拡張機能の概要](../../reporting-services/extensions/data-processing/data-processing-extensions-overview.md)|データ拡張機能に関する上級ユーザー向けの詳細な情報です。|  
  
  
## <a name="see-also"></a>参照  
 [レポート データセット (SSRS)](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [クエリ デザイン ツール &#40;SSRS&#41;](query-design-tools-ssrs.md)  
  
  
