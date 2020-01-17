---
title: SQL Azure の接続の種類 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: c84def6c-e8cf-43d9-9912-098171a7ce79
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: cdee6968bc4760688c6497db6d59ad04a33fa033
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66107025"
---
# <a name="sql-azure-connection-type-ssrs"></a>SQL Azure の接続の種類 (SSRS)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] は、ホストされているクラウドベースのリレーショナル データベースで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テクノロジを利用して構築されています。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] からのデータをレポートに含めるには、 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]の種類のレポート データ ソースに基づいたデータセットが必要です。 このビルトイン データ ソースの種類は、 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] データ拡張機能に基づいています。 このデータ ソースの種類を使用して、 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]からのデータに接続し、そのデータを取得します。  
  
 このデータ拡張機能は、接続文字列とは個別に管理される、複数の値を持つパラメーター、サーバー集計、および資格情報をサポートしています。  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] は、オンプレミスの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスと似ています。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] からは、一部の例外を除き、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]と同じようにデータを取得できます。  
  
> [!NOTE]  
>  [!INCLUDE[ssSDS](../../includes/sssds-md.md)]への接続を開くときに、接続タイムアウトを 30 秒に設定してください。  
  
 詳細については、次を参照してください。 [Azure SQL Database のドキュメント](https://docs.microsoft.com/azure/sql-database/)します。  
  
 このトピックの情報を使用して、データ ソースを構築してください。 手順については、[データ接続またはデータ ソース追加および確認&#40;レポート ビルダーおよび SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)を参照してください。  
  
##  <a name="Connection"></a> 接続文字列  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]に接続する場合、クラウド内のデータベース オブジェクトに接続します。 オンサイトのデータベースと同様に、ホストされているデータベースには、複数のテーブル、ビュー、およびストアド プロシージャを含むスキーマが複数存在している場合があります。 クエリ デザイナーで、使用するデータベース オブジェクトを指定します。 接続文字列でデータベースを指定しない場合は、管理者によって割り当てられた既定のデータベースに接続されます。  
  
 データ ソースへの接続に使用する接続情報および資格情報については、データベース管理者に問い合わせてください。 AdventureWorks というホストされているサンプル データベースを指定する接続文字列の例を次に示します。  
  
```  
Data Source=<host>;Initial Catalog=AdventureWorks; Encrypt=True;  
```  
  
 また、 **[データ ソースのプロパティ]** ダイアログ ボックスを使用して、ユーザー名やパスワードなどの資格情報を入力します。 `User Id` オプションと `Password` オプションは、接続文字列に自動的に付加されます。これらを接続文字列の一部として入力する必要はありません。  
  
 詳細および接続文字列の例については、「 [レポート ビルダーでのデータ接続、データ ソース、および接続文字列](../data-connections-data-sources-and-connection-strings-in-report-builder.md)」を参照してください。  
  
##  <a name="Credentials"></a> 資格情報  
 Windows 認証 (統合セキュリティ) はサポートされていません。 Windows 認証を使用して [!INCLUDE[ssSDS](../../includes/sssds-md.md)] に接続しようとすると、エラーが発生します。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] でサポートされているのが SQL Server 認証 (ユーザー名とパスワード) のみであるため、ユーザーは [!INCLUDE[ssSDS](../../includes/sssds-md.md)]に接続するたびに資格情報 (ログインとパスワード) を入力する必要があります。  
  
 データベースにアクセスするには、十分な資格情報が必要です。 クエリによっては、他の権限 (ストアド プロシージャを実行したり、テーブルやビューにアクセスしたりするために必要な権限) が必要な場合があります。 外部データ ソースの所有者は、十分な資格情報を構成して、ユーザーが必要とするデータベース オブジェクトに対する読み取り専用アクセスを提供する必要があります。  
  
 レポート作成クライアントから資格情報の指定に使用できるオプションは次のとおりです。  
  
-   保存されているユーザー名とパスワードを使用する。 レポート データを格納するデータベースがレポート サーバーとは別のサーバーに存在する場合に発生するダブル ホップに対処するには、資格情報を Windows 資格情報として使用するオプションを選択します。 データ ソースに接続した後に、認証されているユーザーの権限を借用するオプションもあります。  
  
-   資格情報を必要としない。 このオプションを使用するには、レポート サーバーで自動実行アカウントを構成しておく必要があります。 詳細については、msdn.microsoft.com で [Reporting Services に関するドキュメント](https://go.microsoft.com/fwlink/?linkid=121312)の「[自動実行アカウントの構成 &#40;SSRS 構成マネージャー&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)」を参照してください。  
  
 詳しくは、「[データ接続、データ ソース、および接続文字列 (レポート ビルダーおよび SSRS)](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)」または[レポート ビルダーでの資格情報の指定](../specify-credentials-in-report-builder.md)に関する記事を参照してください。  
  
 
  
##  <a name="Query"></a> クエリ  
 クエリでは、レポート データセット用に取得するデータを指定します。 クエリの結果セットの列には、データセットのフィールド コレクションが設定されます。 クエリで複数の結果セットが返された場合にレポートによって処理されるのは、クエリから取得された最初の結果セットだけです。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と [!INCLUDE[ssSDS](../../includes/sssds-md.md)]の間には、サポートされるデータベースのサイズなど、いくつか違いがありますが、 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]に対するクエリの作成方法と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに対するクエリの作成方法はほぼ同じです。 [!INCLUDE[tsql](../../includes/tsql-md.md)] では、BACKUP などの一部の [!INCLUDE[ssSDS](../../includes/sssds-md.md)]ステートメントがサポートされていませんが、これらはレポート クエリで使用するステートメントではありません。 詳細については、「[SQL Server の接続の種類 (SSRS)](sql-server-connection-type-ssrs.md)」を参照してください。  
  
 新しいクエリを作成するか、グラフィカル クエリ デザイナーで表示できる既存のクエリを開く場合、既定でリレーショナル クエリ デザイナーを使用できます。 クエリは、次の方法で指定できます。  
  
-   クエリを対話形式で作成します。 データベース スキーマ別に編成された、テーブル、ビュー、ストアド プロシージャ、およびその他のデータベース アイテムの階層ビューが表示されるリレーショナル クエリ デザイナーを使用します。 テーブルまたはビューから列を選択するか、ストアド プロシージャまたはテーブル値関数を指定します。 フィルター条件を指定して、取得するデータの行数を制限します。 パラメーター オプションを設定してレポートの実行時にフィルターをカスタマイズします。  
  
-   クエリを入力するか、貼り付けます。 テキスト ベースのクエリ デザイナーは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] テキストを直接入力する、クエリ テキストを別のソースから貼り付ける、リレーショナル クエリ デザイナーでは作成できない複雑なクエリを入力する、クエリ ベースの式を入力する、などの場合に使用します。  
  
-   ファイルまたはレポートから既存のクエリをインポートします。 クエリ デザイナーの **[クエリのインポート]** ボタンを使用して、.sql ファイルまたは .rdl ファイルを参照し、クエリをインポートします。  
  
 テキスト ベースのクエリ デザイナーでは、次の 2 つのモードがサポートされています。  
  
-   [テキスト](#QueryText) : データ ソースからデータを選択する [!INCLUDE[tsql](../../includes/tsql-md.md)] コマンドを入力します。  
  
-   [ストアド プロシージャ](#QueryStoredProcedure) : ストアド プロシージャの一覧から選択します。  
  
 詳細については、「[リレーショナル クエリ デザイナーのユーザー インターフェイス &#40;レポート ビルダー&#41;](relational-query-designer-user-interface-report-builder.md)」および「[テキストベースのクエリ デザイナーのユーザー インターフェイス &#40;レポート ビルダー&#41;](text-based-query-designer-user-interface-report-builder.md)」を参照してください。  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] で使用されるグラフィカル クエリ デザイナーには、要約データのみを取得するクエリの作成に役立つグループ化と集計のサポートが組み込まれています。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 言語の機能には、GROUP BY 句、DISTINCT キーワード、および集計 (SUM、COUNT など) があります。 テキスト ベースのクエリ デザイナーでは、グループ化と集計が含まれている [!INCLUDE[tsql](../../includes/tsql-md.md)] 言語が完全にサポートされています。 [!INCLUDE[tsql](../../includes/tsql-md.md)] の詳細については、msdn.microsoft.com の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [オンライン ブック](https://go.microsoft.com/fwlink/?LinkId=141687)にある「[Transact-SQL リファレンス (データベース エンジン)](/sql/t-sql/language-reference)」を参照してください。  
  
###  <a name="QueryText"></a> Text の種類のクエリの使用  
 テキスト ベースのクエリ デザイナーでは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] コマンドを入力して、データセット内のデータを定義します。 たとえば、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリでは、マーケティング アシスタントであるすべての従業員の名前を選択します。  
  
```  
SELECT  
  HumanResources.Employee.BusinessEntityID  
  ,HumanResources.Employee.JobTitle  
  ,Person.Person.FirstName  
  ,Person.Person.LastName  
FROM  
  Person.Person  
  INNER JOIN HumanResources.Employee  
    ON Person.Person.BusinessEntityID = HumanResources.Employee.BusinessEntityID  
WHERE HumanResources.Employee.JobTitle = 'Marketing Assistant'   
```  
  
 ツール バーの **[実行]** ボタン (**!**) をクリックすると、クエリが実行され、結果セットが表示されます。  
  
 このクエリをパラメーター化するには、クエリ パラメーターを追加します。 たとえば、WHERE 句を次の構文に変更します。  
  
```  
WHERE HumanResources.Employee.JobTitle = (@JobTitle)  
```  
  
 クエリの実行時に、クエリ パラメーターに対応するレポート パラメーターが自動的に作成されます。 詳細については、このトピックの「 [クエリ パラメーター](#Parameters) 」を参照してください。  
  
  
  
###  <a name="QueryStoredProcedure"></a> StoredProcedure の種類のクエリの使用  
 データセット クエリのストアド プロシージャは、次のいずれかの方法で指定できます。  
  
-   **[データセットのプロパティ]** ダイアログ ボックスで、 **[ストアド プロシージャ]** オプションを設定します。 ドロップダウン リストからストアド プロシージャまたはテーブル値関数を選択します。  
  
-   リレーショナル クエリ デザイナーのデータベース ビュー ペインで、ストアド プロシージャまたはテーブル値関数を選択します。  
  
-   テキスト ベースのクエリ デザイナーで、ツール バーから **[StoredProcedure]** を選択します。  
  
 ストアド プロシージャまたはテーブル値関数を選択したら、クエリを実行できます。 入力パラメーター値の入力を要求されます。 クエリの実行時に、入力パラメーターに対応するレポート パラメーターが自動的に作成されます。 詳細については、このトピックの「 [クエリ パラメーター](#Parameters) 」を参照してください。  
  
 ストアド プロシージャから取得した最初の結果セットだけがサポートされます。 ストアド プロシージャから複数の結果セットが返された場合、最初の結果セットだけが使用されます。  
  
 既定値が指定されたパラメーターがストアド プロシージャに含まれている場合、パラメーターの値として DEFAULT キーワードを使用してその値にアクセスできます。 クエリ パラメーターがレポート パラメーターにリンクされている場合は、レポート パラメーターの入力ボックスで DEFAULT キーワードを入力または選択できます。  
  
 ストアド プロシージャの詳細については、msdn.microsoft.com にある [SQL Server オンライン ブック](https://go.microsoft.com/fwlink/?linkid=98335) の「ストアド プロシージャ (データベース エンジン)」を参照してください。  
  
  
  
##  <a name="Parameters"></a> パラメーター  
 入力パラメーターを含むクエリ変数またはストアド プロシージャがクエリ テキストに含まれている場合、対応するデータセットのクエリ パラメーターとレポートのレポート パラメーターが自動的に生成されます。 クエリ テキストには、各クエリ変数の DECLARE ステートメントを含めないでください。  
  
 たとえば、次の SQL クエリでは、`EmpID` という名前のレポート パラメーターが作成されます。  
  
```  
SELECT FirstName, LastName FROM HumanResources.Employee E INNER JOIN  
       Person.Contact C ON  E.ContactID=C.ContactID   
WHERE EmployeeID = (@EmpID)  
```  
  
 レポート パラメーターの既定のデータ型は Text です。各レポート パラメーターには自動的に作成されたデータセットが設定され、使用可能な値のドロップダウン リストで使用されます。 レポート パラメーターを作成した後に、既定値の変更が必要になる場合があります。 詳細については、「[レポート パラメーター &#40;レポート ビルダーおよびレポート デザイナー&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)」を参照してください。  
  
  
  
##  <a name="Remarks"></a> 解説  
  
###### <a name="alternate-data-extensions"></a>代替データ拡張機能  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースからのデータの取得は、ODBC のデータ ソースの種類を使用して行うこともできます。 OLE DB を使用した [!INCLUDE[ssSDS](../../includes/sssds-md.md)] への接続はサポートされていません。  
  
 詳細については、「[ODBC 接続の種類 &#40;SSRS&#41;](odbc-connection-type-ssrs.md)」を参照してください。  
  
###### <a name="platform-and-version-information"></a>プラットフォームおよびバージョン情報  
 プラットフォームおよびバージョン サポートの詳細については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [オンライン ブック](https://go.microsoft.com/fwlink/?linkid=121312)にある [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] ドキュメントの「[Reporting Services でサポートされるデータ ソース (SSRS)](../create-deploy-and-manage-mobile-and-paginated-reports.md)」を参照してください。  
  
  
  
##  <a name="HowTo"></a> 操作方法に関するトピック  
 データ接続、データ ソース、およびデータセットを操作する手順について説明します。  
  
 [データ接続またはデータ ソース追加および確認&#40;レポート ビルダーおよび SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [共有データセットまたは埋め込みデータセットの作成 (レポート ビルダーおよび SSRS)](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [データセットへのフィルターの追加 (レポート ビルダーおよび SSRS)](add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
  
##  <a name="Related"></a> 関連項目  
 次に示すセクションでは、レポート データの概念が詳細に説明されているほか、データに関連するレポートのパーツを定義しカスタマイズし使用する手順が説明されています。  
  
 [レポートにデータを追加&#40;レポート ビルダーおよび SSRS&#41;](report-datasets-ssrs.md)  
 レポートのデータへのアクセスの概要について説明します。  
  
 [レポート ビルダーでのデータ接続、データ ソース、および接続文字列](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
 データ接続とデータ ソースについて説明します。  
  
 [レポート埋め込みデータセットと共有データセット &#40;レポート ビルダーおよび SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 埋め込みデータセットと共有データセットについて説明します。  
  
 [データセット フィールド コレクション &#40;レポート ビルダーおよび SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)  
 クエリによって生成されるデータセット フィールド コレクションについて説明します。  
  
 [Reporting Services でサポートされるデータ ソース &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md) ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [オンライン ブック](https://go.microsoft.com/fwlink/?linkid=121312)の [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] ドキュメント)。  
 各データ拡張機能のプラットフォームおよびバージョン サポートに関する詳細な情報です。  
  
  
  
## <a name="see-also"></a>参照  
 [レポート パラメーター &#40;レポート ビルダーおよびレポート デザイナー&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [データのフィルター、グループ化、および並べ替え &#40;レポート ビルダーおよび SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [式 &#40;レポート ビルダーおよび SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
  
  
