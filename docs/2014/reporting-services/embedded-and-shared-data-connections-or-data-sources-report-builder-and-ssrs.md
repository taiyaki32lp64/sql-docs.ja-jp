---
title: 埋め込みし、共有データ接続またはデータ ソース (レポート ビルダーおよび SSRS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- embedded data sources
- shared data sources
- data sources
ms.assetid: f417782c-b85a-4c4d-8a40-839176daba56
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b987dd46f6a60a0d0cadc95cf187566eafa4f527
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109270"
---
# <a name="embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs"></a>埋め込みおよび共有のデータ接続またはデータ ソース (レポート ビルダーおよび SSRS)
  クエリが実行されるとき、またはレポートが処理されるとき、レポートはデータを取得するためにデータ接続を使用します。 ユーザーは、そのデータ接続を、リレーショナル データベース、多次元データベース、Web サービスなどのデータ ソースに接続する組み込みのデータ接続の種類の一覧から選択します。 データ接続の説明では、次の用語を使用します。  
  
-   **データ接続:** " *データ ソース*" とも呼ばれます。 データ接続には、名前と、接続の種類に依存する接続のプロパティが含まれます。 仕様上、データ接続に資格情報は含まれません。 データ接続では、どのデータを外部データ ソースから取得するかは指定されません。 これを行うには、データセットを作成するときにクエリを指定します。  
  
-   **データ ソースの定義:** レポート データ ソースの XML 表現を含むファイル。 レポートをパブリッシュすると、そのデータ ソースは、レポート定義とは別にデータ ソース定義として、レポート サーバーまたは SharePoint サイトに保存されます。 たとえば、レポート サーバー管理者は、接続文字列や資格情報を更新することができます。 ネイティブのレポート サーバーでのファイルの種類は .rds です。 SharePoint サイトでのファイルの種類は .rsds です。  
  
-   **接続文字列:** 接続文字列は、データ ソースに接続するために必要な接続プロパティの文字列バージョンです。 接続プロパティはデータ接続の種類に応じて異なります。 例については、「 [レポート ビルダーでのデータ接続、データ ソース、および接続文字列](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md)」を参照してください。  
  
-   **共有データ ソース:** レポート サーバーまたは SharePoint サイトにあり、複数のレポートで使用することができるデータ ソースです。  
  
-   **埋め込みデータ ソース:** " *レポート固有のデータ ソース*" とも呼ばれます。 1 つのレポート内で定義され、そのレポートのみで使用されるデータ ソースです。  
  
-   **資格情報:** 資格情報は、外部データにアクセスするために指定する必要がある認証情報です。  
  
 埋め込みデータ ソースと共有データ ソースとでは、作成、格納、および管理の方法が異なります。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
## <a name="shared-data-sources"></a>共有データ ソース  
 共有データ ソースは、よく使用するデータ ソースがある場合に役立ちます。 可能な限り共有データ ソースを使用することをお勧めします。 レポートやレポートへのアクセスが管理しやすくなり、レポートやレポートからアクセスするデータ ソースの安全性を高めることができます。 共有データ ソースが必要な場合は、システム管理者に依頼して作成してもらってください。  
  
 レポート ビルダーで共有データ ソースを作成することはできません。 共有データ ソースはレポート サーバーで参照し、選択できます。 詳細については、「 [Data Connections, Data Sources, and Connection Strings in Report Builder](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md)」を参照してください。  
  
 レポート デザイナーでは、レポート サーバー上の共有データ ソースを参照できません。 共有データ ソースは、ソリューション エクスプローラーでプロジェクトの一部として作成し、レポート サーバーに配置するかどうかを選択できます。 使用しているコンピューターとレポート サーバーの資格情報の相違のため、これらをローカルでのみ使用するように選択する場合もあります。 詳細については、「[Reporting Services でのデータ接続、データ ソース、および接続文字列](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)」を参照してください。  
  
 次のアイコンは、レポート サーバーのフォルダー階層内の共有データ ソース アイテムを示します。![共有データ ソースのアイコン](media/hlp-16datasource.png "共有データ ソースのアイコン")  
  
## <a name="embedded-data-sources"></a>埋め込みデータ ソース  
 埋め込みデータ ソースは、レポート定義に保存されるデータ接続です。 埋め込まれたデータ ソースの接続情報は、その情報が埋め込まれたレポートでのみ使用できます。 埋め込みデータ ソースを定義および管理するには、 **[データ ソースのプロパティ]** ダイアログ ボックスを使用します。  
  
##  <a name="Comparing"></a> 埋め込みし、共有データ ソースの比較  
 次の表は、埋め込みデータ ソースと共有データ ソースの違いをまとめたものです。  
  
|説明|埋め込み<br /><br /> [データ ソース]|Shared<br /><br /> [データ ソース]|  
|-----------------|------------------------------|----------------------------|  
|データ接続がレポート定義に埋め込まれる|![使用可能](media/greencheck.gif "使用可能")||  
|レポート サーバー上のデータ接続へのポインターがレポート定義に埋め込まれる||![使用可能](media/greencheck.gif "使用可能")|  
|レポート サーバー上で管理|![使用可能](media/greencheck.gif "使用可能")|![使用可能](media/greencheck.gif "使用可能")|  
|共有データセットに必要||![使用可能](media/greencheck.gif "使用可能")|  
|コンポーネントに必要||![使用可能](media/greencheck.gif "使用可能")|  
  
## <a name="data-source-credentials"></a>データ ソースの資格情報  
 資格情報は、埋め込みデータ ソースの作成、クエリの実行、またはレポート処理時のデータ取得のために使用されます。 データ ソースの所有者が、データへのアクセスに使用する必要がある資格情報の種類を決定します。 資格情報は、データ接続とは別に、レポート作成環境内のレポート サーバー、SharePoint サイト、またはローカル コンピューターで管理されます。 データ ソースの種類に応じて、資格情報を保存して各ユーザーに入力を求めないようにすることも、入力を求めるように設定することもできます。 必要とされる資格情報は、データ ソースへの接続に、自分のコンピューターを使用しているかレポート サーバーを使用しているかに応じて異なる場合があります。 詳細については、次を参照してください。[レポート ビルダーでの資格情報の指定](../../2014/reporting-services/specify-credentials-in-report-builder.md)と[データ接続、データ ソース、および Reporting Services の接続文字列](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)します。  
  
## <a name="see-also"></a>参照  
 [レポートにデータを追加&#40;レポート ビルダーおよび SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [レポート作成の概念 &#40;レポート ビルダーおよび SSRS&#41;](report-design/report-authoring-concepts-report-builder-and-ssrs.md)   
 [Reporting Services でサポートされるデータ ソース &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [データ接続またはデータ ソース追加および確認&#40;レポート ビルダーおよび SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)   
 [埋め込みデータセットと共有データセット &#40;レポート ビルダーおよび SSRS&#41;](report-data/embedded-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
