---
title: FOR XML での RAW モードの使用 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: aec0ec20c9bd46a06560f5ce6ebd374e937f0343
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63193249"
---
# <a name="use-raw-mode-with-for-xml"></a>FOR XML での RAW モードの使用
  RAW モードでは、クエリの結果セットの各行が XML 要素に変換されます。この XML 要素は、汎用識別子 \<row> を持つか、必要に応じて要素名が付けられます。 既定では、NULL 以外の行セットの各列の値が \<row> 要素の属性にマップされます。 FOR XML 句に ELEMENTS ディレクティブが追加されると、各列の値が \<row> 要素のサブ要素にマップされます。 必要に応じて ELEMENTS ディレクティブと共に XSINIL オプションを指定して、xsi:nil=`"`true`"`の属性を持つ要素に結果セットの NULL 列値をマップできます。  
  
 結果として生成される XML のスキーマを要求できます。 XMLDATA オプションを指定すると、インライン XDR スキーマが返されます。 XMLSCHEMA オプションを指定すると、インライン XSD スキーマが返されます。 スキーマはデータの先頭に示されます。 その結果、トップレベルの要素ごとにスキーマの名前空間参照が繰り返されます。  
  
 バイナリ データを base64 エンコード形式で返すには、BINARY BASE64 オプションを FOR XML 句に指定する必要があります。 RAW モードでは、BINARY BASE64 オプションを指定しないでバイナリ データを取得すると、エラーが発生します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 ここでは、次の例について説明します。  
  
-   [例: XML での製品モデル情報の取得](example-retrieving-product-model-information-as-xml.md)  
  
-   [例: ELEMENTS ディレクティブで XSINIL を指定する](example-specifying-xsinil-with-the-elements-directive.md)  
  
-   [例: XMLDATA オプションと XMLSCHEMA オプションを使用した結果としてのスキーマの要求](example-requesting-schemas-as-results-with-the-xmldata-and-xmlschema-options.md)  
  
-   [例: バイナリ データの取得](example-retrieving-binary-data.md)  
  
-   [例: &#60;row&#62; 要素の名前を変更する](example-renaming-the-row-element.md)  
  
-   [例: FOR XML で生成される XML のルート要素の指定](example-specifying-a-root-element-for-the-xml-generated-by-for-xml.md)  
  
-   [例: XML 型の列のクエリ](example-querying-xmltype-columns.md)  
  
## <a name="see-also"></a>関連項目  
 [WITH XMLNAMESPACES を使用したクエリへの名前空間の追加](add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [FOR XML での AUTO モードの使用](use-auto-mode-with-for-xml.md)   
 [FOR XML での EXPLICIT モードの使用](use-explicit-mode-with-for-xml.md)   
 [FOR XML での PATH モードの使用](use-path-mode-with-for-xml.md)   
 [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)   
 [FOR XML &#40;SQL Server&#41;](../xml/for-xml-sql-server.md)  
  
  
