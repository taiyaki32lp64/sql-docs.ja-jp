---
title: 結果セットで、SQL 実行タスク |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- result sets [Integration Services]
- Execute SQL task [Integration Services]
ms.assetid: 62605b63-d43b-49e8-a863-e154011e6109
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8efb049292caecf21f38ef5bc5a7392138bdcf5a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66056427"
---
# <a name="result-sets-in-the-execute-sql-task"></a>SQL 実行タスクにおける結果セット
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージでは、タスクが使用する SQL コマンドの種類によって、SQL 実行タスクに結果セットが返されるかどうかが決まります。 たとえば、通常、SELECT ステートメントは結果セットを返しますが、INSERT ステートメントは返しません。  
  
 結果セットに含まれる内容も、SQL コマンドによって異なります。 たとえば、SELECT ステートメントからの結果セットに含まれる行数は、0 行、1 行、または多数行である場合があります。 ただし、カウントや合計を返す SELECT ステートメントの結果セットに含まれるのは 1 行だけです。  
  
 SQL 実行タスクで結果セットを使用すると、SQL コマンドが結果セットを返すかどうかを確認したり、その結果セットの内容を把握するだけでなく、その他の情報も取得できます。 SQL 実行タスクで結果セットを正しく使用する際に必要となる、追加の使用要件やガイドラインがあります。 以降では、こうした使用要件およびガイドラインについて説明します。  
  
-   [結果セットの種類の指定](#Result_set_type)  
  
-   [結果セットによる変数の設定](#Populate_variable_with_result_set)  
  
-   [セットで、SQL 実行タスク エディターの結果の構成](#Configure_result_sets)  
  
##  <a name="Result_set_type"></a> 結果セットの指定の種類  
 SQL 実行タスクでサポートされている結果セットの種類は、次のとおりです。  
  
-   " **なし** " は、クエリが結果を返さない場合に使用される結果セットです。 たとえば、テーブルのレコードを追加、変更、および削除するクエリで使用されます。  
  
-   " **単一行** " は、クエリが返す行が 1 行のみの場合に使用される結果セットです。 たとえば、カウントや合計を返す SELECT ステートメントでこの結果セットが使用されます。  
  
-   " **完全な結果セット** " は、クエリが複数行を返す場合に使用される結果セットです。 たとえば、テーブル内のすべての行を取得する SELECT ステートメントでこの結果セットが使用されます。  
  
-   " **XML** " は、クエリが結果セットを XML 形式で返す場合に使用される結果セットです。 たとえば、FOR XML 句を含む SELECT ステートメントでこの結果セットが使用されます。  
  
 SQL 実行タスクが " **完全な結果セット** " の結果セットを使用し、クエリが複数の行セットを返す場合、タスクは最初の行セットのみを返します。 この行セットでエラーが発生すると、タスクはそのエラーをレポートします。 他の行セットでエラーが発生しても、タスクはエラーをレポートしません。  
  
##  <a name="Populate_variable_with_result_set"></a> 結果セットによる変数の設定  
 結果セットの種類が、単一行、行セット、または XML の場合、クエリが返す結果セットをユーザー定義の変数にバインドできます。  
  
 結果セットの種類が " **単一行**" の場合、列名を結果セットの名前として使用し、返される結果の列を変数にバインドしたり、列一覧の列の序数を結果セットの名前として使用できます。 たとえば、クエリ `SELECT Color FROM Production.Product WHERE ProductID = ?` の結果セットの名前は **Color** または **0**となります。 クエリが複数の列を返す場合に、すべての列の値にアクセスするには、各列を異なる変数にバインドする必要があります。 数字を結果セットの名前として使用し、列を変数にマップする場合、その数字はクエリの列一覧に列が表示される順序を示します。 たとえば、クエリ `SELECT Color, ListPrice, FROM Production.Product WHERE ProductID = ?`では、 **Color** 列に 0 を、 **ListPrice** 列に 1 を使用します。 列名を結果セットの名前として使用できるかどうかは、タスクの構成で指定されているプロバイダーによって異なります。 すべてのプロバイダーで列名が使用できるわけではありません。  
  
 単一の値を返す一部のクエリには、列名が含まれないことがあります。 たとえば、ステートメント `SELECT COUNT (*) FROM Production.Product` からは列名が返されません。 返される結果にアクセスするには、結果名として序数位置 0 を使用します。 列名で返される結果にアクセスするには、列名を指定する AS \<エイリアス名> 句をクエリに含める必要があります。 ステートメント `SELECT COUNT (*)AS CountOfProduct FROM Production.Product`では、 **CountOfProduct** 列を指定します。 その後、 **CountOfProduct** 列名または序数位置 0 を使用して、返された結果列にアクセスできます。  
  
 結果セットの種類が " **完全な結果セット** " または " **XML**" の場合、結果セット名には 0 を使用する必要があります。  
  
 結果セットの種類が " **単一行** " の結果セットに変数をマップする場合、変数のデータ型と結果セットに含まれる列のデータ型は互換性がある必要があります。 たとえば、`String` データ型の列を含む結果セットを、数値データ型の変数にマップすることはできません。 設定すると、 **TypeConversionMode**プロパティを`Allowed`、SQL 実行タスクが出力パラメーターの変換を試みるしに割り当てられているクエリの結果、変数の結果データを入力します。  
  
 XML 結果セットをマップできるのは、`String` または `Object` データ型の変数のみです。 変数が `String` データ型の場合、SQL 実行タスクは文字列を返し、XML ソースは XML データを使用できます。 変数が `Object` データ型の場合、SQL 実行タスクはドキュメント オブジェクト モデル (DOM) オブジェクトを返します。  
  
 A**完全な結果セット**の変数にマップする必要があります、`Object`データ型。 結果は、行セット オブジェクトとして返されます。 Foreach ループ コンテナーを使用して、Object 変数に格納されたテーブル行の値をパッケージ変数に抽出し、その後、スクリプト タスクを使用して、パッケージ変数に格納されたデータをファイルに書き出すことができます。 Foreach ループ コンテナーとスクリプト タスクを使用したこの処理方法のデモについては、msftisprodsamples.codeplex.com の CodePlex サンプル「 [Execute SQL Parameters and Result Sets (SQL 実行パラメーターと結果セット)](https://go.microsoft.com/fwlink/?LinkId=157863)」を参照してください。  
  
 次の表は、結果セットにマップできる変数のデータ型をまとめたものです。  
  
|結果セットの種類|変数のデータ型|オブジェクトの種類|  
|---------------------|---------------------------|--------------------|  
|単一行|結果セット内の型列と互換性のあるすべての型|適用なし|  
|完全な結果セット|`Object`|タスクで ADO、OLE DB、Excel、および ODBC 接続マネージャーを含むネイティブ接続マネージャー使用する場合、返されるオブジェクトは ADO `Recordset` です。<br /><br /> タスクで [!INCLUDE[vstecado](../includes/vstecado-md.md)] 接続マネージャーなどのマネージド接続マネージャーを使用する場合、返されるオブジェクトは `System.Data.DataSet` です。<br /><br /> 次の例に示すように、スクリプト タスクを使用して、`System.Data.DataSet` オブジェクトにアクセスできます。<br /><br /> `Dim dt As Data.DataTable` <br /> `Dim ds As Data.DataSet = CType(Dts.Variables("Recordset").Value, DataSet)` <br /> `dt = ds.Tables(0)`|  
|XML|`String`|`String`|  
|XML|`Object`|タスクで ADO、OLE DB、Excel、および ODBC 接続マネージャーを含むネイティブ接続マネージャー使用する場合、返されるオブジェクトは `MSXML6.IXMLDOMDocument` です。<br /><br /> タスクがなど、マネージ接続マネージャーを使用するかどうか、[!INCLUDE[vstecado](../includes/vstecado-md.md)]接続マネージャーでは、返されたオブジェクトは、`System.Xml.XmlDocument`します。|  
  
 変数は、SQL 実行タスクまたはパッケージのスコープ内で定義できます。 変数にパッケージ スコープがある場合、結果セットはパッケージ内の他のタスクやコンテナーで利用できます。また、パッケージ実行タスクや DTS 2000 パッケージ実行タスクが実行する任意のパッケージでも利用できます。  
  
 変数を **単一行** の結果セットにマップすると、次の条件が満たされている場合、SQL ステートメントによって返される、文字列以外の値が、文字列に変換されることがあります。  
  
-   **TypeConversionMode** プロパティが true に設定されている。 プロパティ値は、プロパティ ウィンドウで設定するか、 **SQL 実行タスク エディター**を使用して設定します。  
  
-   変換によってデータが切り捨てられない。  
  
 変数への結果セットの読み込みについては、「 [結果セットを SQL 実行タスクの変数にマップする](control-flow/execute-sql-task.md)」を参照してください。  
  
##  <a name="Configure_result_sets"></a> 結果の構成設定、SQL 実行タスク  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーで設定できる、結果セットのプロパティの詳細については、次のトピックを参照してください。  
  
-   [SQL 実行タスク エディター&#40;結果セット ページ&#41;](../../2014/integration-services/execute-sql-task-editor-result-set-page.md)  
  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](../../2014/integration-services/set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 [結果セットを SQL 実行タスクの変数にマップする](control-flow/execute-sql-task.md)  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   msftisprodsamples.codeplex.com の CodePlex サンプル「 [Execute SQL Parameters and Result Sets](https://go.microsoft.com/fwlink/?LinkId=157863)」  
  
  
