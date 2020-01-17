---
title: バッファー |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- input buffers [ODBC]
- length/indicator buffers [ODBC]
- output buffers [ODBC]
- buffers [ODBC], about buffers
- application buffers [ODBC]
- buffers [ODBC]
ms.assetid: 42c5226c-cb40-4d1e-809f-2ea50ce6bd55
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ad13379552e3a5a576b0aa5cc8720ca6ca1688a9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118744"
---
# <a name="buffers"></a>バッファー
バッファーは、任意のアプリケーションとドライバーの間のデータを渡すために使用するアプリケーションのメモリです。 使用すると、たとえば、アプリケーションのバッファーを関連付けることまたは *、バインド*結果セットの列で**SQLBindCol**します。 各の行をフェッチすると、これらのバッファー内の各列のデータが返されます。 *入力バッファー*アプリケーションからドライバーにデータを渡すために使用*出力バッファー*ドライバーからアプリケーションにデータを返すために使用します。  
  
> [!NOTE]  
>  ODBC 関数では、SQL_ERROR が返されます、その関数の出力引数の内容は未定義です。  
  
 この説明で不確定な種類のバッファーで主に自体に関するものです。 これらのバッファーのアドレスがなどの SQLPOINTER、型の引数として表示されます、 *TargetValuePtr*引数**SQLBindCol**します。 ただし、ここでは、説明されているバッファーで使用する引数などのアイテムの一部にも適用されますなど、ドライバーに文字列を渡すために使用する引数、 *TableName*引数**SQLTables**します。  
  
 通常、これらのバッファーはペアになっています。 *データ バッファー*が中に、データ自体を渡すために使用、*長さ/インジケーター バッファー*データ バッファーまたは SQL_NULL_DATA、データが NULL であることを示すなどの特殊な値のデータの長さを渡すために使用します。 データ バッファー内のデータの長さは、データ バッファー自体の長さと異なります。 次の図は、データ バッファーおよび長さ/インジケーター バッファー間の関係を示します。  
  
 ![データ バッファーおよび長さ&#47;インジケーター バッファー](../../../odbc/reference/develop-app/media/pr09.gif "pr09")  
  
 データ バッファーに文字またはバイナリ データなどの可変長データが含まれている場合、長さ/インジケーター バッファーが必要です。 データ バッファーには、整数や日付構造体などの固定長データが含まれている場合、データの長さが既にわかっているので、インジケーターの値を渡すためにのみ長さ/インジケーター バッファーが必要です。 アプリケーションでは、固定長データを含む長さ/インジケーター バッファーを使用する場合、ドライバーは、渡された任意の長さを無視します。  
  
 データ バッファーと含まれるデータの両方の長さは文字ではなくバイト単位で測定されます。 この区別は、バイトと文字の長さは同じであるために、ANSI 文字列を使用するプログラムの重要ではありません。  
  
 アプリケーションは、データ バッファーは、ドライバーの定義済みの記述子フィールド、診断のフィールドまたは属性を表している場合は、ドライバー マネージャーがフィールドまたは属性の値を示す関数の引数の性質に示す必要があります。 アプリケーションはこのフィールドまたは属性値は次のいずれかに設定する関数呼び出しで長の引数を設定します。 (同じはフィールドまたは値に設定関数の引数自体では、引数が指す例外での属性の値を取得する関数の場合は true)。  
  
-   フィールドまたは属性の値を示す関数の引数が文字の文字列へのポインターの場合、*長さ*引数は SQL_NTS または文字列の長さ。  
  
-   アプリケーションの場所、SQL_LEN_BINARY_ATTR の結果のフィールドまたは属性の値を示す関数の引数がバイナリ バッファーへのポインターの場合は、(*長さ*) 内のマクロ、*長さ*引数。 これにより、負の値で、*長さ*引数。  
  
-   フィールドまたは属性の値を示す関数の引数が文字列またはバイナリ文字列以外の値へのポインターの場合、*長さ*SQL_IS_POINTER 値を引数である必要があります。  
  
-   フィールドまたは属性の値を示す関数の引数には、固定長の値が含まれている場合、*長さ*引数に応じて SQL_IS_INTEGER、SQL_IS_UINTEGER、SQL_IS_SMALLINT、または SQL_ISI_USMALLINT は、します。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [遅延バッファー](../../../odbc/reference/develop-app/deferred-buffers.md)  
  
-   [バッファーの割り当てと解放](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)  
  
-   [データ バッファーの使用](../../../odbc/reference/develop-app/using-data-buffers.md)
