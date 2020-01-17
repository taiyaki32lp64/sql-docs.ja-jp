---
title: XML レポート データの XML クエリ構文 (SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- namespaces [Reporting Services]
- data processing extensions [Reporting Services], data sources
- xmldp [Reporting Services]
- XML [Reporting Services], data retrieval
ms.assetid: d203886f-faa1-4a02-88f5-dd4c217181ef
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3fc3cddc10dd53225867b910b8a3b3cb9c73d6ca
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65574857"
---
# <a name="xml-query-syntax-for-xml-report-data-ssrs"></a>XML レポート データの XML クエリ構文 (SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]では、XML データ ソースのデータセットを作成できます。 データセットを取得するためのクエリは、データ ソースを定義した後で作成します。 データセット クエリを作成する際は、データ ソースが参照する XML データの種類に応じて、XML **Query** または要素パスを指定する必要があります。 XML **クエリ** は、 **\<Query>** タグ内に、名前空間と XML 要素を指定したものです。指定する名前空間と XML 要素は、データ ソースによって異なります。 要素パスは、基になる XML データから取り出すノードおよびノード属性を XPath に似た構文で指定するもので、名前空間には依存しません。 要素パスの詳細については、「[Element Path Syntax for XML Report Data &#40;SSRS&#41;](../../reporting-services/report-data/element-path-syntax-for-xml-report-data-ssrs.md)」 (XML レポート データの要素パス構文 &#40;SSRS&#41;) を参照してください。  
  
 次のような種類の XML データについて、XML データ ソースを作成できます。  
  
-   HTTP プロトコルを使って URL で参照される XML ドキュメント  
  
-   XML データを返す Web サービスのエンドポイント  
  
-   埋め込み XML データ  
  
 XML **Query** または要素パスの指定方法は、XML データの種類によって異なります。  
  
 XML ドキュメントの場合、XML **Query** は省略可能です。 省略しなかった場合、必要に応じて XML **ElementPath**を指定できます。 XML **ElementPath** の値には、要素パスの構文を使用します。 XML **Query** および XML **ElementPath** を指定することにより、データ ソースから取得された XML データに対して名前空間を適切に適用できます。  
  
 接続文字列の URL によって参照される Web サービスのエンドポイントの場合、XML **Query** には、Web サービス メソッドか SOAP アクション、またはその両方を定義します。 レポート用の XML データを取得するための Web サービス要求が XML データ プロバイダーによって作成されます。  
  
> [!NOTE]  
>  Web サービスの名前空間にスラッシュ ( **/)** 文字が含まれる場合は、XML データ処理拡張機能が名前空間を正確に取得できるように、Web サービス メソッドと SOAP アクションの両方を指定します。  
  
 埋め込み XML ドキュメントの場合、XML **Query** には、使用する埋め込み XML データを定義します。名前空間と XML **ElementPath**を指定することもできます (省略可能)。  
  
## <a name="specifying-query-parameters-for-xml-data"></a>XML データに対するクエリ パラメーターの指定  
 XML ドキュメントに対するクエリ パラメーターを指定することができます。  
  
-   URL 要求の場合、クエリ パラメーターは標準の URL パラメーターとして含まれます。  
  
-   Web サービス要求の場合、クエリ パラメーターは Web サービスのメソッドに渡されます。 クエリ パラメーターを定義するには、 **[データセットのプロパティ]** ダイアログ ボックスの **[パラメーター]** ページを使用します。 
  
### <a name="example"></a>例  
 次の表は、データの取得方法の例を、レポート サーバー Web サービス、XML ドキュメント、埋め込み XML データのそれぞれについて示したものです。  
  
|XML データ ソース|クエリの例|  
|---------------------|-------------------|  
|Web サービスの XML データ ( <xref:ReportService2010.ReportingService2010.ListChildren%2A> メソッドから)|`<Query>`<br /><br /> `<Method Name="ListChildren" Namespace="https://schemas.microsoft.com/sqlserver/2005/06/30/reporting/reportingservices" />`<br /><br /> `</Query>`|  
|Web サービスの XML データ (SoapAction から)|`<Query xmlns=namespace>`<br /><br /> `<SoapAction>https://schemas/microsoft.com/sqlserver/2005/03/23/reporting/reportingservices/ListChildren</SoapAction>`<br /><br /> `</Query>`|  
|XML ドキュメントまたは埋め込み XML データ (名前空間を使用)<br /><br /> Query 要素 (要素パスに名前空間を指定)|`<Query xmlns:es="https://schemas.microsoft.com/StandardSchemas/ExtendedSales">`<br /><br /> `<ElementPath>/Customers/Customer/Orders/Order/es:LineItems/es:LineItem</ElementPath>`<br /><br /> `</Query>`|  
|埋め込み XML ドキュメント|`<Query>`<br /><br /> `<XmlData>`<br /><br /> `<Customers>`<br /><br /> `<Customer ID="1">Bobby</Customer>`<br /><br /> `</Customers>`<br /><br /> `</XmlData>`<br /><br /> `<ElementPath>Customer {@}</ElementPath>`<br /><br /> `</Query>`|  
|XML ドキュメント (既定)|*クエリなし*。<br /><br /> 要素パスは XML ドキュメントそのものから取得され、名前空間には依存しません。|  
  
> [!NOTE]  
>  最初に挙げた Web サービスの例では、 <xref:ReportService2006.ReportingService2006.ListChildren%2A> メソッドから) このクエリを実行するには、新しいデータ ソースを作成し、接続文字列を `https://localhost/reportserver/reportservice2006.asmx` に設定する必要があります。 <xref:ReportService2006.ReportingService2006.ListChildren%2A> メソッドは、**Item** と **Recursive** の 2 つのパラメーターを受け取ります。 **Item** の既定値は **/** に、 **Recursive** の既定値は **1**に設定されます。  
  
## <a name="specifying-namespaces"></a>名前空間の指定  
 データ ソースから取得された XML データに使用する名前空間を指定するには、XML **Query** 要素を使用します。 次の XML クエリには、名前空間 **sales**が使用されています。 **および** の XML `sales:LineItems` ElementPath `sales:LineItem` ノードには、名前空間 **sales**が使用されています。  
  
```  
<Query xmlns:sales=  
"https://schemas.microsoft.com/StandardSchemas/ExtendedSales">  
   <SoapAction>  
      https://schemas.microsoft.com/SalesWebService/ListOrders   
   </SoapAction>  
   <ElementPath>  
      Customers/Customer/Orders/Order/sales:LineItems/sales:LineItem  
   </ElementPath>  
</Query>  
```  
  
 データ プロバイダーの名前空間を指定して、既定の名前空間を空のままにするには、 **xmldp**を使用します。 次の例を参照してください。  
  
### <a name="example"></a>例  
 次の例では、DPNamespace.xml (後述) という XML ドキュメントが使用されています。 この表では、名前空間プレフィックスを使用した XML ElementPath 構文として、2 つの例を紹介します。  
  
|XML Query 要素|データセットとして取得されるフィールド|  
|-----------------------|-------------------------------------|  
|\<Query/>|Value A: `https://schemas.microsoft.com/...`<br /><br /> Value B: `https://schemas.microsoft.com/...`<br /><br /> Value C: `https://schemas.microsoft.com/...`|  
|`<xmldp:Query xmlns:xmldp="https://schemas.microsoft.com/sqlserver/2005/02/reporting/XmlDPQuery" xmlns:ns="https://schemas.microsoft.com/...">`<br /><br /> `<xmldp:ElementPath>Root {}/ns:Element2/Node</xmldp:ElementPath>`<br /><br /> `</xmldp:Query>`|Value D<br /><br /> Value E<br /><br /> Value F|  
  
#### <a name="xml-document-dpnamespacexml"></a>XML document: DPNamespace.xml  
 この XML をコピーして、レポート デザイナーからアクセスできる URL (https://localhost/DPNamespace.xml など) に保存すると、XML データ ソースとして使用できます。  
  
```  
<Root xmlns:ns="https://schemas.microsoft.com/...">  
   <ns:Element1>  
      <Node>Value A</Node>  
      <Node>Value B</Node>  
      <Node>Value C</Node>  
   </ns:Element1>  
   <ns:Element2>  
      <Node>Value D</Node>  
      <Node>Value E</Node>  
      <Node>Value F</Node>  
   </ns:Element2>  
</Root>  
```  
  
## <a name="see-also"></a>参照  
 [XML の接続の種類 &#40;SSRS&#41;](../../reporting-services/report-data/xml-connection-type-ssrs.md)   
 [Reporting Services チュートリアル &#40;SSRS&#41;](../../reporting-services/reporting-services-tutorials-ssrs.md)  
  
  
