---
title: テキストベースのクエリデザイナーのユーザーインターフェイス |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10010"
- sql12.rtp.rptdesigner.dataview.genericquerydesigner.f1
helpviewer_keywords:
- text-based query designer [Reporting Services]
- query designers [Reporting Services], text-based
ms.assetid: 44b7c664-03aa-494e-a484-052b318e810c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ceec7e4a58b98763f7a3215d29087eb948ec0b41
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68891324"
---
# <a name="text-based-query-designer-user-interface"></a>テキストベースのクエリ デザイナーのユーザー インターフェイス
  デザイン時に、データ ソースでサポートされているクエリ言語でクエリを指定し、クエリを実行し、結果を表示するには、テキスト ベースのクエリ デザイナーを使用します。 複数の [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメント、カスタム データ処理拡張機能のクエリまたはコマンド構文、および式としてのクエリを指定できます。 テキスト ベースのクエリ デザイナーはクエリを前処理せず、あらゆる種類のクエリ構文に対応できるため、これは多くの種類のデータ ソースで既定のクエリ デザイナー ツールになっています。  
  
 テキスト ベースのクエリ デザイナーでは、ツール バーと次の 2 つのペインが表示されます。  
  
-   **クエリ**クエリテキスト、テーブル名、またはストアドプロシージャ名が表示されます。  
  
-   **[結果]** デザイン時にクエリの実行結果が表示されます。  
  
## <a name="text-based-query-designer-toolbar"></a>テキスト ベースのクエリ デザイナーのツール バー  
 テキスト ベースのクエリ デザイナーで使用できるツール バーは、コマンドの種類に関係なく 1 つだけです。 次の表は、ツール バーの各ボタンとその機能を示しています。  
  
|ボタン|説明|  
|------------|-----------------|  
|**[テキストとして編集]**|テキスト ベースのクエリ デザイナーと、グラフィカル クエリ デザイナー間で切り替えます。 すべての種類のデータ ソースでグラフィカル クエリ デザイナーがサポートされているとは限りません。|  
|**[インポート]**|ファイルまたはレポートから既存のクエリをインポートします。 サポートされているファイルの種類は sql と rdl だけです。 詳細については、「 [レポート埋め込みデータセットと共有データセット &#40;レポート ビルダーおよび SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)と呼ばれます。|  
|![クエリを実行する](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-run.gif "クエリを実行する")|クエリを実行し、その結果セットを結果ペインに表示します。|  
|**[コマンドの種類]**|**[Text]** 、 **[StoredProcedure]** 、または **[TableDirect]** を選択します。 パラメーターを受け取るストアド プロシージャの場合、ツール バーの **[実行]** をクリックすると、 **[クエリ パラメーターの定義]** ダイアログ ボックスが表示され、必要な値を入力できます。 ストアドプロシージャから複数の結果セットが返された場合は、最初の結果セットのみを使用してデータセットが設定されることに注意してください。<br /><br /> サポートされるコマンドの種類は、データ ソースの種類によって異なります。 たとえば、 **[TableDirect]** がサポートされるのは、OLE DB と ODBC だけです。|  
  
### <a name="command-type-text"></a>コマンドの種類 (Text)  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データセットを作成するとき、レポート デザイナーには既定によりグラフィカル クエリ デザイナーが表示されます。 テキスト ベースのクエリ デザイナーに切り替えるには、ツール バーの **[テキストとして編集]** 切り替えボタンをクリックします。 テキスト ベースのクエリ デザイナーは、クエリ ペインと結果ペインの 2 つのペインで構成されています。 次の図に各ペインの名称を示します。  
  
 ![リレーショナル データのクエリに使用する汎用クエリ デザイナー](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqd-dsaw-sql-generic.gif "リレーショナル データのクエリに使用する汎用クエリ デザイナー")  
  
 次の表に各ペインの機能を示します。  
  
|ペイン|機能|  
|----------|--------------|  
|Query|[!INCLUDE[tsql](../includes/tsql-md.md)] クエリ テキストを表示します。 [!INCLUDE[tsql](../includes/tsql-md.md)] クエリを記述または編集する際に、このペインを使用します。|  
|結果|クエリの結果を表示します。 クエリを実行するには、任意のペインで右クリックして、 **[実行]** をクリックするか、ツール バーの **[実行]** ボタンをクリックします。|  
  
#### <a name="example"></a>例  
 次のクエリは、[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] データベースの `Contact` テーブルから姓の一覧を取得します。  
  
```  
SELECT LastName FROM Person.Person;  
```  
  
 `EXEC` ステートメントを含むコマンドの種類 (Text) のすべての [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントを使用できます。 次のクエリでは、[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] のストアド プロシージャである `uspGetEmployeeManagers` を呼び出して、識別番号が 1 である従業員の指揮系統を取得しています。  
  
```  
EXEC uspGetEmployeeManagers 1;  
```  
  
 ツール バーの **[実行]** をクリックすると、 **クエリ** ペインのコマンドが実行され、その結果が **結果** ペインに表示されます。  
  
### <a name="command-type-storedprocedure"></a>コマンドの種類 (StoredProcedure)  
 **[コマンドの種類] で [StoredProcedure]** を選択した場合、テキスト ベースのクエリ デザイナーには、クエリ ペインと結果ペインの 2 つのペインが表示されます。 ストアド プロシージャ名をクエリ ペインに入力し、ツール バーの **[実行]** をクリックします。 [クエリ パラメーターの定義] ダイアログ ボックスが表示されます。 ストアド プロシージャのパラメーター値を入力します。 すべてのストアド プロシージャ パラメーターについて、レポート パラメーターが作成されます。  
  
#### <a name="example"></a>例  
 次のクエリでは、[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] ストアド プロシージャである `uspGetEmployeeManagers` を呼び出します。 クエリを実行する場合は、従業員 ID 番号パラメーターの値を入力する必要があります。  
  
```  
uspGetEmployeeManagers;  
```  
  
### <a name="command-type-tabledirect"></a>コマンドの種類 (TableDirect)  
 **[コマンドの種類] で [TableDirect]** を選択した場合、テキスト ベースのクエリ デザイナーには、クエリ ペインと結果ペインの 2 つのペインが表示されます。 テーブルを入力し、 **[実行]** ボタンをクリックすると、そのテーブルのすべての列が返されます。  
  
#### <a name="example"></a>例  
 次のクエリでは、[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] データベースのすべての顧客を結果セットとして取得しています。  
  
 `Sales.Customer`  
  
 テーブル名として「Sales. Customer」と入力すると、 [!INCLUDE[tsql](../includes/tsql-md.md)]ステートメント`SELECT * FROM Sales.Customer;`の作成に相当します。  
  
## <a name="see-also"></a>関連項目  
 [レポートデザイナー SQL Server Data Tools &#40;SSRS のクエリデザインツール&#41;](report-data/query-design-tools-ssrs.md)   
 [レポート埋め込みデータセットと共有データセット &#40;レポート ビルダーおよび SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [SQL Server の接続の種類 &#40;SSRS&#41;](report-data/sql-server-connection-type-ssrs.md)   
 [OLE DB の接続の種類 &#40;SSRS&#41;](report-data/ole-db-connection-type-ssrs.md)   
 [ODBC 接続の&#40;種類 SSRS&#41;](report-data/odbc-connection-type-ssrs.md)   
 [レポート埋め込みデータセットと共有データセット &#40;レポート ビルダーおよび SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [RSReportDesigner 構成ファイル](report-server/rsreportdesigner-configuration-file.md)  
  
  
