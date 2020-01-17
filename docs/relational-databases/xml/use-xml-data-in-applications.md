---
title: アプリケーションでの XML データの使用 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- parameters [XML in SQL Server]
- XML [SQL Server], ADO
- columns [XML in SQL Server], ADO.NET
- ADO [XML in SQL Server]
- columns [XML in SQL Server], SQL Server Native Client
- xml data type [SQL Server], ADO
- SQLNCLI, XML
- xml data type [SQL Server], SQL Server Native Client
- SQL Server Native Client, XML
- ADO.NET [XML in SQL Server]
- XML [SQL Server], ADO.NET
- columns [XML in SQL Server], ADO
- xml data type [SQL Server], ADO.NET
- XML [SQL Server], SQL Server Native Client
ms.assetid: 5dabf7e0-c6df-451d-a070-4661f84607fd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 998504b936681c5e20d185ab17b787630a6ae2f1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039156"
---
# <a name="use-xml-data-in-applications"></a>アプリケーションでの XML データの使用
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  このトピックでは、アプリケーションで **xml** データ型を操作する際のオプションについて説明します。 このトピックには、次の項目に関する情報が含まれています。  
  
-   ADO および **Native Client を使用した、** xml [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 型の列に含まれている XML の操作  
  
-   ADO.NET を使用した、 **xml** 型の列に含まれている XML の操作  
  
-   ADO.NET を使用した、パラメーターに含まれている **xml** 型の操作  
  
## <a name="handling-xml-from-an-xml-type-column-by-using-ado-and-sql-server-native-client"></a>ADO および SQL Server Native Client を使用した、xml 型の列に含まれている XML の操作  
 MDAC コンポーネントを使用して、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]に導入された型や機能にアクセスするためには、DataTypeCompatibility 初期化プロパティを ADO 接続文字列で設定する必要があります。  
  
 たとえば、次の Visual Basic Scripting Edition (VBScript) サンプルは、 **サンプル データベースの** テーブルにある、 `Demographics`xml `Sales.Store` データ型の列である `AdventureWorks2012` に対するクエリの結果を示しています。 具体的には、クエリは `CustomerID` が `3`と等しい行のこの列のインスタンス値を検索します。  
  
```  
Const DS = "MyServer"  
Const DB = "AdventureWorks2012"  
  
Set objConn = CreateObject("ADODB.Connection")  
Set objRs = CreateObject("ADODB.Recordset")  
  
CommandText = "SELECT Demographics" & _  
              " FROM Sales.Store" & _  
              " INNER JOIN Sales.Customer" & _  
              " ON Sales.Store.BusinessEntityID = sales.customer.StoreID" & _  
              " WHERE Sales.Customer.CustomerID = 3" & _  
              " OR Sales.Customer.CustomerID = 4"  
  
ConnectionString = "Provider=SQLNCLI11" & _  
                   ";Data Source=" & DS & _  
                   ";Initial Catalog=" & DB & _  
                   ";Integrated Security=SSPI;" & _  
                   "DataTypeCompatibility=80"  
  
'Connect to the data source.  
objConn.Open ConnectionString  
  
'Execute command through the connection and display  
Set objRs = objConn.Execute(CommandText)  
  
Dim rowcount  
rowcount = 0  
Do While Not objRs.EOF  
   rowcount = rowcount + 1  
   MsgBox "Row " & rowcount & _  
           vbCrLf & vbCrLf & objRs(0)  
   objRs.MoveNext  
Loop  
  
'Clean up.  
objRs.Close  
objConn.Close  
Set objRs = Nothing  
Set objConn = Nothing  
```  
  
 この例は、DataTypeCompatibility を設定する方法を示しています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client を使用している場合、このプロパティには既定値の 0 が設定されています。 この値を 80 に設定すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client プロバイダーにより、 **xml** 型およびユーザー定義型の列が [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] データ型として示されます。 それぞれのデータ型は、DBTYPE_WSTR および DBTYPE_BYTES になります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client はクライアント コンピューターにもインストールし、データ プロバイダーとして使用するために、"`Provider=SQLNCLI11;...`" を含む接続文字列を指定する必要があります。  
  
#### <a name="to-test-this-example"></a>この例をテストするには  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client がクライアント コンピューターにインストールされており、クライアント コンピューターで MDAC 2.6.0 以降のバージョンを使用できることを確認します。  
  
     詳細については、「 [SQL Server Native Client プログラミング](../../relational-databases/native-client/sql-server-native-client-programming.md)」を参照してください。  
  
2.  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サンプル データベースがインストールされていることを確認します。  
  
     この例では [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] サンプル データベースが必要です。  
  
3.  このトピックの前半に示したコードをコピーし、テキスト エディターまたはコード エディターに貼り付けます。 HandlingXmlDataType.vbs という名前でファイルを保存します。  
  
4.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストールでの必要性に応じてスクリプトを変更し、変更を保存します。  
  
     たとえば、 `MyServer` が指定されている箇所は、 `(local)` または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がインストールされているサーバーの実際の名前のいずれかに置き換える必要があります。  
  
5.  HandlingXmlDataType.vbs を実行し、スクリプトを実行します。  
  
 結果は次のサンプル出力に似たものになります。  
  
```  
Row 1  
  
<StoreSurvey xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/StoreSurvey">  
  <AnnualSales>1500000</AnnualSales>  
  <AnnualRevenue>150000</AnnualRevenue>  
  <BankName>Primary International</BankName>  
  <BusinessType>OS</BusinessType>  
  <YearOpened>1974</YearOpened>  
  <Specialty>Road</Specialty>  
  <SquareFeet>38000</SquareFeet>  
  <Brands>3</Brands>  
  <Internet>DSL</Internet>  
  <NumberEmployees>40</NumberEmployees>  
</StoreSurvey>  
  
Row 2  
  
<StoreSurvey xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/StoreSurvey">  
  <AnnualSales>300000</AnnualSales>  
  <AnnualRevenue>30000</AnnualRevenue>  
  <BankName>United Security</BankName>  
  <BusinessType>BM</BusinessType>  
  <YearOpened>1976</YearOpened>  
  <Specialty>Road</Specialty>  
  <SquareFeet>6000</SquareFeet>  
  <Brands>2</Brands>  
  <Internet>DSL</Internet>  
  <NumberEmployees>5</NumberEmployees>  
</StoreSurvey>  
```  
  
## <a name="handling-xml-from-an-xml-type-column-by-using-adonet"></a>ADO.NET を使用した、xml 型の列に含まれている XML の操作  
 ADO.NET および [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] を使用して、**xml** データ型の列に含まれている XML を操作するには、**SqlCommand** クラスの標準の動作を使用します。 たとえば、 **xml** データ型の列とその値は、 **SqlDataReader**を使用して SQL 列を取得するときと同じ方法で取得できます。ただし、XML として **xml** データ型の列のコンテンツを使用して作業を行う場合は、最初にそのコンテンツを **XmlReader** 型に割り当てる必要があります。  
  
 詳細とコード例については、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnlong](../../includes/dnprdnlong-md.md)] SDK のマニュアルの「XML Column Values in a Data Reader」を参照してください。  
  
## <a name="handling-an-xml-type-column-in-parameters-by-using-adonet"></a>ADO.NET を使用した、パラメーター内の xml 型の列の操作  
 ADO.NET および [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]でパラメーターとして渡された xml データ型を操作するには、 **SqlXml** データ型のインスタンスとして値を指定することができます。 特殊な処理は必要ありません。 **の** xml [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型の列は、 **string** や **integer**などの他の列やデータ型と同じように、パラメーター値を受け取ることができます。  
  
 詳細とコード例については、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnlong](../../includes/dnprdnlong-md.md)] SDK のマニュアルの「XML Values as Command Parameters」を参照してください。  
  
## <a name="see-also"></a>参照  
 [XML データ &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
