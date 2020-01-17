---
title: ステートメントのオプション |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- custom statement options [ODBC]
- statement options [ODBC]
- ODBC driver for Oracle [ODBC], statement options
ms.assetid: cd73b769-c8b5-43e0-9f80-b3011b7a6162
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3bf99aace8b058e429898846466294cc42612070
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948833"
---
# <a name="statement-options"></a>ステートメントのオプション
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle によって提供される ODBC ドライバーを使用します。  
  
 これらのオプションは、アプリケーション内の特定の実行ステートメントのカスタマイズを許可します。  
  
|ステートメント オプション|注|  
|----------------------|-----------|  
|SQL_BIND_TYPE|2,147, 483,647 バイトまたは使用可能なメモリを超えることはできません。|  
|SQL_CONCURRENCY|使用できる値は、次を参照してください。、[カーソルの種類および同時実行の組み合わせ](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)します。|  
|SQL_CURSOR_TYPE|ドライバーでは、SQL_CURSOR_DYNAMIC は許可されません。 参照してください[SQLSetScrollOptions](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md)詳細についてはします。 使用できる値は、次を参照してください。、[カーソルの種類および同時実行の組み合わせ](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)します。|  
|SQL_GET_BOOKMARK|現在のレコード数のブックマークは、32 ビット整数値を返します。 Get だけです。設定できません。|  
|SQL_KEYSET_SIZE|0 に設定できます。|  
|SQL_MAX_ROWS|結果から返される行の最大数を設定します。|  
|SQL_ROW_NUMBER|結果セット内の現在の行の位置を指定する 32 ビット整数を返します。 Get だけです。設定できません。|  
|SQL_ROWSET_SIZE|4,294,967,296 行を超えることはできません。ただし、要求を処理するために、コンピューターに十分な仮想メモリが必要です。|  
|SQL_USE_BOOKMARKS|SQL_UB_ON に SQL_USE_BOOKMARKS の設定をサポートし、固定長のブックマークを公開します。|
