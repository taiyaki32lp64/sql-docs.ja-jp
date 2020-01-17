---
title: FOR XML での PATH モードの使用 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 3e7dba8ee18697f2c8940eab2ea6489e6eec687c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63231240"
---
# <a name="use-path-mode-with-for-xml"></a>FOR XML での PATH モードの使用
  「 [FOR XML を使用した XML の構築](for-xml-sql-server.md)」で説明したように、PATH モードを使用すると、要素と属性の組み合わせが容易になります。 入れ子構造を使用することで、複雑なプロパティも容易に表現できるようになります。 FOR XML EXPLICIT モードのクエリを使用してこのような XML を行セットから作成することもできますが、煩雑になりかねない EXPLICIT モードのクエリに比べて PATH モードでは同じことを簡潔に行うことができます。 PATH モードに、入れ子の FOR XML クエリと、 **xml** 型のインスタンスを返す TYPE ディレクティブを組み合わせることで、簡潔なクエリを記述できます。  
  
 PATH モードでは、列名または列の別名が XPath 式として処理されます。 XPath 式は XML に値がどのようにマップされているかを示します。 各 XPath 式は、行要素に対して相対的に生成されるノードの種類 (属性、要素、スカラー値など) および名前と階層を提供する相対 XPath です。  
  
 ここでは、さまざまな条件における行セットでの列のマッピングについて説明し、例を示します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [名前のない列](columns-without-a-name.md)  
  
-   [名前のある列](columns-with-a-name.md)  
  
-   [名前をワイルドカード文字で指定した列](columns-with-a-name-specified-as-a-wildcard-character.md)  
  
-   [XPath ノード テストの名前が付いた列](columns-with-the-name-of-an-xpath-node-test.md)  
  
-   [パスを data&#40;&#41; として指定した列の名前](column-names-with-the-path-specified-as-data.md)  
  
-   [NULL 値が含まれる列の既定動作](columns-that-contain-a-null-value-by-default.md)  
  
-   [PATH モードでの名前空間のサポート](namespace-support-in-path-mode.md)  
  
-   [例: PATH モードの使用](examples-using-path-mode.md)  
  
## <a name="see-also"></a>関連項目  
 [WITH XMLNAMESPACES を使用したクエリへの名前空間の追加](add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)   
 [FOR XML &#40;SQL Server&#41;](for-xml-sql-server.md)  
  
  
