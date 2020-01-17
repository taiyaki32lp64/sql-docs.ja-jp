---
title: 列のデータの長さ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- column data [ODBC]
- length of column data [ODBC]
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: c762c881-ebe0-4eac-84d5-f30281fc3eca
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8d2998eace4772624a1e6590ab2541577147f5c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041611"
---
# <a name="length-of-column-data"></a>列データの長さ
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新しい開発作業でこの機能を使用しないようにして、現在この機能を使用しているアプリケーションの変更を検討してください。 ドライバーのカーソル機能を使用することをお勧めします。  
  
 カーソル ライブラリのキャッシュを使用して結果セットにバインドされた各長さ/インジケーター バッファーでバッファーを作成する**SQLBindCol**します。 これらのバッファーで値を使用して構築を**場所**エミュレート位置指定の update または delete ステートメントの句。 位置指定の update ステートメントを実行すると、データ ソースからデータをフェッチするときは、これらのバッファー行セットのバッファーからを更新します。  
  
 データ バッファーの C 型が SQL_C_CHAR または SQL_C_BINARY、および長さ/インジケーター値は、SQL_NTS、長さ/インジケーター バッファーのデータの文字列の長さが設定されます。  
  
> [!NOTE]  
>  カーソル ライブラリが列のキャッシュを更新していない場合は **StrLen_or_IndPtr* SQL_DATA_AT_EXEC または SQL_LEN_DATA_AT_EXEC マクロの結果、対応する行セットのバッファーでは。
