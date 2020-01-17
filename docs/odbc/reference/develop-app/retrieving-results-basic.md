---
title: 検索 (Basic) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], about result sets
- data sources [ODBC], result sets
- empty result sets [ODBC]
ms.assetid: 052870e3-3f3f-4f07-91da-b649348225f4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7abe4dd2f0bfb0b5302022d8e50cddc7df84f192
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020471"
---
# <a name="retrieving-results-basic"></a>結果の取得 (基本)
*結果セット*は特定の条件に一致するデータ ソースで行のセットです。 これは、クエリの実行結果し、するが表形式で、アプリケーションで使用できる概念テーブルです。 **SELECT**ステートメント、カタログ関数、およびいくつかの手順は、結果セットを作成します。 次の例では、最初の SQL ステートメントのすべての行と、Orders テーブルのすべての列を含む結果セットを作成して 2 番目の SQL ステートメントは、Orders テーブル内の行の OrderID、営業担当者、および状態の列を含む結果セットを作成します。状態の開く。  
  
```  
SELECT * FROM Orders  
SELECT OrderID, SalesPerson, Status FROM Orders WHERE Status = 'OPEN'  
```  
  
 結果セットを空にすることとは異なる結果がすべての設定はありません。 たとえば、次の SQL ステートメントは、空の結果セットを作成します。  
  
```  
SELECT * FROM Orders WHERE 1 = 2  
```  
  
 空の結果セットは、設定する点を除いて、行を持たないその他の結果と変わりません。 たとえば、アプリケーション、結果セットのメタデータを取得できます、行をフェッチしようとしてでき、結果セットに対して、カーソルを閉じる必要があります。  
  
 データ ソースから行を取得して、アプリケーションに戻すプロセスと呼ばれます*フェッチ*します。 このセクションでは、そのプロセスの基本的なパーツについて説明します。 スクロール可能なカーソルは、ブロックなどのより高度なトピックについては、次を参照してください。[ブロック カーソル](../../../odbc/reference/develop-app/block-cursors.md)と[スクロール可能なカーソル](../../../odbc/reference/develop-app/scrollable-cursors.md)します。 更新方法の詳細については、削除、および行の挿入を参照してください[更新データの概要](../../../odbc/reference/develop-app/updating-data-overview.md)します。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [結果セットは作成されましたか?](../../../odbc/reference/develop-app/was-a-result-set-created.md)  
  
-   [結果セットのメタデータ](../../../odbc/reference/develop-app/result-set-metadata.md)  
  
-   [バインディング列](../../../odbc/reference/develop-app/binding-columns.md)  
  
-   [データのフェッチ](../../../odbc/reference/develop-app/fetching-data.md)  
  
-   [カーソルを閉じる](../../../odbc/reference/develop-app/closing-the-cursor.md)
