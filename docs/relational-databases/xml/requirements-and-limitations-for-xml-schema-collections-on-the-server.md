---
title: 要件と制限 (XML スキーマ コレクション) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- identifiers [XML schema collections]
- XML schema collections [SQL Server], limitations
- substitution groups [XML in SQL Server]
- XML schema collections [SQL Server], guidelines
- lax validation
- enumeration facets [XML in SQL Server]
- decimal precision [XML in SQL Server]
- repeated XML schema collection values
- schema collections [SQL Server], limitations
- time zones [XML in SQL Server]
- precision decimals [XML in SQL Server]
- schema collections [SQL Server], guidelines
- lexical representation
ms.assetid: c2314fd5-4c6d-40cb-a128-07e532b40946
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
ms.openlocfilehash: fe65ba7995dc21b4bb5f5889c8667e9c8dfb6c10
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257619"
---
# <a name="requirements-and-limitations-for-xml-schema-collections-on-the-server"></a>サーバー上の XML スキーマ コレクションの要件と制限
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  XSD (XML Schema Definition Language) の検証には、 **xml** データ型を使用する SQL 列に関して制限事項がいくつかあります。 次の表は、このような制限事項に関する詳細と、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で機能するように XSD スキーマを変更するためのガイドラインを示しています。 このセクションのトピックでは、具体的な制限事項の詳細とその対処方法について説明します。  
  
|アイテム|制限事項|  
|----------|----------------|  
|**minOccurs** と **maxOccurs**|**minOccurs** 属性と **maxOccurs** 属性の値は、4 バイトの整数に収める必要があります。 これに違反するスキーマはサーバーで拒否されます。|  
|**\<xsd:choice>**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、**minOccurs** 属性値に 0 を指定してパーティクルを定義していない限り、子のない **\<xsd:choice>** パーティクルを持つスキーマは拒否します。|  
|**\<xsd:include>**|現在、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではこの要素をサポートしません。 この要素を含む XML スキーマはサーバーによって拒否されます。<br /><br /> 解決方法として、 **\<xsd:include>** ディレクティブを含む XML スキーマに前処理を行い、インクルードされるすべてのスキーマの内容をコピーおよびマージして 1 つのスキーマにすることで、サーバーにアップロードできます。 詳細については、「 [含まれているスキーマをマージするためのスキーマの前処理](../../relational-databases/xml/preprocess-a-schema-to-merge-included-schemas.md)」を参照してください。|  
|**\<xsd:key>** 、 **\<xsd:keyref>** 、および **\<xsd:unique>**|現在、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、一意性の強制や、キーおよびキー参照の確立を行うための、これらの XSD ベースの制約はサポートしません。 これらの要素を含む XML スキーマは登録できません。|  
|**\<xsd:redefine>**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではこの要素をサポートしません。 スキーマを更新するための別の方法については、「 [&#60;xsd:redefine&#62; 要素](../../relational-databases/xml/the-xsd-redefine-element.md)で機能するように XSD スキーマを変更するためのガイドラインを示しています。|  
|**\<xsd:simpleType>** 値|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 **xs:time** および **xs:dateTime**以外の秒部分を含む単純型はミリ秒単位の精度までしかサポートされず、 **xs:time** および **xs:dateTime**は 100 ナノ秒単位の精度までサポートされます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、認識されるすべての XSD 単純型の列挙に制限を適用します。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 **\<xsd:simpleType>** 宣言での "NaN" 値の使用はサポートしません。<br /><br /> 詳細については、「[&#60;xsd:simpleType&#62; 宣言の値](../../relational-databases/xml/values-for-xsd-simpletype-declarations.md)で機能するように XSD スキーマを変更するためのガイドラインを示しています。|  
|**xsi:schemaLocation** と **xsi:noNamespaceSchemaLocation**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では **xml** データ型の列や変数に挿入された XML インスタンス データにこれらの属性が含まれている場合、これらの属性を無視します。|  
|**xs:QName**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、XML スキーマ制約要素を使用している **xs:QName** から派生した型はサポートしません。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、メンバー要素に **xs:QName** を指定した共用体型はサポートしません。<br /><br /> 詳細については、「 [The xs:QName Type](../../relational-databases/xml/the-xs-qname-type.md)」を参照してください。|  
|既存の置換グループへのメンバーの追加|XML スキーマ コレクション内の既存の置換グループにメンバーを追加することはできません。 XML スキーマの置換グループは先頭要素のみで使用するように制限されているので、同じ CREATE XML SCHEMA COLLECTION ステートメントまたは ALTER XML SCHEMA COLLECTION ステートメントで置換グループのすべてのメンバー要素を定義する必要があります。|  
|正規の形式とパターン制限|値の正規表現は、その値の型のパターン制限に従う必要があります。 詳細については、「 [Canonical Forms and Pattern Restrictions](../../relational-databases/xml/canonical-forms-and-pattern-restrictions.md)」を参照してください。|  
|列挙ファセット|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、ファセットに違反するパターン ファセットや列挙を含む型を使用した XML スキーマはサポートしません。|  
|ファセット長|**length**ファセット、 **minLength**ファセット、および **maxLength** ファセットは **long** 型で格納されます。 この型は 32 ビット型です。 したがって、これらの値の許容範囲は 2^31 です。|  
|ID 属性|XML スキーマ コンポーネントは、それぞれ ID 属性を 1 つ含むことができます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、**ID** 型の **\<xsd:attribute>** 宣言に一意性を適用しますが、これらの値を格納しません。 一意性のスコープは、CREATE XML SCHEMA COLLECTION ステートメントまたは ALTER XML SCHEMA COLLECTION ステートメントで適用します。|  
|ID 型|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 **xs:ID**型、 **xs:IDREF**型、または **xs:IDREFS**型の要素はサポートしません。 スキーマでは、この型の要素や、この型の制限または拡張によって派生した要素を宣言できません。|  
|ローカル名前空間|**\<xsd:any>** 要素では、ローカル名前空間を明示的に指定する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、名前空間属性の値に空文字列 ("") を使用するスキーマを拒否します。 代わりに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では "##local" を明示的に使用して、修飾されない要素や属性をワイルドカード文字によるインスタンスとして示す必要があります。|  
|混合型と単純コンテンツ|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、混合型を単純コンテンツに制限することはできません。 詳細については、「 [Mixed Type and Simple Content](../../relational-databases/xml/mixed-type-and-simple-content.md)」を参照してください。|  
|NOTATION 型|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、NOTATION 型をサポートしません。|  
|メモリ不足状態|大きな XML スキーマ コレクションの操作では、メモリが不足することがあります。 この問題の解決方法については、「 [大きな XML スキーマ コレクションとメモリ不足状態](../../relational-databases/xml/large-xml-schema-collections-and-out-of-memory-conditions.md)」を参照してください。|  
|繰り返される値|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、block 属性または final 属性で "restriction restriction" や "extension extension" のように値を繰り返すスキーマが拒否されます。|  
|スキーマ コンポーネントの識別子|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、スキーマ コンポーネントの識別子の最大長を Unicode 文字 1,000 文字に制限します。 また、識別子に補助文字のペアを使用することはできません。|  
|タイム ゾーン情報|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降のバージョンでは、 **xs:date**、 **xs:time**、および **xs:dateTime** の値について、XML スキーマ検証でタイム ゾーンの情報が完全にサポートされます。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 後方互換性モードでは、タイム ゾーン情報は常に協定世界時 (グリニッジ標準時) を基準として正規化されます。 **dateTime** 型の要素の場合は、サーバー側でオフセット値 ("-05:00") を使用して対応する GMT 時を返すことによって、指定された時間を GMT に変換します。|  
|共用体型|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、共用体型からの制限はサポートしません。|  
|可変精度の 10 進数|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、有効桁数が可変の 10 進数はサポートしません。 **xs:decimal** 型は任意の有効桁数の 10 進数を表します。 XML プロセッサに準拠するには、最低でも `totalDigits=18`以上の 10 進数をサポートする必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 `totalDigits=38,` をサポートしますが、小数部は 10 桁に制限されます。 インスタンス化されたすべての **xs:decimal** 値は、サーバーでは SQL 型数値 (38, 10) を使用して内部的に表現されます。|  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|[説明]|  
|-----------|-----------------|  
|[正規の形式とパターン制限](../../relational-databases/xml/canonical-forms-and-pattern-restrictions.md)|正規の形式とパターン制限について説明します。|  
|[ワイルドカード コンポーネントと内容検証](../../relational-databases/xml/wildcard-components-and-content-validation.md)|XML スキーマ コレクションでのワイルドカード文字、lax 検証、および anyType 要素の使用に関する制限について説明します。|  
|[&#60;xsd:redefine&#62; 要素](../../relational-databases/xml/the-xsd-redefine-element.md)|\<xsd:redefine> 要素の使用に関する制限とその回避策について説明します。|  
|[xs:QName 型](../../relational-databases/xml/the-xs-qname-type.md)|xs:QName 型に関する制限について説明します。|  
|[&#60;xsd:simpleType&#62; 宣言の値](../../relational-databases/xml/values-for-xsd-simpletype-declarations.md)|\<xsd:simpleType> 宣言に適用される制限について説明します。|  
|[列挙ファセット](../../relational-databases/xml/enumeration-facets.md)|列挙ファセットに関する制限について説明します。|  
|[混合型と単純コンテンツ](../../relational-databases/xml/mixed-type-and-simple-content.md)|混合型を単純コンテンツに制限する場合の制限について説明します。|  
|[大きな XML スキーマ コレクションとメモリ不足状態](../../relational-databases/xml/large-xml-schema-collections-and-out-of-memory-conditions.md)|大きなスキーマ コレクションで発生することがあるメモリ不足の解決方法について説明します。|  
|[非決定的コンテンツ モデル](../../relational-databases/xml/non-deterministic-content-models.md)|非決定的コンテンツ モデルに関する制限について説明します。|  
  
## <a name="see-also"></a>参照  
 [XML データ &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)   
 [型指定された XML と型指定されていない XML の比較](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML スキーマ コレクションに対する権限の許可](../../relational-databases/xml/grant-permissions-on-an-xml-schema-collection.md)   
 [一意のパーティクル属性の制約](../../relational-databases/xml/unique-particle-attribution-constraint.md)   
 [XML スキーマ コレクション &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
