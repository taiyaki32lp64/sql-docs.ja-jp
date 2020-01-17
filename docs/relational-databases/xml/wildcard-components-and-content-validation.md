---
title: ワイルドカード コンポーネントと内容検証 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- wildcard components [XML]
- content validation [XML]
ms.assetid: ffa7d974-3645-446c-8425-f0b22b6b060a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ba4e15016ca7b6ae3094b575ee87a1c7508b8aac
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096951"
---
# <a name="wildcard-components-and-content-validation"></a>ワイルドカード コンポーネントと内容検証
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  ワイルドカード コンポーネントは、コンテンツ モデルで使用できる表現の柔軟性を高めるために使用されます。 ワイルドカード コンポーネントは、次のように XSD 言語でサポートされています。  
  
-   要素ワイルドカード コンポーネント。 これらは **\<xsd:any>** 要素で表現されます。  
  
-   属性ワイルドカード コンポーネント。 これらは **\<xsd:anyAttribute>** 要素で表現されます。  
  
 両方のワイルドカード文字要素 ( **\<xsd:any>** および **\<xsd:anyAttribute>** ) で **processContents** 属性を使用できます。 この属性を使用して、ワイルドカード文字要素で関連付けられるドキュメントの内容の違反を、XML アプリケーションで検証する方法を示す値を指定できます。 検証方法を示す値には、次のようにそれぞれ異なる効果があります。  
  
-   **strict** 値は、内容を完全に検証することを指定します。  
  
-   **skip** 値は、内容を検証しないことを指定します。  
  
-   **lax** 値は、スキーマ定義が有効な要素と属性だけを検証することを指定します。  
  
## <a name="lax-validation-and-xsanytype-elements"></a>lax 検証と xs:anyType 要素  
 XML スキーマの仕様では、 **anyType** 型の要素には **lax** 検証が使用されています。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] では lax 検証をサポートしていなかったので、 **anyType**型の要素にも strict 検証が適用されていました。 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]からは lax 検証がサポートされるようになったため、 **anyType** 型の要素の内容は lax 検証を使用して検証されます。  
  
 次の例は、lax 検証を示しています。 スキーマ要素 `e` は **anyType** 型です。 この例では、型指定された **xml** 変数を作成し、 **anyType** 型の要素の lax 検証を示します。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema"   
        targetNamespace="http://ns">  
   <element name="e" type="anyType"/>  
   <element name="a" type="byte"/>  
   <element name="b" type="string"/>  
 </schema>'  
GO  
```  
  
 `<e>` の検証が成功するので、次の例は成功します。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<e xmlns="http://ns"><a>1</a><b>data</b></e>'  
GO  
```  
  
 次の例は成功します。 要素 `<c>` はスキーマで定義されていませんが、インスタンスは受け入れられます。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<e xmlns="http://ns"><a>1</a><c>Wrong</c><b>data</b></e>'  
GO  
```  
  
 次の例の XML インスタンスは拒否されます。これは、 `<a>` 要素の定義で文字列値が許可されていないためです。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<e xmlns="http://ns"><a>Wrong</a><b>data</b></e>'  
SELECT @var  
GO  
```  
  
## <a name="see-also"></a>参照  
 [サーバー上の XML スキーマ コレクションの要件と制限](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
