---
title: modify() メソッド (xml データ型) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- modify() method
- modify method
ms.assetid: 52430735-51f4-46d1-a308-9aecf8648fda
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5c98ef9c726d2db5b5ec06d71a00de08288098a0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68051277"
---
# <a name="modify-method-xml-data-type"></a>modify() メソッド (xml データ型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  XML ドキュメントのコンテンツを変更します。 **xml** 型の変数または列のコンテンツを変更するには、このメソッドを使用します。 このメソッドは XML DML ステートメントを使用して、XML データのノードの挿入、更新、削除を行います。 **xml** データ型の **modify()** メソッドは、UPDATE ステートメントの SET 句内でしか使用できません。  
  
## <a name="syntax"></a>構文  
  
```  
  
modify (XML_DML)  
```  
  
## <a name="arguments"></a>引数  
 XML_DML  
 XML DML (データ操作言語) の文字列です。 XML ドキュメントは、この表記に従って更新されます。  
  
> [!NOTE]  
>  **modify()** メソッドが NULL 値を使用して呼び出される場合、または結果が NULL 値になる場合、エラーが返されます。  
  
## <a name="examples"></a>使用例  
 **modify()** メソッドには XML データ操作言語 (DML) の文字列が必要なので、**modify()** のサンプルは XML DML ステートメントについて説明するトピックに含まれています。 これらの例については、「[&#40;XML DML&#41; の挿入](../../t-sql/xml/insert-xml-dml.md)」、「[&#40;XML DML&#41; の削除](../../t-sql/xml/delete-xml-dml.md)」、および「[&#40;XML DML&#41; の値の置き換え](../../t-sql/xml/replace-value-of-xml-dml.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [XML データのインスタンスの作成](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml データ型メソッド](../../t-sql/xml/xml-data-type-methods.md)   
 [XML データ変更言語 &#40;XML DML&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
