---
title: SQLGetDescField および SQLGetDescRec (カーソル ライブラリ) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetDescField function [ODBC], Cursor Library
- SQLGetDescRec function [ODBC], Cursor Library
ms.assetid: 1a801f22-6fea-48aa-a723-3187a2ad852b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 853a364b61b63d58da93111c75db0d7d723ee49b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68073911"
---
# <a name="sqlgetdescfield-and-sqlgetdescrec-cursor-library"></a>SQLGetDescField および SQLGetDescRec (カーソル ライブラリ)
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新しい開発作業でこの機能を使用しないようにして、現在この機能を使用しているアプリケーションの変更を検討してください。 ドライバーのカーソル機能を使用することをお勧めします。  
  
 このトピックの使用、 **SQLGetDescField**と**SQLGetDescRec**カーソル ライブラリの関数。 これらの関数については、次を参照してください。 [SQLGetDescField 関数](../../../odbc/reference/syntax/sqlgetdescfield-function.md)と[SQLGetDescRec 関数](../../../odbc/reference/syntax/sqlgetdescrec-function.md)します。  
  
 カーソル ライブラリを実行します**SQLGetDescRec**ブックマーク列のメタデータを返します。 カーソル ライブラリを実行します**SQLGetDescField**によって返されるのと同じフィールドを返す**SQLGetDescRec**は、SQL_DESC_NAME、SQL_DESC_TYPE、SQL_DESC_DATETIME_INTERVAL_CODE SQL_DESC_OCTET_長さ、SQL_DESC_PRECISION、SQL_DESC_SCALE、および SQL_DESC_NULLABLE します。 一貫性を保つのため**SQLGetDescField**も SQL_DESC_UNNAMED を返します。  
  
 カーソル ライブラリを実行します**SQLGetDescField**ブックマーク列をバインドするために設定されているフィールドが、次の値を返すに呼び出されます。SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、SQL_DESC_OCTET_LENGTH_PTR、および SQL_DESC_LENGTH します。  
  
 カーソル ライブラリを実行します**SQLGetDescField** SQL_DESC_BIND_OFFSET_PTR、SQL_DESC_BIND_TYPE、SQL_DESC_ROW_ARRAY_SIZE、または SQL_DESC_ROW_STATUS_PTR フィールドの値を返すに呼び出されます。 これらのフィールドは、ブックマークの行だけでなく、任意の行に対して返されます。  
  
 アプリケーションを呼び出す場合**SQLGetDescField**カーソル ライブラリは、前に説明したもの以外の任意のフィールドの値を取得、ドライバーへの呼び出しを渡します。
