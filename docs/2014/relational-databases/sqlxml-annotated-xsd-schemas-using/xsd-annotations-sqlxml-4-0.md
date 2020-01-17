---
title: XSD 注釈 (SQLXML 4.0) |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, annotations listed
- XSD schemas [SQLXML], annotations
ms.assetid: c62a6785-8d66-40a2-9c5d-80c73d600a3b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1b9e50cc418ef1fa2076b3207d7d3429694f160a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66013545"
---
# <a name="xsd-annotations-sqlxml-40"></a>XSD 注釈 (SQLXML 4.0)
  次の表では、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] で導入された XSD 注釈の一覧を示し、これらを [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] で導入された XDR 注釈と比較します。  
  
|XSD 注釈|説明|トピックへのリンク|XDR 注釈|  
|--------------------|-----------------|----------------|--------------------|  
|`sql:encode`|XML 要素または属性を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] BLOB 列にマップするときに、参照 URI を要求します。 この URI は、後で BLOB データを返すために使用できます。|[使用した BLOB データへの URL 参照の要求: エンコード&#40;SQLXML 4.0&#41;](requesting-url-references-to-blob-data-using-sql-encode-sqlxml-4-0.md)|`url-encode`|  
|`sql:guid`|列に対し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により生成される GUID 値を使用するか、アップデートグラムで提供される値を使用するかを指定します。|[sql:identity 注釈と sql:guid 注釈の使用](using-the-sql-identity-and-sql-guid-annotations.md)|サポートされていません|  
|`sql:hide`|スキーマで指定されている要素または属性を、結果の XML ドキュメントで表示しないようにします。|[sql:hide を使用した要素と属性の非表示](hiding-elements-and-attributes-by-using-sql-hide.md)|サポートされていません|  
|`sql:identity`|IDENTITY 型のデータベース列にマップされる任意のノードに指定できます。 この注釈に指定した値によって、データベース内の対応する IDENTITY 型列の更新方法が決まります。|[sql:identity 注釈と sql:guid 注釈の使用](using-the-sql-identity-and-sql-guid-annotations.md)|サポートされていません|  
|`sql:inverse`|逆に、アップデート グラム ロジックを使用して指定されている親子リレーションシップに解釈するように指示します **\<sql:relationship >** します。|[Sql:relationship での sql:inverse 属性指定&#40;SQLXML 4.0&#41;](specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)|サポートされていません|  
|`sql:is-constant`|どのテーブルにもマップされない XML 要素を作成します。 要素は、クエリ出力に表示されます。|[定数要素を使用した作成します定数&#40;SQLXML 4.0。&#41;](creating-constant-elements-using-sql-is-constant-sqlxml-4-0.md)|同じ|  
|`sql:key-fields`|テーブル内の行を一意に識別する列を指定します。|[キー列を使用して sql:key を識別する-フィールド&#40;SQLXML 4.0&#41;](identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md)|同じ|  
|`sql:limit-field`<br /><br /> `sql:limit-value`|制限値に基づいて、返される値を制限します。|[Sql:limit の値を使用してフィルター処理、およびフィールドの値&#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-limit-field-and-sql-limit-value.md)|同じ|  
|`sql:mapped`|スキーマのアイテムを結果から除外します。|[結果として得られる XML ドキュメントを使用して sql のスキーマ要素の除外: マップ&#40;SQLXML 4.0&#41;](excluding-schema-elements-from-the-xml-document-using-sql-mapped.md)|`map-field`|  
|`sql:max-depth`|スキーマで指定される再帰リレーションシップの深さを指定します。|[sql:max-depth を使用した再帰リレーションシップの深さの指定](specifying-depth-in-recursive-relationships-by-using-sql-max-depth.md)|サポートされていません|  
|`sql:overflow-field`|オーバーフローしたデータを含むデータベース列を識別します。|[未使用データを使用して、sql:overflow を取得する-フィールド&#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-overflow-field.md)|同じ|  
|`sql:prefix`|有効な XML ID、IDREF、および IDREFS を作成します。 ID、IDREF、および IDREFS の値の前に文字列を付加します。|[Sql:prefix 有効な ID、IDREF、IDREFS 型属性を使用した&#40;SQLXML 4.0&#41;](creating-valid-id-idref-and-idrefs-type-attributes-using-sql-prefix-sqlxml-4-0.md)|同じ|  
|`sql:relationship`|XML 要素間のリレーションシップを指定します。 リレーションシップの確立には、`parent`、`child`、`parent-key` および `child-key` 属性を使用します。|[使用したリレーションシップ sql:relationship を指定する&#40;SQLXML 4.0&#41;](specifying-relationships-using-sql-relationship-sqlxml-4-0.md)|属性名は次のように異なります。<br /><br /> `key-relation`<br /><br /> `foreign-relation`<br /><br /> `key`<br /><br /> `foreign-key`|  
|`sql:use-cdata`|XML ドキュメント内の特定の要素に、CDATA セクションを使用するよう指定します。|[使用した CDATA セクション sql:use を作成する-cdata &#40;SQLXML 4.0&#41;](creating-cdata-sections-using-sql-use-cdata-sqlxml-4-0.md)|同じ|  
  
> [!NOTE]  
>  XSD ネイティブの `targetNamespace` 属性は、[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] の XDR マッピング スキーマで導入された `target-namespace` 注釈に代わるものです。  
  
## <a name="see-also"></a>参照  
 [Target Namespace を使用して、targetNamespace 属性を指定する&#40;SQLXML 4.0&#41;](specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-4-0.md)  
  
  
