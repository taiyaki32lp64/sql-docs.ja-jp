---
title: FOR XML での RAW モードの使用 | Microsoft Docs
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML RAW mode
- XMLSCHEMA option
- FOR XML clause, RAW mode
- RAW FOR XML mode
- ELEMENTS directive
- RAW mode
- XMLDATA option
ms.assetid: 02c1bc0b-760c-4589-9ab1-6927c6d9c734
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
ms.openlocfilehash: 7e88a1c65d2c8cdf8ba6129c8af28492dc362aba
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75245235"
---
# <a name="use-raw-mode-with-for-xml"></a>FOR XML での RAW モードの使用

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

RAW モードでは、クエリの結果セットの各行が XML 要素に変換されます。この XML 要素は、汎用識別子 \<row> を持つか、必要に応じて要素名が付けられます。 既定では、NULL 以外の行セットの各列の値が \<row> 要素の属性にマップされます。 FOR XML 句に ELEMENTS ディレクティブが追加されると、各列の値が \<row> 要素のサブ要素にマップされます。 必要に応じて ELEMENTS ディレクティブと共に XSINIL オプションを指定して、`xsi:nil="true"` 属性を持つ要素に結果セットの NULL 列値をマップできます。
  
 結果として生成される XML のスキーマを要求できます。 XMLDATA オプションを指定すると、インライン XDR スキーマが返されます。 XMLSCHEMA オプションを指定すると、インライン XSD スキーマが返されます。 スキーマはデータの先頭に示されます。 その結果、トップレベルの要素ごとにスキーマの名前空間参照が繰り返されます。  
  
 バイナリ データを base64 エンコード形式で返すには、BINARY BASE64 オプションを FOR XML 句に指定する必要があります。 RAW モードでは、BINARY BASE64 オプションを指定しないでバイナリ データを取得すると、エラーが発生します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 このセクションには、次の例が含まれています。  
  
-   [例: XML での製品モデル情報の取得](../../relational-databases/xml/example-retrieving-product-model-information-as-xml.md)  
  
-   [例: ELEMENTS ディレクティブで XSINIL を指定する](../../relational-databases/xml/example-specifying-xsinil-with-the-elements-directive.md)  
  
-   [XMLDATA & XMLSCHEMA を使用した結果としてのスキーマの要求](../../relational-databases/xml/example-requesting-schemas-as-results-with-the-xmldata-and-xmlschema-options.md)  
  
-   [例: バイナリ データの取得](../../relational-databases/xml/example-retrieving-binary-data.md)  
  
-   [例: &#60;row&#62; 要素の名前を変更する](../../relational-databases/xml/example-renaming-the-row-element.md)  
  
-   [例: FOR XML で生成される XML のルート要素の指定](../../relational-databases/xml/example-specifying-a-root-element-for-the-xml-generated-by-for-xml.md)  
  
-   [例: XML 型の列のクエリ](../../relational-databases/xml/example-querying-xmltype-columns.md)  
  
## <a name="see-also"></a>参照  
 [WITH XMLNAMESPACES を使用したクエリへの名前空間の追加](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [FOR XML での AUTO モードの使用](../../relational-databases/xml/use-auto-mode-with-for-xml.md)   
 [FOR XML での EXPLICIT モードの使用](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)   
 [FOR XML での PATH モードの使用](../../relational-databases/xml/use-path-mode-with-for-xml.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [FOR XML (SQL Server)](../../relational-databases/xml/for-xml-sql-server.md)
  
  
