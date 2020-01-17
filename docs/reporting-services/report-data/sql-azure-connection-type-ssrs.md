---
title: SQL Azure の接続の種類 (SSRS) | Microsoft Docs
description: SQL Azure の接続のデータ拡張機能は、接続文字列とは個別に管理される、複数の値を持つパラメーター、サーバー集計、および資格情報をサポートしています。
author: maggiesMSFT
ms.author: maggies
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.date: 02/15/2019
monikerRange: '>= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d3eccb52c9a7164285627063f23dbb790b6dfa3c
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594065"
---
# <a name="sql-azure-connection-type-ssrs"></a>SQL Azure の接続の種類 (SSRS)

[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] は、ホストされているクラウドベースのリレーショナル データベースで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テクノロジを利用して構築されています。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] からのデータをレポートに含めるには、 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]の種類のレポート データ ソースに基づいたデータセットが必要です。 このビルトイン データ ソースの種類は、 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] データ拡張機能に基づいています。 このデータ ソースの種類を使用して、 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]からのデータに接続し、そのデータを取得します。  
  
このデータ拡張機能は、接続文字列とは個別に管理される、複数の値を持つパラメーター、サーバー集計、および資格情報をサポートしています。  
  
[!INCLUDE[ssSDS](../../includes/sssds-md.md)] は、オンプレミスの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスと似ています。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] からは、一部の例外を除き、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]と同じようにデータを取得できます。  
  
> [!NOTE]  
> [!INCLUDE[ssSDS](../../includes/sssds-md.md)]への接続を開くときに、接続タイムアウトを 30 秒に設定してください。
  
詳細については、[docs.microsoft.com で Microsoft Azure SQL Database のドキュメント](https://docs.microsoft.com/azure/sql-database/)を参照してください。  
  
このトピックの情報を使用して、データ ソースを構築してください。 手順については、「 [データ接続を追加および確認する (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="Connection"></a> 接続文字列

[!INCLUDE[ssSDS](../../includes/sssds-md.md)] に接続する場合、クラウド内のデータベース オブジェクトに接続します。 オンサイトのデータベースと同様に、ホストされているデータベースには、複数のテーブル、ビュー、およびストアド プロシージャを含むスキーマが複数存在している場合があります。 クエリ デザイナーで、使用するデータベース オブジェクトを指定します。 接続文字列でデータベースを指定しない場合は、管理者によって割り当てられた既定のデータベースに接続されます。  
  
データ ソースへの接続に使用する接続情報および資格情報については、データベース管理者に問い合わせてください。 AdventureWorks というホストされているサンプル データベースを指定する接続文字列の例を次に示します。  
  
```
Data Source=<host>;Initial Catalog=AdventureWorks; Encrypt=True;  
```
  
また、 **[データ ソースのプロパティ]** ダイアログ ボックスを使用して、ユーザー名やパスワードなどの資格情報を入力します。 `User Id` オプションと `Password` オプションは、接続文字列に自動的に付加されます。これらを接続文字列の一部として入力する必要はありません。  
  
詳細および接続文字列の例については、「 [レポート ビルダーでのデータ接続、データ ソース、および接続文字列](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="Credentials"></a> [資格情報]

Windows 認証 (統合セキュリティ) はサポートされていません。 Windows 認証を使用して [!INCLUDE[ssSDS](../../includes/sssds-md.md)] に接続しようとすると、エラーが発生します。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] でサポートされているのが SQL Server 認証 (ユーザー名とパスワード) のみであるため、ユーザーは [!INCLUDE[ssSDS](../../includes/sssds-md.md)]に接続するたびに資格情報 (ログインとパスワード) を入力する必要があります。  
  
データベースにアクセスするには、十分な資格情報が必要です。 クエリによっては、他の権限 (ストアド プロシージャを実行したり、テーブルやビューにアクセスしたりするために必要な権限) が必要な場合があります。 外部データ ソースの所有者は、十分な資格情報を構成して、ユーザーが必要とするデータベース オブジェクトに対する読み取り専用アクセスを提供する必要があります。  
  
レポート作成クライアントから、次のオプションを使用して資格情報を指定します。  
  
- 保存されているユーザー名とパスワードを使用する。 レポート データを格納するデータベースがレポート サーバーとは別のサーバーに存在する場合に発生するダブル ホップに対処するには、資格情報を Windows 資格情報として使用するオプションを選択します。 データ ソースに接続した後に、認証されているユーザーの権限を借用するオプションもあります。  
  
- 資格情報を必要としない。 このオプションを使用するには、レポート サーバーで自動実行アカウントを構成しておく必要があります。 詳細については、「[自動実行アカウントを構成する &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)」を参照してください。  
  
詳細については、「[データ接続、データソース、および&#40;接続文字列レポートビルダー&#41;と SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) 」または「[レポートデータソースに関する資格情報と接続情報の指定](specify-credential-and-connection-information-for-report-data-sources.md)」を参照してください。  
  
## <a name="Query"></a> クエリ

クエリでは、レポート データセット用に取得するデータを指定します。 クエリの結果セットの列には、データセットのフィールド コレクションが設定されます。 クエリで複数の結果セットが返された場合にレポートによって処理されるのは、クエリから取得された最初の結果セットだけです。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と [!INCLUDE[ssSDS](../../includes/sssds-md.md)]の間には、サポートされるデータベースのサイズなど、いくつか違いがありますが、 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]に対するクエリの作成方法と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに対するクエリの作成方法はほぼ同じです。 [!INCLUDE[tsql](../../includes/tsql-md.md)] では、BACKUP などの一部の [!INCLUDE[ssSDS](../../includes/sssds-md.md)] ステートメントがサポートされていませんが、これらはレポート クエリで使用するステートメントではありません。 詳細については、「[SQL Server の接続の種類 (SSRS)](../../reporting-services/report-data/sql-server-connection-type-ssrs.md)」を参照してください。  
  
新しいクエリを作成するか、グラフィカル クエリ デザイナーで表示できる既存のクエリを開く場合、既定でリレーショナル クエリ デザイナーを使用できます。 クエリは、次の方法で指定できます。  
  
- クエリを対話形式で作成します。 データベース スキーマ別に編成された、テーブル、ビュー、ストアド プロシージャ、およびその他のデータベース アイテムの階層ビューが表示されるリレーショナル クエリ デザイナーを使用します。 テーブルまたはビューから列を選択するか、ストアド プロシージャまたはテーブル値関数を指定します。 フィルター条件を指定して、取得するデータの行数を制限します。 パラメーター オプションを設定してレポートの実行時にフィルターをカスタマイズします。  
  
- クエリを入力するか、貼り付けます。 テキスト ベースのクエリ デザイナーは、[!INCLUDE[tsql](../../includes/tsql-md.md)] テキストを直接入力する、クエリ テキストを別のソースから貼り付ける、リレーショナル クエリ デザイナーでは作成できない複雑なクエリを入力する、クエリ ベースの式を入力する、などの場合に使用します。  
  
- ファイルまたはレポートから既存のクエリをインポートします。 クエリ デザイナーの **[クエリのインポート]** ボタンを使用して、.sql ファイルまたは .rdl ファイルを参照し、クエリをインポートします。  
  
テキスト ベースのクエリ デザイナーでは、次の 2 つのモードがサポートされています。  
  
- [テキスト](#QueryText) : データ ソースからデータを選択する [!INCLUDE[tsql](../../includes/tsql-md.md)] コマンドを入力します。  
  
- [ストアド プロシージャ](#QueryStoredProcedure) : ストアド プロシージャの一覧から選択します。  
  
詳細については、「[リレーショナル クエリ デザイナーのユーザー インターフェイス &#40;レポート ビルダー&#41;](../../reporting-services/report-data/relational-query-designer-user-interface-report-builder.md)」および「[テキストベースのクエリ デザイナーのユーザー インターフェイス &#40;レポート ビルダー&#41;](../../reporting-services/report-data/text-based-query-designer-user-interface-report-builder.md)」を参照してください。  
  
[!INCLUDE[ssSDS](../../includes/sssds-md.md)] で使用されるグラフィカル クエリ デザイナーには、要約データのみを取得するクエリの作成に役立つグループ化と集計のサポートが組み込まれています。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 言語の機能には、GROUP BY 句、DISTINCT キーワード、および集計 (SUM、COUNT など) があります。 テキスト ベースのクエリ デザイナーでは、グループ化と集計が含まれている [!INCLUDE[tsql](../../includes/tsql-md.md)] 言語が完全にサポートされています。 [!INCLUDE[tsql](../../includes/tsql-md.md)] の詳細については、「[Transact-SQL リファレンス &#40;データベース エンジン&#41;](../../t-sql/transact-sql-reference-database-engine.md)」を参照してください。  
  
### <a name="QueryText"></a> Text の種類のクエリの使用

テキスト ベースのクエリ デザイナーでは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] コマンドを入力して、データセット内のデータを定義します。 たとえば、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリでは、マーケティング アシスタントであるすべての従業員の名前を選択します。

```sql
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

ツール バーの **[実行]** ボタン ( **!** ) をクリックすると、クエリが実行され、結果セットが表示されます。  
  
このクエリをパラメーター化するには、クエリ パラメーターを追加します。 たとえば、WHERE 句を次の構文に変更します。  

```sql
WHERE HumanResources.Employee.JobTitle = (@JobTitle)  
```

クエリの実行時に、クエリ パラメーターに対応するレポート パラメーターが自動的に作成されます。 詳細については、このトピックの「 [クエリ パラメーター](#Parameters) 」を参照してください。  
  
### <a name="QueryStoredProcedure"></a> StoredProcedure の種類のクエリの使用

データセット クエリのストアド プロシージャは、次のいずれかの方法で指定できます。  
  
- **[データセットのプロパティ]** ダイアログ ボックスで、 **[ストアド プロシージャ]** オプションを設定します。 ドロップダウン リストからストアド プロシージャまたはテーブル値関数を選択します。  
  
- リレーショナル クエリ デザイナーのデータベース ビュー ペインで、ストアド プロシージャまたはテーブル値関数を選択します。  
  
- テキスト ベースのクエリ デザイナーで、ツール バーから **[StoredProcedure]** を選択します。  
  
ストアド プロシージャまたはテーブル値関数を選択したら、クエリを実行できます。 入力パラメーター値の入力を要求されます。 クエリの実行時に、入力パラメーターに対応するレポート パラメーターが自動的に作成されます。 詳細については、このトピックの「 [クエリ パラメーター](#Parameters) 」を参照してください。  
  
ストアド プロシージャから取得した最初の結果セットだけがサポートされます。 ストアド プロシージャから複数の結果セットが返された場合、最初の結果セットだけが使用されます。  
  
既定値が指定されたパラメーターがストアド プロシージャに含まれている場合、パラメーターの値として DEFAULT キーワードを使用してその値にアクセスできます。 クエリ パラメーターがレポート パラメーターにリンクされている場合は、レポート パラメーターの入力ボックスで DEFAULT キーワードを入力または選択できます。  
  
ストアド プロシージャの詳細については、「[ストアド プロシージャ (データベース エンジン)](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)」を参照してください。  
  
## <a name="Parameters"></a> パラメーター

入力パラメーターを含むクエリ変数またはストアド プロシージャがクエリ テキストに含まれている場合、対応するデータセットのクエリ パラメーターとレポートのレポート パラメーターが自動的に生成されます。 クエリ テキストには、各クエリ変数の DECLARE ステートメントを含めないでください。  
  
 たとえば、次の SQL クエリでは、 **EmpID**という名前のレポート パラメーターが作成されます。  

```sql
SELECT FirstName, LastName FROM HumanResources.Employee E INNER JOIN  
       Person.Contact C ON  E.ContactID=C.ContactID   
WHERE EmployeeID = (@EmpID)  
```

レポート パラメーターの既定のデータ型は Text です。各レポート パラメーターには自動的に作成されたデータセットが設定され、使用可能な値のドロップダウン リストで使用されます。 レポート パラメーターを作成した後に、既定値の変更が必要になる場合があります。 詳細については、MSDN の「 [レポート パラメーター &#40;レポート ビルダーおよびレポート デザイナー&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)の種類のレポート データ ソースに基づいたデータセットが必要です。  

## <a name="Remarks"></a> 解説
  
###### <a name="alternate-data-extensions"></a>代替データ拡張機能

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースからのデータの取得は、ODBC のデータ ソースの種類を使用して行うこともできます。 OLE DB を使用した [!INCLUDE[ssSDS](../../includes/sssds-md.md)] への接続はサポートされていません。  
  
詳細については、「[ODBC 接続の種類 &#40;SSRS&#41;](../../reporting-services/report-data/odbc-connection-type-ssrs.md)」を参照してください。  
  
###### <a name="platform-and-version-information"></a>プラットフォームおよびバージョン情報

プラットフォームとバージョンのサポートについて詳しくは、「[Reporting Services でサポートされるデータ ソース &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)」をご覧ください。  

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"

## <a name="azure-sql-database-and-aad"></a>Azure SQL データベースと AAD

Azure SQL Database は Azure Active Directory (AAD) パススルー認証と共に使用できます。

このシナリオは、以下の項目を正しく設定した場合にサポートされます。

- [SQL Server 用の Active Directory 認証ライブラリ (ADALSQL) ](https://www.microsoft.com/en-us/download/details.aspx?id=48742) がレポート サーバーにインストールされている。
- [Active Directory フェデレーション サービス (AD FS)](https://docs.microsoft.com/windows-server/identity/active-directory-federation-services) が、オンプレミスの Active Directory (AD) と AAD 全体で連携するように構成されている。
- [Kerberos の制約付き委任 (KCD)](https://docs.microsoft.com/windows-server/security/kerberos/kerberos-constrained-delegation-overview) がレポート サーバーから ADFS サーバーに対して構成されている。
- レポートを表示するユーザーとして [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview) に対する認証を受けるようにレポート/データ ソースを構成している。

::: moniker-end

## <a name="HowTo"></a> 操作方法に関するトピック

データ接続、データ ソース、およびデータセットを操作する手順について説明します。  
  
[データ接続を追加および確認する (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
[共有データセットまたは埋め込みデータセットの作成 (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
[データセットへのフィルターの追加 (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
## <a name="Related"></a> 関連項目

次に示すセクションでは、レポート データの概念が詳細に説明されているほか、データに関連するレポートのパーツを定義しカスタマイズし使用する手順が説明されています。  
  
[レポート データセット &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
レポートのデータへのアクセスの概要について説明します。  
  
[レポート ビルダーでのデータ接続、データ ソース、および接続文字列](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
データ接続とデータ ソースについて説明します。  
  
[レポート埋め込みデータセットと共有データセット (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
埋め込みデータセットと共有データセットについて説明します。  
  
[データセット フィールド コレクション (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
クエリによって生成されるデータセット フィールド コレクションについて説明します。  
  
[Reporting Services でサポートされるデータ ソース &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)。  
各データ拡張機能のプラットフォームおよびバージョン サポートに関する詳細な情報です。  
  
## <a name="see-also"></a>参照

[docs.microsoft.com の Microsoft Azure SQL Database のドキュメント](https://docs.microsoft.com/azure/sql-database/)  
[レポート パラメーター (レポート ビルダーおよびレポート デザイナー)](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
[データのフィルター、グループ化、および並べ替え (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
[式 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  

