---
title: クエリ式と Uniform Resource Name | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
helpviewer_keywords:
- query expressions
- unique resource names
- URN
ms.assetid: e0d30dbe-7daf-47eb-8412-1b96792b6fb9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4fec86c0f732a4f47d3132be51226b877c428d5f
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72782760"
---
# <a name="query-expressions-and-uniform-resource-names"></a>クエリ式と Uniform Resource Name
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 管理オブジェクト (SMO) モデルおよび [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell スナップインでは、XPath 式に似た、2 種類の式文字列が使用されます。 クエリ式は、オブジェクト モデル階層内の 1 つまたは複数のオブジェクトを列挙するための条件のセットを指定する文字列です。 URN (Uniform Resource Name) は、単一のオブジェクトを一意に識別する特定の種類のクエリ式文字列です。  
  
## <a name="syntax"></a>構文  
  
```
      Object1  
      [<FilterExpression1>]/ ... /ObjectN[<FilterExpressionN>]<FilterExpression>::=  
<PropertyExpression> [and <PropertyExpression>][...n]  
  
<PropertyExpression>::=@BooleanPropertyName=true()  
 | @BooleanPropertyName=false()  
 | contains(@StringPropertyName, 'PatternString')  
  | @StringPropertyName='String'  
 | @DatePropertyName=datetime('DateString')  
 | is_null(@PropertyName)  
 | not(<PropertyExpression>)  
```  
  
## <a name="arguments"></a>引数  
 *オブジェクト*  
 オブジェクトの種類を指定します。オブジェクトの種類は、式文字列のこのノードで表されます。 各オブジェクトは、これらの SMO オブジェクト モデルの名前空間からのコレクション クラスを表します。  
  
 <xref:Microsoft.SqlServer.Management.Smo>  
  
 <xref:Microsoft.SqlServer.Management.Smo.Agent>  
  
 <xref:Microsoft.SqlServer.Management.Smo.Broker>  
  
 <xref:Microsoft.SqlServer.Management.Smo.Mail>  
  
 <xref:Microsoft.SqlServer.Management.Dmf>  
  
 <xref:Microsoft.SqlServer.Management.Facets>  
  
 <xref:Microsoft.SqlServer.Management.RegisteredServers>  
  
 <xref:Microsoft.SqlServer.Management.Smo.RegSvrEnum>  
  
 たとえば、サーバーでは **ServerCollection** クラスを、データベースでは **DatabaseCollection** クラスを指定します。  
  
 \@*PropertyName*  
 *Object*に指定したオブジェクトと関連付けるクラスのいずれかのプロパティの名前を指定します。 プロパティの名前の前に \@ 文字を付ける必要があります。 たとえば、\@Database**クラスのプロパティ**IsAnsiNull**には、** IsAnsiNull と指定します。  
  
 \@*BooleanPropertyName*=true()  
 指定したブール型のプロパティが TRUE に設定されているすべてのオブジェクトを列挙します。  
  
 \@*BooleanPropertyName*=false()  
 指定したブール型のプロパティが FALSE に設定されているすべてのオブジェクトを列挙します。  
  
 contains(\@*StringPropertyName*, '*PatternString*')  
 指定した文字列プロパティに '*PatternString*' に指定した文字のセットが 1 つ以上含まれるすべてのオブジェクトを列挙します。  
  
 \@*StringPropertyName*='*PatternString*'  
 指定した文字列プロパティの値が '*PatternString*' に指定した文字パターンとまったく同じであるすべてのオブジェクトを列挙します。  
  
 \@*DatePropertyName*= datetime('*DateString*')  
 指定した日付プロパティの値が '*DateString*' に指定した日付と一致するすべてのオブジェクトを列挙します。 *DateString* は、yyyy-mm-dd hh:mi:ss.mmm 形式で指定する必要があります。  
  
|||  
|-|-|  
|yyyy|年を表す 4 桁の数字。|  
|mm|月を表す 2 桁の数字 (01 ～ 12)。|  
|dd|日を表す 2 桁の数字 (01 ～ 31)。|  
|mm|時を 24 時間形式で表す 2 桁の数字 (01 ～ 23)。|  
|mi|分を表す 2 桁の数字 (01 ～ 59)。|  
|ss|秒を表す 2 桁の数字 (01 ～ 59)。|  
|mmm|ミリ秒数 (001 ～ 999)。|  
  
 この形式で指定された日付は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]に格納されているすべての日付形式に対して評価できます。  
  
 is_null(\@*PropertyName*)  
 指定したプロパティの値が NULL であるすべてのオブジェクトを列挙します。  
  
 not(\<*PropertyExpression*>)  
 *PropertyExpression*の評価値を否定して、 *PropertyExpression*に指定した条件に一致しないすべてのオブジェクトを列挙します。 たとえば、not(contains(\@Name, 'xyz')) と指定した場合、名前に xyz という文字列が含まれないすべてのオブジェクトが列挙されます。  
  
## <a name="remarks"></a>Remarks  
 クエリ式は、SMO モデル階層のノードを列挙する文字列です。 各ノードには、そのノードのどのオブジェクトを列挙するかを決定する条件を指定するためのフィルター式があります。 クエリ式は、XPath 式言語をモデル化したものです。 クエリ式は、XPath でサポートされる式の小さなサブセットを実装し、XPath には用意されていないいくつかの拡張を含みます。 XPath 式は、XML ドキュメント内の 1 つまたは複数のタグを列挙するための条件のセットを指定する文字列です。 XPath の詳細については、 [W3C XPath 言語の Web サイト](http://www.w3.org/TR/xpath20/)を参照してください。  
  
 クエリ式は、Server オブジェクトへの絶対参照で開始する必要があります。 / で始まる相対的な式は使用できません。 クエリ式に指定するオブジェクトの順序は、関連付けられたオブジェクト モデルのコレクション オブジェクトの階層に従っている必要があります。 たとえば、Microsoft.SqlServer.Management.Smo 名前空間のオブジェクトを参照するクエリ式は、Server ノードで開始し、続けて Database ノードを指定する必要があります。  
  
 オブジェクトに対して *\<FilterExpression>* を指定しなかった場合、そのノードのすべてのオブジェクトが列挙されます。  
  
## <a name="uniform-resource-names-urn"></a>URN (Uniform Resource Name)  
 URN は、クエリ式のサブセットです。 それぞれの URN は、1 つのオブジェクトへの完全修飾参照を示します。 一般的な URN では、Name プロパティを使用して、各ノードの単独のオブジェクトを識別します。 たとえば、次の URN は特定の列を参照します。  
  
```  
Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012']/Table[@Name='SalesPerson' and @Schema='Sales']/Column[@Name='SalesPersonID']  
```  
  
## <a name="examples"></a>使用例  
  
### <a name="a-enumerating-objects-using-false"></a>A. false() を使用したオブジェクトの列挙  
 このクエリ式は、 **MyComputer** 上の既定のインスタンスにおいて **AutoClose**属性が false に設定されているすべてのデータベースを列挙します。  
  
```  
Server[@Name='MYCOMPUTER']/Database[@AutoClose=false()]  
```  
  
### <a name="b-enumerating-objects-using-contains"></a>b. contains を使用したオブジェクトの列挙  
 このクエリ式は、大文字と小文字が区別されない、名前に m という文字を含むすべてのデータベースを列挙します。  
  
```  
Server[@Name='MYCOMPUTER']/Database[@CaseSensitive=false() and contains(@Name, 'm')]   
```  
  
### <a name="c-enumerating-objects-using-not"></a>C. not を使用したオブジェクトの列挙  
 このクエリ式は、 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] Production **スキーマに含まれていない、テーブル名に History という単語を含むすべての** テーブルを列挙します。  
  
```  
Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012']/Table[not(@Schema='Production') and contains(@Name, 'History')]  
```  
  
### <a name="d-not-supplying-a-filter-expression-for-the-final-node"></a>D. 最後のノードのフィルター式を省略した例  
 このクエリ式は、 **AdventureWorks2012.Sales.SalesPerson** テーブル内のすべての列を列挙します。  
  
```  
Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012"]/Table[@Schema='Sales' and @Name='SalesPerson']/Columns  
```  
  
### <a name="e-enumerating-objects-using-datetime"></a>E. datetime を使用したオブジェクトの列挙  
 このクエリ式は、特定の時刻に [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] データベースに作成されたすべてのテーブルを列挙します。  
  
```  
Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012"]/Table[@CreateDate=datetime('2008-03-21 19:49:32.647')]  
```  
  
### <a name="f-enumerating-objects-using-is_null"></a>F. is_null を使用したオブジェクトの列挙  
 このクエリ式は、最終更新日プロパティの値が NULL ではない [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] データベース内のすべてのテーブルを列挙します。  
  
```  
Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012"]/Table[Not(is_null(@DateLastModified))]  
```  
  
## <a name="see-also"></a>参照  
 [Invoke-PolicyEvaluation コマンドレット](../database-engine/invoke-policyevaluation-cmdlet.md)   
 [SQL Server Audit &#40;データベース エンジン&#41;](../relational-databases/security/auditing/sql-server-audit-database-engine.md)  
