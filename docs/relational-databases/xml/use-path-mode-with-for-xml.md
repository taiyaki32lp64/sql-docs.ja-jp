---
title: FOR XML での PATH モードの使用 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- PATH FOR XML mode
- characters [SQL Server], XML
- aliases [SQL Server], XML
- FOR XML clause, PATH mode
- FOR XML PATH mode
- column names [SQL Server]
- XPath queries [SQL Server]
ms.assetid: a685a9ad-3d28-4596-aa72-119202df3976
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dff9b54963eb88bb29172d270c092c33d0be4127
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039169"
---
# <a name="use-path-mode-with-for-xml"></a>FOR XML での PATH モードの使用
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  「 [FOR XML を使用した XML の構築](../../relational-databases/xml/for-xml-sql-server.md)」で説明したように、PATH モードを使用すると、要素と属性の組み合わせが容易になります。 入れ子構造を使用することで、複雑なプロパティも容易に表現できるようになります。 FOR XML EXPLICIT モードのクエリを使用してこのような XML を行セットから作成することもできますが、煩雑になりかねない EXPLICIT モードのクエリに比べて PATH モードでは同じことを簡潔に行うことができます。 PATH モードに、入れ子の FOR XML クエリと、 **xml** 型のインスタンスを返す TYPE ディレクティブを組み合わせることで、簡潔なクエリを記述できます。  
  
 PATH モードでは、列名または列の別名が XPath 式として処理されます。 XPath 式は XML に値がどのようにマップされているかを示します。 各 XPath 式は、行要素に対して相対的に生成されるノードの種類 (属性、要素、スカラー値など) および名前と階層を提供する相対 XPath です。  
  
 ここでは、さまざまな条件における行セットでの列のマッピングについて説明し、例を示します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [名前のない列](../../relational-databases/xml/columns-without-a-name.md)  
  
-   [名前のある列](../../relational-databases/xml/columns-with-a-name.md)  
  
-   [名前をワイルドカード文字で指定した列](../../relational-databases/xml/columns-with-a-name-specified-as-a-wildcard-character.md)  
  
-   [XPath ノード テストの名前が付いた列](../../relational-databases/xml/columns-with-the-name-of-an-xpath-node-test.md)  
  
-   [パスを data&#40;&#41; として指定した列の名前](../../relational-databases/xml/column-names-with-the-path-specified-as-data.md)  
  
-   [NULL 値が含まれる列の既定動作](../../relational-databases/xml/columns-that-contain-a-null-value-by-default.md)  
  
-   [PATH モードでの名前空間のサポート](../../relational-databases/xml/namespace-support-in-path-mode.md)  
  
-   [例: PATH モードの使用](../../relational-databases/xml/examples-using-path-mode.md)  
  
## <a name="see-also"></a>参照  
 [WITH XMLNAMESPACES を使用したクエリへの名前空間の追加](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)  
  
  
