---
title: XSD スキーマでの注釈の使用 (SQLXML)
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 00cb5a095e6186ed6009f94dedaa43a81f8165d9
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75246835"
---
# <a name="using-annotations-in-xsd-schemas-sqlxml-40"></a>XSD スキーマでの注釈の使用 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQLXML 4.0 では、XML-Data Reduced (XDR) スキーマ言語で導入された注釈と同様に、XSD スキーマ言語で注釈がサポートされます。 XSD では、XDR でサポートされない追加の注釈も導入されています。  
  
 XSD スキーマでこれらの注釈を使用して、XML とリレーショナルのマッピングを指定できます。 これには、XSD スキーマ内の要素および属性から、データベース内のテーブル (ビュー) および列へのマッピングが含まれます。  
  
 注釈を指定しない場合は、既定のマッピングが行われます。 既定では、複合型の XSD 要素は指定したデータベースのテーブルまたはビュー名にマップされ、単純型の要素または属性は、要素または属性と同じ名前の列にマップされます。  
  
 これらの注釈を使用して、XML 内の階層リレーションシップを指定することもできます。これは、XSD スキーマがリレーショナルデータの XML ビューであるためです。  
  
 ここでは、XSD スキーマで使用できる注釈について説明し、それらの使用例を示します。  
  
> [!NOTE]  
>  すべての例では、それぞれの注釈付き XSD スキーマに対して、単純な XPath クエリを指定します。 前提条件として、XPath 言語について理解していることが必要です。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [&#40;SQLXML 4.0&#41;の XSD 注釈](../../relational-databases/sqlxml-annotated-xsd-schemas-using/xsd-annotations-sqlxml-4-0.md)  
 XSD スキーマで使用できる注釈と、その説明、および同等の XDR 注釈を一覧で示します。  
  
 [テーブルおよび列への XSD 要素と属性の既定のマッピング &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)  
 既定のマッピングについて説明し、既定のマッピングに関連するタスクの例を示します。  
  
 [テーブルおよび列への XSD 要素と属性の明示的なマッピング &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/explicit-mapping-xsd-elements-and-attributes-to-tables-and-columns.md)  
 **Sql: relation**注釈と**sql: field**注釈による明示的なマッピングについて説明し、例を示します。  
  
 [Sql: relationship を使用したリレーションシップの指定 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-relationships-using-sql-relationship-sqlxml-4-0.md)  
 について説明し、 **sql: relationship**注釈の例を示します。  
  
 [Sql: relationship での sql: 逆属性の指定 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)  
 **Sql: 逆**の注釈について説明します。  
  
 [Sql を使用した定数要素の作成: &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-constant-elements-using-sql-is-constant-sqlxml-4-0.md)  
 について説明し、 **sql: is constant**注釈の例を示します。  
  
 [Sql: マップト &#40;SQLXML 4.0&#41;を使用した結果の XML ドキュメントからのスキーマ要素の除外](../../relational-databases/sqlxml-annotated-xsd-schemas-using/excluding-schema-elements-from-the-xml-document-using-sql-mapped.md)  
 について説明し、 **sql: マップ**された注釈の例を示します。  
  
 [Sql: limit-field および sql: limit-value &#40;SQLXML 4.0&#41;を使用した値のフィルター処理](../../relational-databases/sqlxml-annotated-xsd-schemas-using/filtering-values-using-sql-limit-field-and-sql-limit-value-sqlxml-4-0.md)  
 について説明し、 **sql: limit-field**および**sql: limit-value**注釈の例を示します。  
  
 [Sql: キーフィールド &#40;SQLXML 4.0&#41;を使用したキー列の識別](../../relational-databases/sqlxml-annotated-xsd-schemas-using/identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md)  
 について説明し、 **sql: キーフィールド**の注釈の例を示します。  
  
 [TargetNamespace 属性を使用してターゲットの名前空間を指定する &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-4-0.md)  
 について説明し、 **targetNamespace**属性の例を示します。  
  
 [Sql: prefix &#40;SQLXML 4.0&#41;を使用した有効な ID、IDREF、IDREFS 型の属性の作成](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-valid-id-idref-and-idrefs-type-attributes-using-sql-prefix-sqlxml-4-0.md)  
 について説明し、 **sql: prefix**注釈の例を示します。  
  
 [データ型変換と sql: datatype 注釈 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md)  
 について説明し、 **sql: datatype**注釈の例を示します。  
  
 [XSD データ型から XPath データ型へのマッピング &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/mapping-xsd-data-types-to-xpath-data-types-sqlxml-4-0.md)  
 XSD、XDR、および XPath のデータ型の対照表と、関連する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 変換の一覧を示します。  
  
 [Sql を使用した CDATA セクションの作成: &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-cdata-sections-using-sql-use-cdata-sqlxml-4-0.md)  
 について説明し、 **sql: use-data**注釈の例を示します。  
  
 [Sql: encode &#40;SQLXML 4.0&#41;を使用した BLOB データへの URL 参照の要求](../../relational-databases/sqlxml-annotated-xsd-schemas-using/requesting-url-references-to-blob-data-using-sql-encode-sqlxml-4-0.md)  
 について説明し、 **sql: encode**注釈の例を示します。  
  
 [Sql: overflow フィールドを使用した未使用データの取得 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/retrieving-unconsumed-data-using-the-sql-overflow-field-sqlxml-4-0.md)  
 について説明し、 **sql: overflow フィールド**注釈の例を示します。  
  
 [sql:hide による要素と属性の非表示](../../relational-databases/sqlxml-annotated-xsd-schemas-using/hiding-elements-and-attributes-by-using-sql-hide.md)  
 について説明し、 **sql: hide**注釈の例を示します。  
  
 [sql:identity 注釈と sql:guid 注釈の使用](../../relational-databases/sqlxml-annotated-xsd-schemas-using/using-the-sql-identity-and-sql-guid-annotations.md)  
 について説明し、 **sql: identity**注釈と**sql: guid**注釈の例を示します。  
  
 [sql:max-depth を使用した、再帰リレーションシップの深さの指定](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-depth-in-recursive-relationships-by-using-sql-max-depth.md)  
 について説明し、 **sql: max depth**注釈の例を示します。  
  
## <a name="see-also"></a>参照  
 [SQLXML 4.0&#41;&#40;注釈付きスキーマのセキュリティに関する考慮事項](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/annotated-schema-security-considerations-sqlxml-4-0.md)  
  
  
