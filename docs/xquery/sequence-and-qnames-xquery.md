---
title: シーケンスと Qname (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- sequence [XQuery]
- XQuery, sequence
- QName [XQuery]
- predefined namespaces [XML in SQL Server]
ms.assetid: 3593ac26-dd78-4bf0-bb87-64fbcac5f026
author: rothja
ms.author: jroth
ms.openlocfilehash: fbb20c9e14c4e76b8862a23e8d758fcbba94da7f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946345"
---
# <a name="sequence-and-qnames-xquery"></a>シーケンスと QName (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  このトピックでは、XQuery の次の基本的な概念について説明します。  
  
-   Sequence  
  
-   QName と事前に定義された名前空間  
  
## <a name="sequence"></a>Sequence  
 XQuery では、式の結果は XML ノードおよび XSD アトミック型のインスタンスの一覧から構成されるシーケンスです。 シーケンス内の個々 のエントリは、"アイテム"と呼ばれます。 シーケンス内のアイテムは、次のいずれかになります。  
  
-   要素、属性、テキスト、処理命令、コメント、またはドキュメントなどのノード  
  
-   XSD 単純型のインスタンスなどのアトミック値  
  
 たとえば、次のクエリでは、2 つの要素ノードのアイテムのシーケンスが作成されます。  
  
```  
SELECT Instructions.query('  
     <step1> Step 1 description goes here</step1>,  
     <step2> Step 2 description goes here </step2>  
') AS Result  
FROM Production.ProductModel  
WHERE ProductModelID=7;  
  
```  
  
 結果を次に示します。  
  
```  
<step1> Step 1 description goes here </step1>  
<step2> Step 2 description goes here </step2>   
```  
  
 上記のクエリでは、コンマ (`,`) の最後に、`<step1>`構築はシーケンス コンス トラクターであり、必要です。 結果に空白文字は、例示のみを目的が追加され、このドキュメントでのすべての例を結果に含められます。  
  
 シーケンスについて知っておくべきその他の情報を次に示します。  
  
-   クエリの結果が他のシーケンスを含むシーケンスになる場合、含まれているシーケンスは外側のシーケンスにフラット化されます。 たとえば、シーケンス ((1,2, (3,4,5)),6) はデータ モデル内で (1, 2, 3, 4, 5, 6) にフラット化されます。  
  
    ```  
    DECLARE @x xml;  
    SET @x = '';  
    SELECT @x.query('(1,2, (3,4,5)),6');  
    ```  
  
-   空のシーケンスとは、アイテムが含まれていないシーケンスです。 これは、「()」として表されます。  
  
-   アトミック値として、またはその逆は、1 つの項目のシーケンスを扱うことができます。 つまり、(1) = 1。  
  
 この実装で、シーケンスは同種にある必要があります。 つまり、いずれかがあるアトミック値のシーケンスまたはノードのシーケンス。 たとえば、有効なシーケンスは、次のように。  
  
```  
DECLARE @x xml;  
SET @x = '';  
-- Expression returns a sequence of 1 text node (singleton).  
SELECT @x.query('1');  
-- Expression returns a sequence of 2 text nodes  
SELECT @x.query('"abc", "xyz"');  
-- Expression returns a sequence of one atomic value. data() returns  
-- typed value of the node.  
SELECT @x.query('data(1)');  
-- Expression returns a sequence of one element node.   
-- In the expression XML construction is used to construct an element.  
SELECT @x.query('<x> {1+2} </x>');  
```  
  
 次のクエリは、異種シーケンスはサポートされていないため、エラーを返します。  
  
```  
SELECT @x.query('<x>11</x>, 22');  
```  
  
## <a name="qname"></a>QName  
 XQuery の識別子は QName です。 QName は、名前空間プレフィックスとローカル名で構成されます。 この実装で XQuery の変数名は Qname とプレフィックスを含めることはできません。  
  
 クエリが指定されている次の例を検討してください、型指定されていないに対して**xml**変数。  
  
```  
DECLARE @x xml;  
SET @x = '<Root><a>111</a></Root>';  
SELECT @x.query('/Root/a');  
```  
  
 式 (`/Root/a`) では、`Root` と `a` が QName です。  
  
 次の例では、クエリを指定する、型指定されたに対して**xml**列。 クエリは、すべてを反復処理\<手順 > 最初のワーク センターからの場所にある要素。  
  
```  
SELECT Instructions.query('  
   declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $Step in /AWMI:root/AWMI:Location[1]/AWMI:step  
      return  
           string($Step)   
') AS Result  
FROM Production.ProductModel  
WHERE ProductModelID=7;  
```  
  
 クエリ式で、次のことを確認してください。  
  
-   `AWMI root`、`AWMI:Location`、`AWMI:step`、`$Step` は、すべて QName です。 `AWMI` プレフィックスであり、 `root`、 `Location`、および`Step`はすべてのローカル名。  
  
-   `$step`変数は QName であり、プレフィックスはありません。  
  
 XQuery サポートで使用するための次の名前空間が定義済み[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]します。  
  
|Prefix|URI|  
|------------|---------|  
|xs|http://www.w3.org/2001/XMLSchema|  
|xsi|http://www.w3.org/2001/XMLSchema-instance|  
|xdt|http://www.w3.org/2004/07/xpath-datatypes|  
|fn|http://www.w3.org/2004/07/xpath-functions|  
|(プレフィックスなし)|`urn:schemas-microsoft-com:xml-sql`|  
|sqltypes|https://schemas.microsoft.com/sqlserver/2004/sqltypes|  
|xml|`http://www.w3.org/XML/1998/namespace`|  
|(プレフィックスなし)|`https://schemas.microsoft.com/sqlserver/2004/SOAP`|  
  
 各データベースを作成するには、 **sys** XML スキーマ コレクションです。 各データベースにはこれらのスキーマが保持されるため、ユーザーが作成した XML スキーマ コレクションからアクセスすることができます。  
  
> [!NOTE]  
>  この実装がサポートしていません、`local`の XQuery 仕様に記載されているプレフィックス http://www.w3.org/2004/07/xquery-local-functions します。  
  
## <a name="see-also"></a>参照  
 [XQuery の基礎](../xquery/xquery-basics.md)  
  
  
