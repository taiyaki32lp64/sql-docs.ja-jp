---
title: 一意のパーティクル属性の制約 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
f1_keywords:
- unique particle attribution
helpviewer_keywords:
- schema collections [SQL Server], unique particle attribution
- XML schema collections [SQL Server], unique particle attribution
- UPA constraint rule
- unique particle attribution constraint rule
ms.assetid: 6bb879e9-a5ee-402e-94e4-fe8cec5966b0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b09c2392f49bdfb8a86c33ce16679ec02c232310
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078014"
---
# <a name="unique-particle-attribution-constraint"></a>一意のパーティクル属性の制約
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  XSD では、UPA (一意のパーティクル属性) 制約の規則によって、複雑なコンテンツ モデルが制約を受けます。 この規則では、あいまいさを排除し、インスタンス ドキュメント内の各要素が、その親のコンテンツ モデル内の `<xsd:element>` パーティクルまたは `<xsd:any>` パーティクルの 1 つに正確に対応することが必要です。 あいまいなコンテンツ モデルになる可能性のある型を含むスキーマは拒否されます。  
  
 あいまいさの最も一般的な原因は、`<xsd:any>` のワイルドカード文字や、minOccurs < maxOccurs のような可変の出現範囲を持つパーティクルです。 たとえば、次のコンテンツ モデルでは、<`e1`> 要素は `<xsd:element>` 要素または `<xsd:any>` 要素のどちらにも一致するので、あいまいになります。  
  
```  
<xsd:element name="root">  
    <xsd:complexType>  
        <xsd:choice>  
            <xsd:element name="e1"/>  
            <xsd:any namespace="##any"/>  
        </xsd:choice>  
    </xsd:complexType>  
</xsd:element>  
```  
  
 また、次のコンテンツ モデルもあいまいです。  
  
```  
<xsd:element name="root">  
    <xsd:complexType>  
        <xsd:sequence>  
            <xsd:element name="e1" maxOccurs="2"/>  
            <xsd:element name="e2" minOccurs="0"/>  
            <xsd:element name="e1"/>  
        </xsd:sequence>  
    </xsd:complexType>  
</xsd:element>  
```  
  
 `<root><e1/><e2/><e1/></root>` などのドキュメントは明確に検証できますが、 `<root><e1/><e1/></root>` などのドキュメントは明確に検証できません。これは、2 番目の `<xsd:element>` がどの `<e1/>` に対応するかが明確でないためです。 一部のドキュメントを明確に検証できても、あいまいさが残る可能性があるため、スキーマは拒否されます。  
  
 コンテンツ モデルが有効であるためには、先行読み取りを行わなくても、インスタンスを明確に検証できる必要があります。 たとえば、次のコンテンツ モデルについて考えてみます。  
  
```  
<xsd:element name="root">  
    <xsd:complexType>  
        <xsd:choice>  
           <xsd:sequence>  
               <xsd:element name="e1"/>  
               <xsd:element name="e2"/>  
           </xsd:sequence>  
           <xsd:sequence>  
               <xsd:element name="e1"/>  
               <xsd:element name="e3"/>  
           </xsd:sequence>  
       </xsd:choice>  
    </xsd:complexType>  
</xsd:element>  
```  
  
 `<root><e1/><e3/></root>`などのドキュメントの場合、シーケンス `<e1/><e3/>` が 2 番目の `<xsd:sequence>`に明確に一致します。 ただし、 `<xsd:element>` を先行読み取りしないと、 `<e1/>` が対応する `<e3/>`を決定できないので、コンテンツ モデルは UPA 制約規則に違反することになります。  
  
## <a name="finding-more-information"></a>詳細情報  
 次のドキュメントは W3C (World Wide Web Consortium) が発行したもので、一意のパーティクル属性の制約に関する技術的な説明が含まれています。  
  
 "XML Schema Part 1: Structures Second Edition, W3C Proposed Edited Recommendation":  
  
-   Section 3.8.6: Constraints on Model Group Schema Components  
  
-   Appendix H: Analysis of the Unique Particle Attribution Constraint (non-normative)  
  
 ドキュメントを表示するには、[http://www.w3.org/TR/xmlschema-1](https://go.microsoft.com/fwlink/?linkid=48881) を参照してください。  
  
## <a name="see-also"></a>参照  
 [XML スキーマ コレクション &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
