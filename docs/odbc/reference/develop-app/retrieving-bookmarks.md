---
title: ブックマークの取得 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- retrieving bookmarks [ODBC]
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
ms.assetid: a34c8f09-b786-4835-a44b-b7294c970aff
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f18b87adf31f19d2a93bb3af3e14c265ae3940af
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020573"
---
# <a name="retrieving-bookmarks"></a>ブックマークの取得
アプリケーションでブックマークを使用する場合は、SQL_ATTR_USE_BOOKMARKS ステートメント属性を準備またはステートメントを実行する前に SQL_UB_VARIABLE に設定があります。 これは、機能は、それらのビルドとメンテナンス アプリケーションを適切に行うことができる場合にのみ、ブックマークを有効にするため、ブックマークは、コストのかかる操作を指定できますが使用するため必要です。  
  
 ブックマークは、結果セットの列 0 として返されます。 アプリケーションが取得できる 3 つの方法があります。  
  
-   結果セットの列 0 をバインドします。 **SQLFetch**または**SQLFetchScroll**他のデータと共に、行セット内の各行には、列がバインドされているブックマークを返します。  
  
-   呼び出す**SQLSetPos**行セット内の行に配置し、呼び出す**SQLGetData**列 0 です。 呼び出す機能を常にサポートする必要があります、ドライバーは、ブックマークをサポートする場合**SQLGetData**列 0 を呼び出すアプリケーションを許可しない場合でも**SQLGetData**の最後のバインドする前に他の列列です。  
  
-   呼び出す**SQLBulkOperations**で、*操作*引数 SQL_ADD に設定し、バインド列 0 です。 カーソルは、行を挿入し、バインドされたバッファー内の行のブックマークを返します。
