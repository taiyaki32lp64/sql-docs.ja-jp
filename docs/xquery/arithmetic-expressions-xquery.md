---
title: 算術式 (XQuery) |Microsoft Docs
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
- expressions [XQuery], arithmetic
- arithmetic expressions
ms.assetid: 90d675bf-56da-459a-9771-8cd13920a9fc
author: rothja
ms.author: jroth
ms.openlocfilehash: ccbeda01726a3473f8e955676c3ebd62a93fd630
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67985738"
---
# <a name="arithmetic-expressions-xquery"></a>算術式 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  すべての算術演算子がサポートされている、除く**idiv**します。 次の例は、算術演算子の基本的な使用方法を示しています。  
  
```  
DECLARE @x xml  
SET @x=''  
SELECT @x.query('2 div 2')  
SELECT @x.query('2 * 2')  
```  
  
 **Idiv**はサポートされていないソリューションを使用するが、 **xs:integer()** コンス トラクター。  
  
```  
DECLARE @x xml  
SET @x=''  
-- Following will not work  
-- SELECT @x.query('2 idiv 2')  
-- Workaround   
SELECT @x.query('xs:integer(2 div 3)')  
```  
  
 算術演算子を使用した演算結果の型は入力値の型によって決まります。 オペランドどうしの型が異なる場合、必要に応じて一方または両方のオペランドが、データ型階層に基づき共通のプリミティブな基本データ型にキャストされます。 型階層については、次を参照してください。[型キャストの規則では、XQuery](../xquery/type-casting-rules-in-xquery.md)します。  
  
 数値データ型の上位変換は、2 つのオペランドが異なる数値基本データ型である場合に行われます。 などの追加、 **xs:decimal**を**xs:double** double 型の値を 10 進数の値がまずします。 次に、結果が double 型の値となる加算処理が行われます。  
  
 アトミック値の型指定されていない場合は、もう一方のオペランドの数値基本型、またはキャスト**xs:double**もう一方のオペランドも型指定された場合。  
  
## <a name="implementation-limitations"></a>実装の制限事項  
 制限事項を次に示します。  
  
-   算術演算子の引数が数値型にする必要がありますまたは**untypedAtomic**します。  
  
-   に対する操作**xs:integer**値型の値になる**xs:decimal**の代わりに**xs:integer**します。  
  
  
