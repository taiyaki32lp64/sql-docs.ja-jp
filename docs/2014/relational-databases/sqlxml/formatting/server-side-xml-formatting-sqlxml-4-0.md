---
title: サーバー側の XML 書式設定 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- FOR XML clause, formatting
- server-side XML formatting
ms.assetid: ae9ea068-0857-4505-a3b2-f53d256b644c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: af44d854ba28e8e8ac3b1a4572bf9b222f20299b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66012208"
---
# <a name="server-side-xml-formatting-sqlxml-40"></a>サーバー側の XML 書式設定 (SQLXML 4.0)
  ここでは、Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のデータベースに対するクエリを実行して生成される行セットを基に、サーバー側で XML ドキュメントを書式設定する場合の情報をまとめます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、データベース テーブルに XML ドキュメントを格納したり、データベース テーブルから XML ドキュメントを取得することができます。 XML ドキュメントを取得するには、SELECT クエリで FOR XML クエリ拡張を使用します。  
  
 たとえば、クライアント アプリケーションに対してコマンドを実行する[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]次で構成される[!INCLUDE[tsql](../../../includes/tsql-md.md)]クエリ。  
  
```  
SELECT FirstName, LastName  
FROM   Person.Contact  
FOR XML AUTO  
```  
  
 サーバーでは、クエリが 2 段階で実行されます。 最初に、サーバーでは次の SELECT ステートメントが実行されます。  
  
```  
SELECT FirstName, LastName  
FROM   Person.Contact  
```  
  
 次に、サーバーでは生成された行セットに対して FOR XML 変換が適用され、 結果の XML が 1 列の行セットとしてクライアントに送られます。 このドキュメントでは、この処理をサーバー側の XML 書式設定と呼びます。  
  
 サーバー側では、FOR XML 句で次のモードを指定できます。  
  
-   RAW  
  
-   AUTO  
  
-   EXPLICIT  
  
 FOR XML 句の詳細については、次を参照してください。 [For を使用して XML](../../xml/for-xml-sql-server.md)します。  
  
## <a name="see-also"></a>参照  
 [クライアント側とサーバー側の XML 書式設定のアーキテクチャ&#40;SQLXML 4.0&#41;](architecture-of-client-side-and-server-side-xml-formatting-sqlxml-4-0.md)   
 [クライアント側の XML 書式設定&#40;SQLXML 4.0&#41;](client-side-xml-formatting-sqlxml-4-0.md)   
 [FOR XML &#40;SQL Server&#41;](../../xml/for-xml-sql-server.md)  
  
  
