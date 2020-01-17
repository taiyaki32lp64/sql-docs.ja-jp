---
title: XML の接続の種類 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 5b55fff2-1b15-4156-83ef-15ad9cf9f509
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6d9f5c70e0457009f71c3b9087ecf9f1354a8835
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106925"
---
# <a name="xml-connection-type-ssrs"></a>XML の接続の種類 (SSRS)
  XML データ ソースのデータをレポートに含めるには、種類が XML のレポート データ ソースに基づいたデータセットが必要です。 このビルトイン データ ソースの種類は、XML データ拡張機能に基づいています。 このデータ ソースの種類を使用して、XML ドキュメント、Web サービス、またはクエリに埋め込まれた XML に接続し、データを取得します。  
  
 このデータ拡張機能は、接続文字列とは別に管理される資格情報およびパラメーターをサポートしています。  
  
 このトピックの情報を使用して、データ ソースを構築してください。 手順については、[データ接続またはデータ ソース追加および確認&#40;レポート ビルダーおよび SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)を参照してください。  
  
##  <a name="Connection"></a> 接続文字列  
 接続文字列を、HTTP 経由でアクセス可能な Web サービス、Web ベース アプリケーション、または XML ドキュメントを指す URL に設定する必要があります。 XML ドキュメントの拡張子は XML にする必要があります。 データセット クエリに埋め込まれた XML データに対し、空の接続文字列を使用することもできます。  
  
 次の例に、それぞれ Web サービスと XML ドキュメントに対する接続文字列の構文を示します。 `file://` プロトコルはサポートされません。  
  
|XML ドキュメントの種類|接続文字列の例|  
|-----------------------|-------------------------------|  
|Web サービス|`http://adventure-works.com/results.aspx`|  
|XML ドキュメント|`http://localhost/XML/Customers.xml`|  
|埋め込み XML ドキュメント|*空*|  
  
 他の接続文字列の例については、 [レポート ビルダーでのデータ接続、データ ソース、および接続文字列](../data-connections-data-sources-and-connection-strings-in-report-builder.md)に関する記事を参照してください。  
  
##  <a name="Credentials"></a> 資格情報  
 クエリの実行、ローカルでのレポートのプレビュー、およびレポート サーバーからのレポートのプレビューには、資格情報が必要です。  
  
 レポートをパブリッシュした後、そのデータ ソースに対する資格情報を変更する必要が生じる場合があります。そのレポートをレポート サーバーで実行するときに、データを取得するためのアクセス許可が有効な状態になるようにするためです。  
  
 レポート作成クライアントから資格情報の指定に使用できるオプションは次のとおりです。  
  
-   現在の Windows ユーザー (統合セキュリティとも呼ばれます)。  
  
-   資格情報を必要としない。 資格情報を選択しない場合には、匿名アクセスが使用されます。 レポート サーバーが外部データ ソースに接続するための自動実行アカウントが定義済みであることを確認してください。 XML データ処理拡張機能は、対象 URL または Web サービスに資格情報を渡しません。したがって、自動実行アカウントが定義されていないと接続に失敗します。 詳細については、msdn.microsoft.com の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [オンライン ブック](https://go.microsoft.com/fwlink/?linkid=121312)にある [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ドキュメントの「[自動実行アカウントの構成 (SSRS 構成マネージャー)](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)」を参照してください。  
  
 保存された資格情報や要求された資格情報はサポートされていません。 Windows 統合セキュリティが無効になっていると、データの取得に Windows 統合セキュリティを使用できないので注意してください。 保存された資格情報や要求された資格情報を指定すると、実行時にエラーが発生します。  
  
 詳しくは、「[データ接続、データ ソース、および接続文字列 (レポート ビルダーおよび SSRS)](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)」または[レポート ビルダーでの資格情報の指定](../specify-credentials-in-report-builder.md)に関する記事を参照してください。  
  
##  <a name="Query"></a> クエリ  
 クエリでは、レポート データセット用に取得するデータを指定します。 クエリの結果セットの列には、データセットのフィールド コレクションが設定されます。 レポートによって処理されるのは、クエリから取得された最初の結果セットだけです。  
  
 クエリを作成するにはテキスト ベースのクエリ デザイナーを使用する必要があります。 クエリでは XML データを返す必要があります。  
  
 テキスト ベースのクエリ デザイナーについては、「[テキストベースのクエリ デザイナーのユーザー インターフェイス (レポート ビルダー)](text-based-query-designer-user-interface-report-builder.md)」を参照してください。  
  
 XML データ ソースに対して使用できるデータセット クエリの値を以下に示します。  
  
-   *空*:既定の結果セットを作成するには、空のクエリを使用します。 既定のクエリは、データ ソースを読み取り、最初のリーフ コレクションまで XML ノード階層をたどることによって作成されます。 結果セットには、テキスト値を持つすべてのノード、および、そのパス上に存在するすべてのノード属性が格納されます。 結果セットの列は、データセットのフィールドにマップされます。  
  
-   要素パス:データ ソースから XML データを取得するときに使用するノードのシーケンスを指定します。  
  
-   XML Query 要素:XML Query の必須の要素および省略可能な要素を次に示します。  
  
    -   **Web サービス。**  
  
         XML 要素が必要です。  
  
         `<Method Namespace=` *"名前空間"*  `Name="MethodName" />`  
  
         `-- or --`  
  
         `<SoapAction>` *SOAP アクション* `</SoapAction>`  
  
         省略可能な XML 要素:  
  
         `<ElementPath>`  *要素パス*  `</ElementPath>`  
  
         `<Method Namespace=` *"名前空間"*  `Name="MethodName" />`  
  
         `-- or --`  
  
         `<SoapAction>` *SOAP アクション* `</SoapAction>`  
  
    -   **XML ドキュメント。**  
  
         省略可能な XML 要素:  
  
         `<ElementPath>`  *要素パス*  `</ElementPath>`  
  
    -   **埋め込み XML ドキュメント。**  
  
         XML 要素が必要です。  
  
         `<XmlData>` 内部 XML `</XmlData>`  
  
         省略可能な XML 要素:  
  
         `<ElementPath>`  *要素パス*  `</ElementPath>`  
  
         `-- or --`  
  
         `<ElementPath IgnoreNamespaces="true">`  *要素パス*  `</ElementPath>`  
  
 クエリ構文の詳細については、msdn.microsoft.com にある [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ドキュメント ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [オンライン ブック](https://go.microsoft.com/fwlink/?linkid=121312)) の「[XML レポート データの XML クエリ構文 (SSRS)](report-data-ssrs.md)」を参照してください。  
  
 例については、「[Reporting Services:XML および Web サービス データ ソースを使用する](https://go.microsoft.com/fwlink/?LinkId=81654)」を参照してください。  
  
### <a name="requirements-for-retrieving-xml-web-service-data"></a>XML Web サービスのデータを取得するための要件  
 これらは XML データ処理拡張機能では検出されません。 そのため、必要なデータを取得する SOAP メソッドを検索するための、なんらかの手段が必要です。 また、Web サービスがそのデータに対して使用するアドレス指定スキームや名前空間を把握しておく必要もあります。  
  
 Web サービスの場合、<`Query`> 要素を使って、呼び出すメソッドや SOAP アクションを指定できます。 XML データ ソースが、レポートに必要なデータを取得できるような階層構造になっていれば、クエリを空にして、既定のクエリを使用することもできます。 クエリの実行時に取得される XML 要素ノードの値および属性は、レポートに使用されているデータセットのフィールドにマップされます。  
  
### <a name="requirements-for-retrieving-xml-document-data"></a>XML ドキュメントのデータを取得するための要件  
 サーバーから HTTP プロトコルを使って XML データを取得するか、XML データを XML `Query` 要素に埋め込む必要があります。 XML ドキュメントを HTTP プロトコルを使って直接参照する場合、拡張子を .xml にする必要があります。  
  
 必要なすべてのデータを取得するための XML クエリの作成方法を理解しておく必要があります。 要素パスを指定しない場合、XML ドキュメントを解析するときの既定の動作では、XML ドキュメントのリーフノード コレクションへの使用可能な最初のパスが選択されます。 XML ドキュメントに他の兄弟リーフノード コレクションへのパスが含まれている場合、クエリでパスを指定しない限り、それらのノードは無視されます。  
  
 XQuery と似た XML 構文を使って要素パスを指定できます。  
  
 詳細については、msdn.microsoft.com にある [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ドキュメント ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [オンライン ブック](https://go.microsoft.com/fwlink/?linkid=121312)) の「[XML レポート データの要素パス構文 (SSRS)](element-path-syntax-for-xml-report-data-ssrs.md)」を参照してください。  
  
##  <a name="Parameters"></a> パラメーター  
 クエリの解析時にパラメーターは識別されません。  
  
 パラメーターを追加するには、 **[データセットのプロパティ]** ダイアログ ボックスの [[パラメーター]](../dataset-properties-dialog-box-parameters-report-builder.md) ページを使用して手動で作成する必要があります。  
  
##  <a name="Remarks"></a> 解説  
 XML データ拡張機能は、階層構造でない表形式の XML データからのレポート作成をサポートしています。 詳細については、「[外部データ ソースのデータを追加する (SSRS)](add-data-from-external-data-sources-ssrs.md)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースから XML ドキュメントを取得するためのサポートは組み込まれていません。  
  
##  <a name="HowTo"></a> 操作方法に関するトピック  
 データ接続、データ ソース、およびデータセットを操作する手順について説明します。  
  
 [データ接続またはデータ ソース追加および確認&#40;レポート ビルダーおよび SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [共有データセットまたは埋め込みデータセットの作成 (レポート ビルダーおよび SSRS)](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [データセットへのフィルターの追加 (レポート ビルダーおよび SSRS)](add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
##  <a name="Related"></a> 関連項目  
 次に示すセクションでは、レポート データの概念が詳細に説明されているほか、データに関連するレポートのパーツを定義し、カスタマイズし、使用する方法が説明されています。  
  
 [レポートにデータを追加&#40;レポート ビルダーおよび SSRS&#41;](report-datasets-ssrs.md)  
 レポートのデータへのアクセスの概要について説明します。  
  
 [レポート ビルダーでのデータ接続、データ ソース、および接続文字列](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
 データ接続とデータ ソースについて説明します。  
  
 [レポート埋め込みデータセットと共有データセット &#40;レポート ビルダーおよび SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 埋め込みデータセットと共有データセットについて説明します。  
  
 [データセット フィールド コレクション &#40;レポート ビルダーおよび SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)  
 クエリによって生成されるデータセット フィールド コレクションについて説明します。  
  
 [Reporting Services でサポートされるデータ ソース &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md) ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [オンライン ブック](https://go.microsoft.com/fwlink/?linkid=121312)の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ドキュメント)。  
 各データ拡張機能のプラットフォームおよびバージョン サポートに関する詳細な情報です。  
  
## <a name="see-also"></a>参照  
 [レポート パラメーター &#40;レポート ビルダーおよびレポート デザイナー&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [データのフィルター、グループ化、および並べ替え &#40;レポート ビルダーおよび SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [式 &#40;レポート ビルダーおよび SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
  
  
