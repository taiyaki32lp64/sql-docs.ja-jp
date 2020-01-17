---
title: 非決定的コンテンツ モデル | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- non-deterministic content models
- content models [XML in SQL Server]
ms.assetid: 9d4513e7-dd19-4491-b7c7-28bc7c2f8589
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4de53a22bb650098db48619bef26efe543dd9ebd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68137434"
---
# <a name="non-deterministic-content-models"></a>非決定的コンテンツ モデル
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 1 (SP1) よりも前の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、非決定的コンテンツ モデルを含む XML スキーマは拒否されていました。  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP1 以降では、オカレンス制約が 0、1、または unbounded の場合、非決定的コンテンツ モデルが許容されます。  
  
## <a name="example-non-deterministic-content-model-rejected"></a>例: 拒否される非決定的コンテンツ モデル  
 次の例では、非決定的コンテンツ モデルを含む XML スキーマの作成を試みています。 このコードは、 `<root>` 要素には 2 つの `<a>` 要素で構成されたシーケンスが 1 つ必要なのか、 `<root>` 要素にはそれぞれ `<a>` 要素を含む 2 つのシーケンスが必要なのかが明確ではないので失敗します。  
  
```  
CREATE XML SCHEMA COLLECTION MyCollection AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
    <element name="root">  
        <complexType>  
            <sequence minOccurs="1" maxOccurs="2">  
                <element name="a" type="string" minOccurs="1" maxOccurs="2"/>  
            </sequence>  
        </complexType>  
    </element>  
</schema>  
'  
GO  
```  
  
 このスキーマは、オカレンス制約を固有の位置に移動することにより修正できます。 たとえば、親要素であるシーケンス パーティクルに制約を移動できます。  
  
```  
<sequence minOccurs="1" maxOccurs="4">  
    <element name="a" type="string" minOccurs="1" maxOccurs="1"/>  
</sequence>  
```  
  
 または、子要素に制約を移動することもできます。  
  
```  
<sequence minOccurs="1" maxOccurs="1">  
     <element name="a" type="string" minOccurs="1" maxOccurs="4"/>  
</sequence>  
```  
  
## <a name="example-non-deterministic-content-model-accepted"></a>例: 許容される非決定的コンテンツ モデル  
 次のスキーマは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SP1 よりも前のバージョンの [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] では拒否されます。  
  
```  
CREATE XML SCHEMA COLLECTION MyCollection AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
    <element name="root">  
        <complexType>  
            <sequence minOccurs="0" maxOccurs="unbounded">  
                <element name="a" type="string" minOccurs="0" maxOccurs="1"/>  
                <element name="b" type="string" minOccurs="1" maxOccurs="unbounded"/>  
            </sequence>  
        </complexType>  
    </element>  
</schema>  
'  
GO  
```  
  
## <a name="see-also"></a>参照  
 [サーバー上の XML スキーマ コレクションの要件と制限](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
