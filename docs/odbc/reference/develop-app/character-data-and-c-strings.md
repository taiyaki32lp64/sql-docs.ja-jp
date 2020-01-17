---
title: 文字データや C 文字列 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data buffers [ODBC], length
- data buffers [ODBC], character data
- buffers [ODBC], C strings
- buffers [ODBC], character data
- character data and buffers [ODBC]
- length of data buffers [ODBC]
- data buffers [ODBC], C strings
- buffers [ODBC], length
- C strings and buffers [ODBC]
ms.assetid: 3a141cb4-229d-4027-9349-615cb2995e36
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ed99ab72e3d5112588a0b1c93df34b01aff7acdd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68044921"
---
# <a name="character-data-and-c-strings"></a>文字データと C 文字列
(列名、動的パラメーターは、文字列の属性値など) の可変長文字データを参照する入力パラメーターは、関連付けられている長さパラメーターを指定します。 アプリケーションを終了させる場合は C で一般に、null 文字の文字列 (null 終端文字を含まない) 文字列のバイト単位の長さまたは SQL_NTS (Null-Terminated 文字列) のいずれかの引数として提供します。 負ではない length 引数には、関連付けられている文字列の実際の長さを指定します。 Length 引数には、NULL 値とは異なりますが、長さ 0 の文字列を指定する 0 になります。 SQL_NTS 負の値は、null 終端文字を検索する文字列の長さを判別するのには、ドライバーに指示します。  
  
 文字データは、ドライバーからアプリケーションに返されると、ドライバーする必要があります常に null で終了します。 これにより、アプリケーションは、文字列または文字配列としてデータを処理するかどうかを選択します。 アプリケーション バッファーをすべての文字データを返すのに十分な大きさでない場合、ドライバーの null 終端文字によって必要なバイト数を引いたバッファーのバイトの長さに切り捨てます、切り捨てられたデータを null で終端しますに格納しますバッファー。 そのため、アプリケーションが文字データの取得に使用されるバッファーに null 終端文字のため余分なスペースを常に配置する必要があります。 たとえば、50 文字のデータを取得する必要 51 バイト バッファー。  
  
 特別な注意は、アプリケーションと送信または使用して、パーツで時間の長い文字データを取得するときに、ドライバーの両方で実行する必要があります**SQLPutData**または**SQLGetData**します。 データが一連の null で終わる文字列として渡された場合、データが再構築する前にこれらの文字列に null 終端文字を除去する必要があります。  
  
 C 文字列の文字データや ODBC プログラマの数値を混乱させています。 ODBC 関数を定義するときに C 言語の使用の成果物は、この問題が発生します。 ODBC ドライバーまたはアプリケーションの別の言語を使用している場合は、ODBC は言語に依存しない - このような混乱が発生する可能性が低くに注意してください。  
  
 文字データを保持するために C 文字列を使用している場合、null 終了文字は、データの一部であるとは見なされません、バイト長の一部としてはカウントされません。 たとえば、文字データ"ABC"は"ABC\0"C 文字列または文字配列 {'A'、'B'、'C'} として保持できます。 データのバイトの長さは、文字列または文字配列として扱われるかどうか、3、です。  
  
 アプリケーションとドライバー、文字データを保持するためによく C 文字列 (文字の null で終わる配列) を使用して、ですが、これを行う必要はありません。 C では、文字データを個別に渡された長さ/インジケーター バッファーのバイト長と (null 終了) を持たない文字の配列として処理こともできます。  
  
 Null で終わる配列に文字データを保持できるバイト長が個別に渡されるためは、null 文字を文字データに組み込むことができます。 ただし、ODBC 関数の動作ここではない定義されに、ドライバー固有かどうかをドライバーこれを正しく処理します。 そのため、相互運用可能なアプリケーションは、バイナリ データとして埋め込まれた null 文字を含むことのできる文字データを常に処理する必要があります。
