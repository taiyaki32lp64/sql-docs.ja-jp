---
title: FOR XML 句の基本構文 | Microsoft Docs
ms.custom: fresh2019may
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- BINARY BASE64 directive
- ROOT directive
- FOR XML clause, BINARY BASE64 directive
- FOR XML clause, syntax
- FOR XML clause, ROOT directive
ms.assetid: df19ecbf-d28e-4e9c-aaa3-700f8bbd3be4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3ed13483746d2a3592f8c37380862719103d438a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029372"
---
# <a name="basic-syntax-of-the-for-xml-clause"></a>FOR XML 句の基本構文

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

FOR XML モードには、RAW、AUTO、EXPLICIT、または PATH を使用できます。 このモードにより、結果の XML の構造が決まります。  
  
> [!IMPORTANT]  
> FOR XML オプションに対する **XMLDATA** ディレクティブは、**非推奨**です。 RAW モードと AUTO モードの場合は、XSD 世代を使用してください。 EXPLICIT モードでは、XMLDATA ディレクティブに代わる機能はありません。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]

## <a name="syntax"></a>構文

「[FOR 句 (Transact-SQL)](../../t-sql/queries/select-for-clause-transact-sql.md)」で説明されている基本構文を次に示します。

```  
[ FOR { BROWSE | <XML> } ]  
<XML> ::=  
XML   
    {   
      { RAW [ ('ElementName') ] | AUTO }   
        [   
           <CommonDirectives>   
           [ , { XMLDATA | XMLSCHEMA [ ('TargetNameSpaceURI') ]} ]
           [ , ELEMENTS [ XSINIL | ABSENT ]   
        ]  
      | EXPLICIT   
        [   
           <CommonDirectives>   
           [ , XMLDATA ]   
        ]  
      | PATH [ ('ElementName') ]   
        [   
           <CommonDirectives>   
           [ , ELEMENTS [ XSINIL | ABSENT ] ]  
        ]  
     }   
  
 <CommonDirectives> ::=   
   [ , BINARY BASE64 ]  
   [ , TYPE ]  
   [ , ROOT [ ('RootName') ] ]  
```  

### <a name="syntax-for-azure-sql-database"></a>Azure SQL Database の構文

Azure SQL Database にも適用される SELECT...**FOR XML** 句のドキュメントについては、「[FOR XML (SQL Server)](../../relational-databases/xml/for-xml-sql-server.md)」をご覧ください。

## <a name="arguments"></a>引数

**RAW** [('_ElementName_')]  
 クエリの結果を取得し、結果セット内の各行を、要素タグとして汎用識別子 \<row /> を持つ XML 要素に変換します。 このディレクティブを使用するときは、必要に応じて、行要素の名前を指定できます。 結果の XML では、指定した *ElementName* が、行ごとに生成される行要素として使用されます。 詳細については、「 [FOR XML での RAW モードの使用](../../relational-databases/xml/use-raw-mode-with-for-xml.md)」を参照してください。  
  
**AUTO**  
 クエリの結果を単純な入れ子の XML ツリーで返します。 1 つ以上の列が SELECT 句にリストされている FROM 句の各テーブルは、XML 要素として表されます。 SELECT 句に一覧されている列は、該当する要素属性にマップされます。 詳細については、「 [FOR XML での AUTO モードの使用](../../relational-databases/xml/use-auto-mode-with-for-xml.md)」を参照してください。  
  
**EXPLICIT**  
 結果として得られる XML ツリーの形状を明示的に定義することを指定します。 このモードを使用する場合は、クエリを特殊な方法で記述することにより、目的の入れ子構造に関して追加情報を明示的に指定する必要があります。 詳細については、「 [FOR XML での EXPLICIT モードの使用](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)」を参照してください。  
  
**PATH**  
 PATH モードを使用すると、要素と属性を組み合わせた使用が容易になり、入れ子構造を使用することで、複雑なプロパティも容易に表現できるようになります。 FOR XML EXPLICIT モードのクエリを使用してこのような XML を行セットから作成することもできますが、煩雑になりかねない EXPLICIT モードのクエリに比べて PATH モードでは同じことを簡潔に行うことができます。 PATH モードに、入れ子の FOR XML クエリと、 **xml** 型のインスタンスを返す TYPE ディレクティブを組み合わせることで、簡潔なクエリを記述できます。 この方法により、EXPLICIT モードのクエリの大半を書き直すことができます。 既定で、PATH モードは結果セットの行ごとに \<row> 要素ラッパーを生成します。 要素名は、必要に応じて指定できます。 要素名を指定すると、指定した名前が囲み要素名として使用されます。 空の文字列 (FOR XML PATH ('')) を指定すると、囲み要素は生成されません。 詳細については、「 [FOR XML での PATH モードの使用](../../relational-databases/xml/use-path-mode-with-for-xml.md)」を参照してください。  
  
**MLDATA**  
 インライン XDR (XML-Data Reduced) スキーマが返されることを指定します。 このスキーマは、ドキュメントの前にインライン スキーマとして付加されます。 作業用サンプルについては、「 [FOR XML での RAW モードの使用](../../relational-databases/xml/use-raw-mode-with-for-xml.md)」を参照してください。  
  
**XMLSCHEMA**  
 インライン W3C XML スキーマ (XSD) を返します。 このディレクティブを指定する場合は、必要に応じて対象名前空間 URI を指定できます。 これにより、スキーマで指定した名前空間が返されます。 詳細については、「 [Generate an Inline XSD Schema](../../relational-databases/xml/generate-an-inline-xsd-schema.md)」を参照してください。 作業用サンプルについては、「 [FOR XML での RAW モードの使用](../../relational-databases/xml/use-raw-mode-with-for-xml.md)」を参照してください。  
  
**ELEMENTS**  
 ELEMENTS オプションを指定すると、列が副要素として返されます。 指定していない場合は、XML 属性にマップされます。 このオプションは、RAW、AUTO、および PATH の各モードでのみサポートされます。 このディレクティブを使用する場合は、必要に応じて XSINIL または ABSENT を指定できます。 XSINIL は、NULL 列の値に対して、 **xsi:nil** 属性が True に設定された要素を作成することを指定します。 既定の状態や、ABSENT が ELEMENTS と共に指定されている場合は、NULL 値に対して要素は作成されません。 作業用サンプルについては、「 [FOR XML での RAW モードの使用](../../relational-databases/xml/use-raw-mode-with-for-xml.md) 」 および 「 [FOR XML での AUTO モードの使用](../../relational-databases/xml/use-auto-mode-with-for-xml.md)」を参照してください。  
  
**BINARY BASE64**  
 BINARY Base64 オプションを指定した場合、クエリの返すバイナリ データは Base64 エンコード形式で表されます。 RAW モードおよび EXPLICIT モードでバイナリ データを取得する場合は、このオプションを指定する必要があります。 AUTO モードでは、特に指定しない限りバイナリ データが参照として返されます。 作業用サンプルについては、「 [FOR XML での RAW モードの使用](../../relational-databases/xml/use-raw-mode-with-for-xml.md)」を参照してください。  
  
**TYPE**  
 クエリが結果を **xml** 型で返すことを指定します。 詳細については、「 [FOR XML クエリの TYPE ディレクティブ](../../relational-databases/xml/type-directive-in-for-xml-queries.md)」を参照してください。  
  
**ROOT** [('_RootName_')]  
 結果の XML に、1 つの最上位要素が追加されることを指定します。 必要に応じて、生成するルート要素名を指定することもできます。 既定値は `<root>` です。  
  
## <a name="see-also"></a>参照  
 [FOR XML での RAW モードの使用](../../relational-databases/xml/use-raw-mode-with-for-xml.md)   
 [FOR XML での AUTO モードの使用](../../relational-databases/xml/use-auto-mode-with-for-xml.md)   
 [FOR XML での EXPLICIT モードの使用](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)   
 [FOR XML での PATH モードの使用](../../relational-databases/xml/use-path-mode-with-for-xml.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)  
