---
title: SharePoint リストの接続の種類 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 2c4adf2f-e9c4-4fae-bd3c-97fe64436caf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: cfa09322af5b4838ccdc2bb9dc85d13a412bc359
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66107077"
---
# <a name="sharepoint-list-connection-type-ssrs"></a>SharePoint リストの接続の種類 (SSRS)
  Microsoft SharePoint リストのデータをレポートに含めるには、種類が Microsoft SharePoint リストのレポート データ ソースに基づいたデータセットを追加または作成する必要があります。 これは、Microsoft SQL Server Reporting Services SharePoint リストのデータ拡張機能に基づいたビルトイン データ ソースの種類です。 このデータ ソースの種類を使用して、 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]、 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]、 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 3.0、および [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007 のサイトからのリスト データに接続し、そのデータを取得します。  
  
 このトピックの情報を使用して、データ ソースを構築してください。 手順については、[データ接続またはデータ ソース追加および確認&#40;レポート ビルダーおよび SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)を参照してください。  
  
##  <a name="Connection"></a> 接続文字列  
 SharePoint リストへの接続文字列は、SharePoint サイトまたはサブサイトの URL です ( `http://MySharePointWeb/MySharePointSite` や `http://MySharePointWeb/MySharePointSite/Subsite`など)。  
  
 クエリ デザイナーには、付与されている権限でアクセスできる SharePoint リストが表示されます。  
  
 他の接続文字列の例については、 [レポート ビルダーでのデータ接続、データ ソース、および接続文字列](../data-connections-data-sources-and-connection-strings-in-report-builder.md)に関する記事を参照してください。  
  
##  <a name="Credentials"></a> 資格情報  
 クエリの実行、ローカルでのレポートのプレビュー、およびレポート サーバーからのレポートのプレビューには、資格情報が必要です。 レポートをパブリッシュした後、そのデータ ソースに対する資格情報を変更する必要が生じる場合があります。そのレポートをレポート サーバーで実行するときに、データを取得するためのアクセス許可が有効な状態になるようにするためです。 このデータ拡張機能で使用できる資格情報の種類は、データ ソースとして使用している SharePoint リストの SharePoint テクノロジの構成によって異なります。  
  
 次の表は、ローカル ファームの SharePoint リストおよびリモートの SharePoint リストに接続するときに SharePoint リスト拡張機能が実行する資格情報取得動作の概要を示しています。  
  
 **表 1** は、レガシ Windows SharePoint サイトに配置されたレポートの場合です。 レガシ Windows サイトがサポートしているのは、Kerberos、NTLM、およびフォーム ベースの認証 (FBA) のみです。 **表 2** は、要求ベースの SharePoint サイトに配置されたレポートの場合です。  
  
 **表 1**  
  
||サポートされる資格情報|クラシック モードの Windows 認証|<sup>3</sup>要求認証|  
|-|---------------------------|-----------------------------------------|----------------------------------------|  
|ローカル ファームの SharePoint リスト|Windows 認証 (統合セキュリティ) または SharePoint ユーザー トークン|はい|はい|  
||保存、要求、なし (Windows 資格情報を使用<sup>1</sup>)|はい|いいえ|  
|リモートの SharePoint リスト|Windows 認証 (統合セキュリティ) または SharePoint ユーザー トークン|はい|いいえ<sup>2</sup>|  
||保存、要求、なし (Windows 資格情報を使用<sup>1</sup>)|はい|いいえ<sup>2</sup>|  
  
 **表 2**  
  
||サポートされる資格情報|クラシック モードの Windows 認証|<sup>3</sup>要求認証|  
|-|---------------------------|-----------------------------------------|----------------------------------------|  
|ローカル ファームの SharePoint リスト|Windows 認証 (統合セキュリティ) または SharePoint ユーザー トークン|はい|はい|  
||保存、要求、なし (Windows 資格情報を使用<sup>1</sup>)|いいえ|いいえ|  
|リモートの SharePoint リスト|Windows 認証 (統合セキュリティ) または SharePoint ユーザー トークン|はい|いいえ<sup>2</sup>|  
||保存、要求、なし (Windows 資格情報を使用<sup>1</sup>)|いいえ|いいえ<sup>2</sup>|  
  
 <sup>1</sup>保存された情報や Windows 以外の資格情報のプロンプトの資格情報はサポートされていません。  
  
 <sup>2</sup>リモートの SharePoint リストのフォーム ベースの認証および要求認証はサポートされません。  
  
 <sup>3</sup> Windows 認証、フォーム ベース認証 (FBA)、セキュア アプリケーション マークアップ言語 (SAML) トークン、その他の id プロバイダーまたは上記の 1 つ以上の組み合わせは、認証プロバイダーを説明します。  
  
 **[Windows 認証]**  
 信頼済みアカウント モードのレポート サーバーと連携するように構成されている SharePoint テクノロジの場合、このオプションはサポートされません。 これは、SQL Server 2012 Reporting Services より前のリリースにのみ適用されます。  
  
 Windows 統合モードのレポート サーバーと連携するように構成されている SharePoint テクノロジの場合、このオプションは現在の Windows ユーザーと現在の SharePoint ユーザーの両方に適用されます。  
  
 レポート サーバー (ローカル モード) なしで動作するように構成されている SharePoint テクノロジの場合、このオプションはサポートされません。 ローカル モードの詳細については、「[レポート ビューアーでのローカル モードと接続モードのレポート (Reporting Services の SharePoint モード)](../local-vs-connected-mode-report-viewer-reporting-services-sharepoint-mode.md)」を参照してください。  
  
 **[資格情報は必要ありません]\([資格情報を使用しない])**  
 このオプションを使用するには、レポート サーバーで自動実行アカウントを構成する必要があります。 詳細については、「[自動実行アカウントを構成する &#40;SSRS 構成マネージャー&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)」を参照してください。  
  
 Microsoft BI スタックにおける要求認証サポートの詳細については、「 [Microsoft BI スタックにおける要求認証の使用](https://social.technet.microsoft.com/wiki/contents/articles/15274.using-claims-authentication-across-the-microsoft-bi-stack.aspx)」を参照してください。  
  
 詳細については、次を参照してください[データ接続、データ ソース、および Reporting Services の接続文字列](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)、[レポート ビルダーでの資格情報の指定](../specify-credentials-in-report-builder.md)、および[でサポートされるデータ ソース。Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md)します。  
  
##  <a name="Query"></a> クエリ  
 クエリを設計するには、データ ソースから新規データセットを作成し、関連するクエリ デザイナーを開きます。 詳細については、「 [共有データセットまたは埋め込みデータセットの作成 (レポート ビルダーおよび SSRS)](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)」を参照してください。  
  
 SharePoint リストのグラフィカル クエリ デザイナーには、次の 4 つのペインがあります。  
  
 **SharePoint リスト**  このデータ ソースについて、サイト上のすべての SharePoint リストの一覧が表示されます。 リストを選択してから、クエリに使用するフィールドを選択します。 このペインの各フィールドの名前は、SharePoint 表示名です。 アイテムの上にマウス ポインターを移動すると、ツールヒントに次のプロパティが表示されます。  
  
-   **名前** フィールドの一意の名前です。  
  
-   **識別子** フィールドの一意の識別子です。  
  
-   **フィールドの種類** フィールドのデータ型。  
  
-   **非表示** SharePoint リスト ビューにフィールドを表示するかどうかを指定します。  
  
 複数のリストからフィールドを選択することはできません。 各リストのデータセットを作成し、各データセットからフィールドを選択できます。 リストに共通のフィールドが含まれている場合、一方のデータセットにバインドされている Tablix データ領域で Lookup 関数を使用し、データ領域にバインドされていない他方のデータセットから値を抽出することができます。 詳細については、「[Lookup 関数 &#40;レポート ビルダーおよび SSRS&#41;](../report-design/report-builder-functions-lookup-function.md)」を参照してください。  
  
-   **選択されたフィールド**  選択したフィールドが表示されます。 このペインのフィールドの名前は、SharePoint ユーザーが指定した表示名になります。 クエリ デザイナーを閉じると、レポート データ ペインのデータセット フィールド コレクションにこれらの名前が表示されます。 一意の名前と表示名の関係については、「[[フィールド] ([データセットのプロパティ] ダイアログ ボックス) &#40;レポート ビルダー&#41;](../dataset-properties-dialog-box-fields-report-builder.md)」を参照してください。  
  
-   **適用されたフィルター**  SharePoint リストから返されたデータがレポートに返される前に、このデータを制限します。 使用するフィールド名、演算子、および値を選択して、リストに取得されるデータを制限します。 演算子は、選択した値のデータ型によって異なります。  
  
     グラフィカル クエリ デザイナーでは、並べ替え順を変更したり、グループを指定したりすることはできません。 これらの手順を実行するには、レポート データセットの並べ替え式およびレポートのデータ領域のグループ式を設定します。 クエリ パラメーターはサポートされていません。 レポートでデータをフィルター処理するには、作成したレポート フィルターまたはレポート パラメーターを使用します。 詳細については、「 [データのフィルター、グループ化、および並べ替え (レポート ビルダーおよび SSRS)](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md) 」および「 [レポート パラメーター (レポート ビルダーおよびレポート デザイナー)](../report-design/report-parameters-report-builder-and-report-designer.md)」を参照してください。  
  
-   **クエリ結果**  クエリの実行時に返される行のサンプルが表示されます。 SharePoint リストの値が SharePoint サイトで頻繁に変更されると、クエリ結果ペインに表示される値とレポートの値が異なる場合があります。  
  
-   **選択されたフィールド**  選択したフィールドが表示されます。 このペインのフィールドの名前は、SharePoint ユーザーが指定した表示名になります。 クエリ デザイナーを閉じると、レポート データ ペインのデータセット フィールド コレクションにこれらの名前が表示されます。 一意の名前と表示名の関係については、「[[フィールド] ([データセットのプロパティ] ダイアログ ボックス) &#40;レポート ビルダー&#41;](../dataset-properties-dialog-box-fields-report-builder.md)」を参照してください。  
  
-   **適用されたフィルター**  SharePoint リストから返されたデータがレポートに返される前に、このデータを制限します。 使用するフィールド名、演算子、および値を選択して、リストに取得されるデータを制限します。 演算子は、選択した値のデータ型によって異なります。  
  
     グラフィカル クエリ デザイナーでは、並べ替え順を変更したり、グループを指定したりすることはできません。 これらの手順を実行するには、レポート データセットの並べ替え式およびレポートのデータ領域のグループ式を設定します。 クエリ パラメーターはサポートされていません。 レポートでデータをフィルター処理するには、作成したレポート フィルターまたはレポート パラメーターを使用します。 詳細については、「 [データのフィルター、グループ化、および並べ替え (レポート ビルダーおよび SSRS)](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md) 」および「 [レポート パラメーター (レポート ビルダーおよびレポート デザイナー)](../report-design/report-parameters-report-builder-and-report-designer.md)」を参照してください。  
  
-   **クエリ結果**  クエリの実行時に返される行のサンプルが表示されます。 SharePoint リストの値が SharePoint サイトで頻繁に変更されると、クエリ結果ペインに表示される値とレポートの値が異なる場合があります。  
  
 詳細については、「[SharePoint リストのクエリ デザイナー &#40;レポート ビルダー&#41;](sharepoint-list-query-designer-report-builder.md)」を参照してください。  
  
### <a name="query-text"></a>クエリ テキスト  
 グラフィカル クエリ デザイナーで生成されたクエリを表示するには、テキスト ベースのクエリ デザイナーに切り替えます。 このビューには、グラフィカル クエリ デザイナーで作成された XML が表示されます。 XML には要素として、リスト名、フィールド コレクション、およびフィルターも含まれます。  
  
#### <a name="example-1-specified-fields-for-a-list"></a>例 1. リストの指定フィールド  
 次の例は、整形式の SharePoint クエリを示しています。  
  
```  
<RSSharePointList>  
<listName>MyList</listName>  
<viewFields>  
  <FieldRef Name="Field1"/>  
  <FieldRef Name="Field4"/>  
</viewFields>  
<Query>  
  <Where>  
    <And>  
      <Gt>  
        <FieldRef Name="Field1"/>  
        <Value Type="Integer">1</Value>  
      </Gt>  
      <IsNotNull>  
        <FieldRef Name="Field2"/>  
        <Value Type="string"/>  
      </IsNotNull>   
    </And>  
  </Where>  
</Query>  
</RSSharePointList>  
```  
  
 整形式の XML テキストという状態を崩さない限り、このビューのクエリを編集できます。  
  
#### <a name="example-2-all-fields-for-a-list"></a>例 2。 リストのすべてのフィールド  
 リストの名前のみを指定することもできます。非表示のフィールドを含むすべてのフィールドが返されます。 次の例では、Tasks という名前のリストからすべてのフィールドを取得します。  
  
```  
<RSSharePointList>  
<listName>Tasks</listName>  
</RSSharePointList>  
```  
  
 リスト Tasks のすべてのフィールドがクエリ結果で返されます。  
  
##  <a name="Parameters"></a> パラメーター  
 このデータ拡張機能では、パラメーターはサポートされていません。  
  
  
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
  
  
