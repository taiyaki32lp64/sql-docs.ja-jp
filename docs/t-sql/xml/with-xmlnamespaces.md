---
title: WITH XMLNAMESPACES (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WITH_XMLNAMESPACES_TSQL
- WITH XMLNAMESPACES
dev_langs:
- TSQL
helpviewer_keywords:
- adding XML namespaces
- XML namespace declarations [SQL Server]
- clauses [SQL Server], WITH XMLNAMESPACES
- WITH XMLNAMESPACES clause
- declaring XML namespaces
ms.assetid: 3b32662b-566f-454d-b7ca-e247002a9a0b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 86bdd12d5dabd7ad74662cd47b2004594328a6c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68048139"
---
# <a name="with-xmlnamespaces"></a>WITH XMLNAMESPACES
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  1 つまたは複数の XML 名前空間を宣言します。  
  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
WITH XMLNAMESPACES ( <XML namespace declaration item>  
[ { , <XML namespace declaration item> }...] )   
  
<XML namespace declaration item> ::=  
<xml_namespace_uri> AS <xml_namespace_prefix>  
| <XML default namespace declaration item>  
<xml_namespace_uri> ::= <character string literal>  
```  
  
```  
  
<xml_namespace_prefix> ::= <identifier>  
```  
  
```  
  
<XML default namespace declaration item> ::=  
DEFAULT <xml_namespace_uri>  
  
```  
  
## <a name="arguments"></a>引数  
 *xml_namespace_uri*  
 宣言する XML 名前空間を識別する Uniform Resource Identifier (URI) を指定します。 *xml_namespace_uri* は SQL 文字列です。  
  
 *xml_namespace_prefix*  
 *xml_namespace_uri* で指定した名前空間 URI 値にマップされ、関連付けられるプレフィックスを指定します。 *xml_namespace_prefix* は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別子にする必要があります。  
  
## <a name="remarks"></a>Remarks  
 共通テーブル式を含むステートメントで WITH XMLNAMESPACES 句を使用する場合は、ステートメント内で WITH XMLNAMESPACES 句を共通テーブル式より前に置く必要があります。  
  
 次は、WITH XMLNAMESPACES 句を使用するときに適用される一般的な構文規則です。  
  
-   XML 名前空間の各宣言には、既定の XML 名前空間宣言の項目が少なくとも 1 つ含まれている必要があります。  
  
-   使用する各 XML 名前空間プレフィックスは、名前の一部にコロン (:) が使用されていない名前 (NCName) であることが必要です。  
  
-   名前空間プレフィックスは 2 回定義できません。  
  
-   XML 名前空間プレフィックスと URI では、大文字小文字が区別されます。  
  
-   XML 名前空間プレフィックス `xmlns` は宣言できません。  
  
-   XML 名前空間接頭辞 `xml` は、名前空間 URI `'http://www.w3.org/XML/1998/namespace'` と別のプレフィックスを割り当てることができないこの URI 以外の名前空間ではオーバーライドできません。  
  
-   クエリで ELEMENTS XSINIL ディレクティブが使用されている場合、XML 名前空間プレフィックス `xsi` は再宣言できません。  

-   xsi 標準名前空間を使用するために 'http://www.w3.org/2001/XMLSchema-instance ' を宣言する必要はありません。 'http://www.w3.org/2001/XMLSchema-instance ' スキーマが xml ドキュメントで正しく宣言されている限り、未指定の場合は XML/XPATH プロセッサによって暗黙的に追加され、xpath 式で xsi プレフィックスを使用できます。

-   URI 文字列値は、現在のデータベースの照合順序のコード ページに基づいてエンコードされ、内部で Unicode に変換されます。  
  
-   XML 名前空間 URI では、**xs:anyURI** で使用される XSD の空白短縮の規則に従って空白が短縮されます。 また、XML 名前空間 URI 値は、エンティティ化または非エンティティ化されないことに注意してください。  

-   XML 名前空間 URI に対して、無効な XML 1.0 文字がないかどうかが確認され、検出された場合はエラーが生成されます (U+0007 など)。  
  
-   空白が短縮された後の XML 名前空間 URI が長さ 0 の文字列になると、"無効な空の名前空間 URI" エラーが発生します。  
  
-   XMLNAMESPACES キーワードは WITH 句のコンテキストでは予約されています。  
  
## <a name="examples"></a>使用例  
 例については、「 [WITH XMLNAMESPACES を使用したクエリへの名前空間の追加](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [XQuery 言語リファレンス &#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md)  
  
  
