---
title: XSD スキーマ (SQLXML 4.0) の注釈の使用 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, about annotated XSD schemas
- annotations [SQLXML]
- relationships [SQLXML]
- relationships [SQLXML], hierarchical relationships
- hierarchical relationships [SQLXML]
- mapping schema [SQLXML], scenarios for using
ms.assetid: 78f318a4-7a36-473b-9852-a4bae6940ce5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7c62357496d0b143fcd8736bc61117d43c6a0fac
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66013597"
---
# <a name="using-annotations-in-xsd-schemas-sqlxml-40"></a>XSD スキーマでの注釈の使用 (SQLXML 4.0)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQLXML 4.0 では、XML-Data Reduced (XDR) スキーマ言語で導入された注釈と同様に、XSD スキーマ言語で注釈がサポートされます。 XSD では、XDR でサポートされない追加の注釈も導入されています。  
  
 XSD スキーマでこれらの注釈を使用して、XML とリレーショナルのマッピングを指定できます。 これには、XSD スキーマ内の要素および属性から、データベース内のテーブル (ビュー) および列へのマッピングが含まれます。  
  
 注釈を指定しない場合は、既定のマッピングが行われます。 既定では、複合型の XSD 要素は指定したデータベースのテーブルまたはビュー名にマップされ、単純型の要素または属性は、要素または属性と同じ名前の列にマップされます。  
  
 これらの注釈は、リレーショナル データの XML ビューだけである XSD スキーマで XML のため、データベース内のリレーションシップを表す階層リレーションシップを指定することもできます。  
  
 ここでは、XSD スキーマで使用できる注釈について説明し、それらの使用例を示します。  
  
> [!NOTE]  
>  すべての例では、それぞれの注釈付き XSD スキーマに対して、単純な XPath クエリを指定します。 前提条件として、XPath 言語について理解していることが必要です。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [XSD 注釈&#40;SQLXML 4.0&#41;](xsd-annotations-sqlxml-4-0.md)  
 XSD スキーマで使用できる注釈と、その説明、および同等の XDR 注釈を一覧で示します。  
  
 [XSD 要素および属性からテーブルと列の既定のマッピング&#40;SQLXML 4.0&#41;](default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)  
 既定のマッピングについて説明し、既定のマッピングに関連するタスクの例を示します。  
  
 [XSD 要素および属性からテーブルと列の明示的なマッピング&#40;SQLXML 4.0&#41;](explicit-mapping-xsd-elements-and-attributes-to-tables-and-columns.md)  
 `sql:relation` 注釈と `sql:field` 注釈の明示的なマッピングについて説明し、例を示します。  
  
 [使用したリレーションシップ sql:relationship を指定する&#40;SQLXML 4.0&#41;](specifying-relationships-using-sql-relationship-sqlxml-4-0.md)  
 `sql:relationship` 注釈について説明し、例を示します。  
  
 [Sql:relationship での sql:inverse 属性指定&#40;SQLXML 4.0&#41;](specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)  
 `sql:inverse` 注釈について説明します。  
  
 [定数要素を使用した作成します定数&#40;SQLXML 4.0。&#41;](creating-constant-elements-using-sql-is-constant-sqlxml-4-0.md)  
 `sql:is-constant` 注釈について説明し、例を示します。  
  
 [結果として得られる XML ドキュメントを使用して sql のスキーマ要素の除外: マップ&#40;SQLXML 4.0&#41;](excluding-schema-elements-from-the-xml-document-using-sql-mapped.md)  
 `sql:mapped` 注釈について説明し、例を示します。  
  
 [Sql:limit の値を使用してフィルター処理、およびフィールドの値&#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-limit-field-and-sql-limit-value.md)  
 `sql:limit-field` 注釈と `sql:limit-value` 注釈について説明し、例を示します。  
  
 [キー列を使用して sql:key を識別する-フィールド&#40;SQLXML 4.0&#41;](identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md)  
 `sql:key-fields` 注釈について説明し、例を示します。  
  
 [Target Namespace を使用して、targetNamespace 属性を指定する&#40;SQLXML 4.0&#41;](specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-4-0.md)  
 について説明しの例を示します、 **targetNamespace**属性。  
  
 [Sql:prefix 有効な ID、IDREF、IDREFS 型属性を使用した&#40;SQLXML 4.0&#41;](creating-valid-id-idref-and-idrefs-type-attributes-using-sql-prefix-sqlxml-4-0.md)  
 `sql:prefix` 注釈について説明し、例を示します。  
  
 [データ型の強制型変換と sql:datatype 注釈&#40;SQLXML 4.0&#41;](data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md)  
 `sql:datatype` 注釈について説明し、例を示します。  
  
 [XSD データ型を XPath データ型にマッピング&#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/xpath-data-types-sqlxml-4-0.md)  
 XSD、XDR、および XPath のデータ型の対照表と、関連する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 変換の一覧を示します。  
  
 [使用した CDATA セクション sql:use を作成する-cdata &#40;SQLXML 4.0&#41;](creating-cdata-sections-using-sql-use-cdata-sqlxml-4-0.md)  
 `sql:use-data` 注釈について説明し、例を示します。  
  
 [使用した BLOB データへの URL 参照の要求: エンコード&#40;SQLXML 4.0&#41;](requesting-url-references-to-blob-data-using-sql-encode-sqlxml-4-0.md)  
 `sql:encode` 注釈について説明し、例を示します。  
  
 [未使用データを使用して、sql:overflow を取得する-フィールド&#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-overflow-field.md)  
 `sql:overflow-field` 注釈について説明し、例を示します。  
  
 [sql:hide を使用した要素と属性の非表示](hiding-elements-and-attributes-by-using-sql-hide.md)  
 `sql:hide` 注釈について説明し、例を示します。  
  
 [sql:identity 注釈と sql:guid 注釈の使用](using-the-sql-identity-and-sql-guid-annotations.md)  
 `sql:identity` 注釈と `sql:guid` 注釈について説明し、例を示します。  
  
 [sql:max-depth を使用した再帰リレーションシップの深さの指定](specifying-depth-in-recursive-relationships-by-using-sql-max-depth.md)  
 `sql:max-depth` 注釈について説明し、例を示します。  
  
## <a name="see-also"></a>参照  
 [スキーマのセキュリティに関する考慮事項を注釈が付けられた&#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/security/annotated-schema-security-considerations-sqlxml-4-0.md)  
  
  
