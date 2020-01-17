---
title: XSD 注釈 (SQLXML)
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, annotations listed
- XSD schemas [SQLXML], annotations
ms.assetid: c62a6785-8d66-40a2-9c5d-80c73d600a3b
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: acd1dc15531f2e4830993eed1404db4d7205feef
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75246796"
---
# <a name="xsd-annotations-sqlxml-40"></a>XSD 注釈 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  次の表では、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] で導入された XSD 注釈の一覧を示し、これらを [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] で導入された XDR 注釈と比較します。  
  
|XSD 注釈|説明|トピックリンク|XDR 注釈|  
|--------------------|-----------------|----------------|--------------------|  
|**sql:encode**|XML 要素または属性を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] BLOB 列にマップするときに、参照 URI を要求します。 この URI は、後で BLOB データを返すために使用できます。|[Sql: encode &#40;SQLXML 4.0&#41;を使用した BLOB データへの URL 参照の要求](../../relational-databases/sqlxml-annotated-xsd-schemas-using/requesting-url-references-to-blob-data-using-sql-encode-sqlxml-4-0.md)|**url エンコード**|  
|**sql: guid**|列に対し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により生成される GUID 値を使用するか、アップデートグラムで提供される値を使用するかを指定します。|[sql:identity 注釈と sql:guid 注釈の使用](../../relational-databases/sqlxml-annotated-xsd-schemas-using/using-the-sql-identity-and-sql-guid-annotations.md)|サポートされていません|  
|**sql:hide**|スキーマで指定されている要素または属性を、結果の XML ドキュメントで表示しないようにします。|[sql:hide による要素と属性の非表示](../../relational-databases/sqlxml-annotated-xsd-schemas-using/hiding-elements-and-attributes-by-using-sql-hide.md)|サポートされていません|  
|**sql:identity**|IDENTITY 型のデータベース列にマップされる任意のノードに指定できます。 この注釈に指定した値によって、データベース内の対応する IDENTITY 型列の更新方法が決まります。|[sql:identity 注釈と sql:guid 注釈の使用](../../relational-databases/sqlxml-annotated-xsd-schemas-using/using-the-sql-identity-and-sql-guid-annotations.md)|サポートされていません|  
|**sql:inverse**|アップデートグラムロジックに対して、 ** \<sql: relationship>** を使用して指定されている親子リレーションシップの解釈を逆に指示します。|[Sql: relationship での sql: 逆属性の指定 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)|サポートされていません|  
|**sql:is-constant**|どのテーブルにもマップされない XML 要素を作成します。 要素は、クエリ出力に表示されます。|[Sql を使用した定数要素の作成: &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-constant-elements-using-sql-is-constant-sqlxml-4-0.md)|同じ|  
|**sql:key-fields**|テーブル内の行を一意に識別する列を指定します。|[Sql: キーフィールド &#40;SQLXML 4.0&#41;を使用したキー列の識別](../../relational-databases/sqlxml-annotated-xsd-schemas-using/identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md)|同じ|  
|**sql:limit-field**<br /><br /> **sql:limit-value**|制限値に基づいて、返される値を制限します。|[Sql: limit-field および sql: limit-value &#40;SQLXML 4.0&#41;を使用した値のフィルター処理](../../relational-databases/sqlxml-annotated-xsd-schemas-using/filtering-values-using-sql-limit-field-and-sql-limit-value-sqlxml-4-0.md)|同じ|  
|**sql:mapped**|スキーマのアイテムを結果から除外します。|[Sql: マップト &#40;SQLXML 4.0&#41;を使用した結果の XML ドキュメントからのスキーマ要素の除外](../../relational-databases/sqlxml-annotated-xsd-schemas-using/excluding-schema-elements-from-the-xml-document-using-sql-mapped.md)|**マップ-フィールド**|  
|**sql:max-depth**|スキーマで指定される再帰リレーションシップの深さを指定します。|[sql:max-depth を使用した、再帰リレーションシップの深さの指定](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-depth-in-recursive-relationships-by-using-sql-max-depth.md)|サポートされていません|  
|**sql:overflow-field**|オーバーフローしたデータを含むデータベース列を識別します。|[Sql: overflow フィールドを使用した未使用データの取得 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/retrieving-unconsumed-data-using-the-sql-overflow-field-sqlxml-4-0.md)|同じ|  
|**sql:prefix**|有効な XML ID、IDREF、および IDREFS を作成します。 ID、IDREF、および IDREFS の値の前に文字列を付加します。|[Sql: prefix &#40;SQLXML 4.0&#41;を使用した有効な ID、IDREF、IDREFS 型の属性の作成](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-valid-id-idref-and-idrefs-type-attributes-using-sql-prefix-sqlxml-4-0.md)|同じ|  
|**sql:relationship**|XML 要素間のリレーションシップを指定します。 リレーションシップを確立するには、**親**、**子**、**親キー**、および**子キー**の属性を使用します。|[Sql: relationship を使用したリレーションシップの指定 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-relationships-using-sql-relationship-sqlxml-4-0.md)|属性名は次のように異なります。<br /><br /> **キーの関係**<br /><br /> **外部関係**<br /><br /> **レジストリ**<br /><br /> **外部キー**|  
|**sql:use-cdata**|XML ドキュメント内の特定の要素に、CDATA セクションを使用するよう指定します。|[Sql を使用した CDATA セクションの作成: &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-cdata-sections-using-sql-use-cdata-sqlxml-4-0.md)|同じ|  
  
> [!NOTE]  
>  XSD ネイティブ**targetNamespace**属性は、 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] XDR マッピングスキーマで導入された**ターゲット名前空間**の注釈を置き換えます。  
  
## <a name="see-also"></a>参照  
 [TargetNamespace 属性を使用してターゲットの名前空間を指定する &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-4-0.md)  
  
  
