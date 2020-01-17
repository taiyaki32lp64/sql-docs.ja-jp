---
title: パラメーターとリターン コード、SQL 実行タスク |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- return codes [Integration Services]
- parameters [Integration Services]
- parameterized SQL statements [Integration Services]
- Execute SQL task [Integration Services]
ms.assetid: a3ca65e8-65cf-4272-9a81-765a706b8663
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 49ac4661e533b4c4e56a750f208c3ded09f72d27
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66056789"
---
# <a name="parameters-and-return-codes-in-the-execute-sql-task"></a>SQL 実行タスクのパラメーターとリターン コード
  SQL ステートメントとストアド プロシージャでは多くの場合、`input` パラメーター、`output` パラメーター、およびリターン コードを使用します。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] の SQL 実行タスクでは、`Input`、`Output`、および `ReturnValue` という、パラメーターの型がサポートされています。 入力パラメーターには `Input` 型、出力パラメーターには `Output` 型、およびリターン コードには `ReturnValue` 型を使用します。  
  
> [!NOTE]  
>  SQL 実行タスクでは、データ プロバイダーがサポートしている場合のみ、パラメーターを使用できます。  
  
 クエリやストアド プロシージャなど、SQL コマンドのパラメーターは、SQL 実行タスクのスコープ内、親コンテナー、またはパッケージのスコープ内に作成されたユーザー定義変数にマップされます。 変数の値はデザイン時に設定することも、実行時に動的に設定することもできます。 パラメーターは、システム変数にマップすることもできます。 詳細については、「[Integration Services &#40;SSIS&#41; の変数](integration-services-ssis-variables.md)」および「[システム変数](system-variables.md)」を参照してください。  
  
 SQL 実行タスクでパラメーターやリターン コードを使用すると、タスクでサポートされるパラメーターの型やこれらのパラメーターのマップ方法を把握するだけでなく、その他の情報も取得できます。 SQL 実行タスクでパラメーターおよびリターン コードを正しく使用する際に必要となる、追加の使用要件やガイドラインがあります。 以降では、こうした使用要件およびガイドラインについて説明します。  
  
-   [パラメーター名とパラメーター マーカーの使用](#Parameter_names_and_markers)  
  
-   [日付と時刻のデータ型のパラメーターの使用](#Date_and_time_data_types)  
  
-   [WHERE 句でのパラメーターの使用](#WHERE_clauses)  
  
-   [ストアド プロシージャでのパラメーターの使用](#Stored_procedures)  
  
-   [リターン コードの値の取得](#Return_codes)  
  
-   [構成パラメーターとリターン コードで、SQL 実行タスク エディター](#Configure_parameters_and_return_codes)  
  
##  <a name="Parameter_names_and_markers"></a> パラメーター名とパラメーター マーカーを使用します。  
 SQL コマンドの構文では、SQL 実行タスクが使用する接続の種類によって、異なるパラメーター マーカーが使用されます。 たとえば、[!INCLUDE[vstecado](../includes/vstecado-md.md)] 接続マネージャーの場合は、SQL コマンドが使用するパラメーター マーカーの形式を **\@varParameter** にする必要がありますが、OLE DB 接続の場合は疑問符 (?) パラメーター マーカーが必要です。  
  
 変数とパラメーターの間でのマッピングでパラメーター名として使用できる名前も、接続マネージャーの種類によって異なります。 たとえば、[!INCLUDE[vstecado](../includes/vstecado-md.md)] 接続マネージャーでは \@ プレフィックス付きのユーザー定義名を使用し、OLE DB 接続マネージャーではパラメーター名として 0 から始まる序数の数値を使用する必要があります。  
  
 次の表に、SQL 実行タスクで使用できる接続マネージャーの種類の SQL コマンドの要件をまとめます。  
  
|接続の種類|パラメーター マーカー|[パラメーター名]|SQL コマンドの例|  
|---------------------|----------------------|--------------------|-------------------------|  
|ADO (ADO)|?|Param1、Param2、...|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|\@\<パラメーター名>|\@\<パラメーター名>|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = \@parmContactID|  
|ODBC|?|1、2、3、...|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
|EXCEL および OLE DB|?|0、1、2、3、…|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
  
### <a name="using-parameters-with-adonet-and-ado-connection-managers"></a>ADO.NET 接続マネージャーおよび ADO 接続マネージャーでのパラメーターの使用  
 [!INCLUDE[vstecado](../includes/vstecado-md.md)] および ADO 接続マネージャーでは、パラメーターを使用する SQL コマンドに関する特定の要件があります。  
  
-   [!INCLUDE[vstecado](../includes/vstecado-md.md)] 接続マネージャーでは、SQL コマンド内のパラメーター マーカーとしてパラメーター名を使用することが必要になります。 これは、変数をパラメーターに直接マップできることを意味します。 たとえば、変数 `@varName` は、 `@parName` という名前のパラメーターにマップされ、パラメーター `@parName`に変数を提供します。  
  
-   ADO 接続マネージャーでは、SQL コマンド内のパラメーター マーカーとして疑問符 (?) を使用する必要があります。 ただし、パラメーター名として任意のユーザー定義名 (整数値を除く) を使用できます。  
  
 パラメーターに値を提供するプロセスで、変数がパラメーター名にマップされます。 その後、SQL 実行タスクがパラメーター リスト内にあるパラメーター名の序数値を使用して、変数からパラメーターに値を読み込みます。  
  
### <a name="using-parameters-with-excel-odbc-and-ole-db-connection-managers"></a>EXCEL、ODBC、および OLE DB 接続マネージャーでのパラメーターの使用  
 EXCEL、ODBC、および OLE DB の各接続マネージャーでは、SQL コマンド内のパラメーター マーカーとして疑問符 (?) を使用し、パラメーター名として 0 または 1 から始まる序数を使用する必要があります。 SQL 実行タスクで ODBC 接続マネージャーが使用される場合、クエリの最初のパラメーターにマップされるパラメーター名は 1 になります。それ以外の場合、パラメーター名は 0 になります。 後続のパラメーター名の数値は、パラメーター名のマップ先である SQL コマンドのパラメーターを示します。 たとえば、3 というパラメーター名は、SQL コマンド内の 3 番目の疑問符 (?) で表される、3 番目のパラメーターにマップされます。  
  
 パラメーターに値を提供するプロセスで、変数がパラメーター名にマップされ、SQL 実行タスクがパラメーター名の序数値を使用して、変数からパラメーターに値を読み込みます。  
  
 接続マネージャーが使用するプロバイダーによっては、一部の OLE DB データ型がサポートされないことがあります。 たとえば、Excel ドライバーは限定されたデータ型のセットしか認識しません。 Excel ドライバーでの Jet プロバイダーの動作の詳細については、「[Excel ソース](data-flow/excel-source.md)」を参照してください。  
  
#### <a name="using-parameters-with-ole-db-connection-managers"></a>OLE DB 接続マネージャーでのパラメーターの使用  
 SQL 実行タスクが OLE DB 接続マネージャーを使用する場合は、タスクの BypassPrepare プロパティを使用できます。 SQL 実行タスクが、パラメーターと共に SQL ステートメントを使用する場合は、このプロパティを `true` に設定する必要があります。  
  
 OLE DB 接続マネージャーを使用する場合、パラメーター化サブクエリは使用できません。これは、SQL 実行タスクが OLE DB プロバイダーを介してパラメーター情報を取得できないからです。 ただし、式を使用することで、パラメーター値をクエリ文字列に連結したり、タスクの SqlStatementSource プロパティを設定したりできます。  
  
##  <a name="Date_and_time_data_types"></a> 日付と時刻のデータ型とパラメーターの使用  
  
### <a name="using-date-and-time-parameters-with-adonet-and-ado-connection-managers"></a>ADO.NET 接続マネージャーおよび ADO 接続マネージャーでの日付と時刻のパラメーターの使用  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 型 (`time` および `datetimeoffset`) のデータを読み取る場合、[!INCLUDE[vstecado](../includes/vstecado-md.md)] 接続マネージャーまたは ADO 接続マネージャーのいずれかを使用する SQL 実行タスクには、次の追加要件があります。  
  
-   `time` 、データ、[!INCLUDE[vstecado](../includes/vstecado-md.md)]接続マネージャーは、パラメーターの型がパラメーターに格納するには、このデータを必要と`Input`または`Output`、データ型が`string`します。  
  
-   `datetimeoffset` 型のデータの場合、[!INCLUDE[vstecado](../includes/vstecado-md.md)] 接続マネージャーでは、次のいずれかのパラメーターにこのデータを格納する必要があります。  
  
    -   パラメーターの型が `Input` で、データ型が `string` のパラメーター。  
  
    -   パラメーターの型が `Output` または `ReturnValue` で、データ型が `datetimeoffset`、`string`、または `datetime2` のパラメーター。 データ型が `string` または `datetime2` のパラメーターを選択した場合、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ではデータが string または datetime2 に変換されます。  
  
-   ADO 接続マネージャーでは、`time` 型または `datetimeoffset` 型のデータを、パラメーターの型が `Input` または `Output` で、データ型が `adVarWchar` のパラメーターに格納する必要があります。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データ型の詳細とそれを [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] データ型にマッピングする方法については、「[データ型 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)」と「[Integration Services のデータ型](data-flow/integration-services-data-types.md)」を参照してください。  
  
### <a name="using-date-and-time-parameters-with-ole-db-connection-managers"></a>OLE DB 接続マネージャーでの日付と時刻のパラメーターの使用  
 OLE DB 接続マネージャーを使用する場合、SQL 実行タスクには、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データ型 (`date`、`time`、`datetime`、`datetime2`、および `datetimeoffset`) のデータに関して特定のストレージ要件があります。 このデータは、次のいずれかの型のパラメーターに格納する必要があります。  
  
-   NVARCHAR データ型の入力パラメーター。  
  
-   次の表に示す、適切なデータ型の出力パラメーター。  
  
    |`Output` パラメーターの型|Date データ型|  
    |-------------------------------|--------------------|  
    |DBDATE|`date`|  
    |DBTIME2|`time`|  
    |DBTIMESTAMP|`datetime`, `datetime2`|  
    |DBTIMESTAMPOFFSET|`datetimeoffset`|  
  
 データが適切な入力パラメーターまたは出力パラメーターに格納されないと、パッケージは失敗します。  
  
### <a name="using-date-and-time-parameters-with-odbc-connection-managers"></a>ODBC 接続マネージャーでの日付と時刻のパラメーターの使用  
 ODBC 接続マネージャーを使用する場合、SQL 実行タスクには、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データ型 (`date`、`time`、`datetime`、`datetime2`、または `datetimeoffset`) のデータに関して特定のストレージ要件があります。 このデータは、次のいずれかの型のパラメーターに格納する必要があります。  
  
-   SQL_WVARCHAR データ型の `input` パラメーター。  
  
-   次の表に示す、適切なデータ型の `output` パラメーター。  
  
    |`Output` パラメーターの型|Date データ型|  
    |-------------------------------|--------------------|  
    |SQL_DATE|`date`|  
    |SQL_SS_TIME2|`time`|  
    |SQL_TYPE_TIMESTAMP<br /><br /> \- または -<br /><br /> SQL_TIMESTAMP|`datetime`, `datetime2`|  
    |SQL_SS_TIMESTAMPOFFSET|`datetimeoffset`|  
  
 データが適切な入力パラメーターまたは出力パラメーターに格納されないと、パッケージは失敗します。  
  
##  <a name="WHERE_clauses"></a> パラメーターを使用して、where 句  
 SELECT、INSERT、UPDATE、および DELETE コマンドには、多くの場合、WHERE 句が含まれています。WHERE 句は、SQL コマンドを限定するために、ソース テーブル内の各行が満たすべき条件を定義したフィルターの役割を果たします。 パラメーターは、WHERE 句で使用されるフィルター値を提供します。  
  
 パラメーター マーカーを使用して、パラメーター値を動的に指定できます。 SQL ステートメントで使用できるパラメーター マーカーとパラメーター名に関する規則は、SQL 実行タスクで使用される接続マネージャーの種類によって異なります。  
  
 次の表に、SELECT コマンドの例を接続マネージャーの種類別に示します。 INSERT、UPDATE、および DELETE ステートメントでも同様です。 この例では、SELECT を使用して、2 つのパラメーターで指定された値よりも **ProductID** の値が大きい製品と小さい製品を、[!INCLUDE[ssSampleDBUserInputNonLocal](../includes/sssampledbuserinputnonlocal-md.md)] の **Product** テーブルから返します。  
  
|接続の種類|SELECT 構文|  
|---------------------|-------------------|  
|EXCEL、ODBC、OLEDB|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
|ADO (ADO)|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|`SELECT* FROM Production.Product WHERE ProductId > @parmMinProductID AND ProductID < @parmMaxProductID`|  
  
 この例では、次の名前のパラメーターが必要になります。  
  
-   EXCEL 接続マネージャーと OLE DB 接続マネージャーでは、パラメーター名 0 と 1 を使用します。 ODBC 接続では、1 と 2 を使用します。  
  
-   ADO 接続では、Param1 や Param2 など、任意の 2 つのパラメーター名を使用します。ただし、これらのパラメーター名は、パラメーター リストの序数位置によってマップされる必要があります。  
  
-   [!INCLUDE[vstecado](../includes/vstecado-md.md)] 接続では、パラメーター名 \@parmMinProductID と \@parmMaxProductID を使用します。  
  
##  <a name="Stored_procedures"></a> ストアド プロシージャでパラメーターを使用  
 ストアド プロシージャを実行する SQL コマンドでは、パラメーター マッピングを使用することもできます。 パラメーター マーカーとパラメーター名の使用方法に関する規則は、パラメーター化クエリの規則と同様に、SQL 実行タスクで使用される接続マネージャーの種類によって異なります。  
  
 次の表に、EXEC コマンドの例を接続マネージャーの種類別に示します。 この例では、 **の** uspGetBillOfMaterials [!INCLUDE[ssSampleDBUserInputNonLocal](../includes/sssampledbuserinputnonlocal-md.md)]ストアド プロシージャを実行します。 このストアド プロシージャでは、`input` パラメーター `@StartProductID` と `@CheckDate` を使用します。  
  
|接続の種類|EXEC 構文|  
|---------------------|-----------------|  
|EXCEL および OLEDB|`EXEC uspGetBillOfMaterials ?, ?`|  
|ODBC|`{call uspGetBillOfMaterials(?, ?)}`<br /><br /> ODBC の呼び出し構文の詳細については、MSDN ライブラリの ODBC プログラマ リファレンスにある「[プロシージャのパラメーター](https://go.microsoft.com/fwlink/?LinkId=89462)」を参照してください。|  
|ADO (ADO)|IsQueryStoredProcedure に設定されている場合`False`、 `EXEC uspGetBillOfMaterials ?, ?`<br /><br /> IsQueryStoredProcedure に設定されている場合`True`、 `uspGetBillOfMaterials`|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|IsQueryStoredProcedure に設定されている場合`False`、 `EXEC uspGetBillOfMaterials @StartProductID, @CheckDate`<br /><br /> IsQueryStoredProcedure に設定されている場合`True`、 `uspGetBillOfMaterials`|  
  
 出力パラメーターを使用するには、構文で各パラメーター マーカーの後に OUTPUT キーワードを指定する必要があります。 たとえば、`EXEC myStoredProcedure ? OUTPUT` という出力パラメーターの構文は正しい構文です。  
  
 Transact-SQL ストアド プロシージャでの入力パラメーターと出力パラメーターの使用の詳細については、「[EXECUTE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/execute-transact-sql)」を参照してください。  
  
##  <a name="Return_codes"></a> リターン コードの値の取得  
 ストアド プロシージャは、リターン コードという整数値を返してプロシージャの実行状態を表すことができます。 SQL 実行タスクにリターン コードを実装するには、`ReturnValue` 型のパラメーターを使用します。  
  
 次の表に、リターン コードを実装する EXEC コマンドの一部の例を接続の種類別に示します。 すべての例で、`input` パラメーターを使用します。 パラメーター マーカーとパラメーター名を使用する方法に関する規則は、すべてのパラメーターの種類-同じ`Input`、 `Output`、および`ReturnValue`します。  
  
 一部の構文では、パラメーターのリテラルがサポートされません。 その場合は、変数を使用してパラメーター値を指定する必要があります。  
  
|接続の種類|EXEC 構文|  
|---------------------|-----------------|  
|EXCEL および OLEDB|`EXEC ? = myStoredProcedure 1`|  
|ODBC|`{? = call myStoredProcedure(1)}`<br /><br /> ODBC の呼び出し構文の詳細については、MSDN ライブラリの ODBC プログラマ リファレンスにある「[プロシージャのパラメーター](https://go.microsoft.com/fwlink/?LinkId=89462)」を参照してください。|  
|ADO (ADO)|IsQueryStoreProcedure に設定されている場合`False`、 `EXEC ? = myStoredProcedure 1`<br /><br /> IsQueryStoreProcedure に設定されている場合`True`、 `myStoredProcedure`|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|IsQueryStoreProcedure に設定されている`True`します。<br /><br /> `myStoredProcedure`|  
  
 前の表に示した構文では、SQL 実行タスクは **[直接入力]** ソース タイプを使用してストアド プロシージャを実行します。 SQL 実行タスクは **[ファイル接続]** ソース タイプを使用してストアド プロシージャを実行することもできます。 SQL 実行タスクを使用しているかどうかに関係なく、**直接入力**または**ファイル接続**ソース タイプのパラメーターを使用して、`ReturnValue`リターン コードを実装する型。 SQL 実行タスクで実行される SQL ステートメントのソース タイプの構成方法の詳細については、「[[SQL 実行タスク エディター] &#40;[全般] タブ&#41;](general-page-of-integration-services-designers-options.md)」を参照してください。  
  
 Transact-SQL ストアド プロシージャでのリターン コードの使用の詳細については、「[RETURN &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/return-transact-sql)」を参照してください。  
  
##  <a name="Configure_parameters_and_return_codes"></a> 構成パラメーターとリターン コードで、SQL 実行タスク  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーで設定できる、パラメーターとリターン コードのプロパティの詳細については、次のトピックを参照してください。  
  
-   [SQL 実行タスク エディター&#40;パラメーター マッピング ページ&#41;](../../2014/integration-services/execute-sql-task-editor-parameter-mapping-page.md)  
  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](../../2014/integration-services/set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 [タスクまたはコンテナーのプロパティを設定する](../../2014/integration-services/set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   blogs.msdn.com のブログ「[出力パラメーターを使用するストアド プロシージャ](https://go.microsoft.com/fwlink/?LinkId=157786)」  
  
-   msftisprodsamples.codeplex.com の CodePlex サンプル「 [Execute SQL Parameters and Result Sets](https://go.microsoft.com/fwlink/?LinkId=157863)」  
  
## <a name="see-also"></a>参照  
 [SQL 実行タスク](control-flow/execute-sql-task.md)   
 [SQL 実行タスクにおける結果セット](../../2014/integration-services/result-sets-in-the-execute-sql-task.md)  
  
  
