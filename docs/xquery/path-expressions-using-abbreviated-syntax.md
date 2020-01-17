---
title: パス式の構文を使用して簡略化された |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- axis step [XQuery]
- abbreviated syntax [XQuery]
ms.assetid: f83c2e41-5722-47c3-b5b8-bf0f8cbe05d3
author: rothja
ms.author: jroth
ms.openlocfilehash: 8e75db08f283631cf9b5daf064790786a1abc10f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946414"
---
# <a name="path-expressions---using-abbreviated-syntax"></a>パス式 - 省略構文の使用
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  すべての例で[では、XQuery パス式について](../xquery/path-expressions-xquery.md)パス式は省略しない構文を使用します。 パス式の軸ステップの省略構文では、軸名とノード テストを 2 つのコロン (::) で区切り、その後にステップ修飾子を指定します。ステップ修飾子は、指定しなくてもかまいません。  
  
 以下に例を示します。  
  
```  
child::ProductDescription[attribute::ProductModelID=19]  
```  
  
 XQuery は、パス式で次の省略をサポートしています。  
  
-   **子**軸は既定の軸。 そのため、**子::** 軸は、式のステップから省略できます。 たとえば、`/child::ProductDescription/child::Summary`として記述できます`/ProductDescription/Summary`します。  
  
-   **属性**として省略できます@します。 たとえば、`/child::ProductDescription[attribute::ProductModelID=10]`として記述できます`/ProudctDescription[@ProductModelID=10]`します。  
  
-   A **/descendant-or-self::node()** ように短縮できます//。 たとえば、`/descendant-or-self::node()/child::act:telephoneNumber`として記述できます`//act:telephoneNumber`します。  
  
     前のクエリでは、Contact テーブルの AdditionalContactInfo 列に格納されているすべての電話番号を取得します。 AdditionalContactInfo のスキーマが方法で定義されている、 \<telephoneNumber > 要素がドキュメントにどこでも表示できます。 したがって、すべての電話番号を取得するには、ドキュメント内のすべてのノードを検索する必要があります。 検索は、ドキュメントのルートから開始され、続いてすべての子孫ノードが検索されます。  
  
     次のクエリは、特定の顧客の連絡先のすべての電話番号を取得します。  
  
    ```  
    SELECT AdditionalContactInfo.query('             
                declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";             
                declare namespace crm="https://schemas.adventure-works.com/Contact/Record";             
                declare namespace ci="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";             
                /descendant-or-self::node()/child::act:telephoneNumber             
                ') as result             
    FROM Person.Contact             
    WHERE ContactID=1             
    ```  
  
     省略構文のパス式に置き換えた場合`//act:telephoneNumber`、同じ結果が表示されます。  
  
-   **Self::node()** の手順では、1 つのドット (.) を省略できます。 ただし、ドットでないと同等か、互換性、 **self::node()** します。  
  
     たとえば、次のクエリでは、ドットを使用して、ノードではなく値を表しています。  
  
    ```  
    ("abc", "cde")[. > "b"]  
    ```  
  
-   **Parent::node()** の手順では、2 つのドット (.) を省略できます。  
  
  
