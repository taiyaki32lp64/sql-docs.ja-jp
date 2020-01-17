---
title: UPDATE、DELETE、および INSERT ステートメント |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], about updating data
- DELETE [ODBC]
- UPDATE [ODBC]
- INSERT [ODBC]
- data updates [ODBC], about data updates
ms.assetid: 5004ea72-4c49-4064-9752-f7032ba7f133
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c2a2787be1bf44e1f214d396444a73b938acf7ce
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942838"
---
# <a name="update-delete-and-insert-statements"></a>UPDATE、DELETE、INSERT ステートメント
SQL ベースのアプリケーションでは、 **UPDATE**、**DELETE**、および **INSERT** ステートメントを実行してテーブルに変更を加えます。 これらのステートメントは、Minimum SQL 文法準拠レベルの一部であり、すべてのドライバーとデータ ソースによってサポートされている必要があります。  
  
 これらのステートメントの構文です。  
  
 **UPDATE** _table-name_  
  
 **SET** _列識別子_ **=** {*式* | **NULL**}  
  
 [ **,**  _列識別子_ **=** {*式* | **NULL**}].  
  
 [**WHERE** _search-condition_]  
  
 **DELETE FROM** _table-name_[**WHERE** _search-condition_]  
  
 **INSERT INTO** _テーブル名_[ **(** _列識別子_[ **、** _列識別子_]... **)** ]  
  
 {*クエリ仕様* | **VALUES (** _挿入値_[ **,** _挿入値_]. **)** }  
  
 なお、*クエリ仕様*要素は、コアと拡張 SQL 文法とでのみ有効ですが、*式*と*検索条件*要素の詳細になりますコアと拡張 SQL 文法で複雑です。  
  
 他の SQL ステートメントと同様に、**UPDATE**、**DELETE** および **INSERT** ステートメントは、パラメーターを使用するとより効率的です。 たとえば、次のステートメントを準備して繰り返し実行することで、 Orders テーブルに複数の行を挿入できます。  
  
```  
INSERT INTO Orders (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 この効率性のパラメーター値の配列を渡すことによって増やすことができます。 ステートメントのパラメーターとパラメーター値の配列の詳細については、次を参照してください。[ステートメント パラメーター](../../../odbc/reference/develop-app/statement-parameters.md)します。
