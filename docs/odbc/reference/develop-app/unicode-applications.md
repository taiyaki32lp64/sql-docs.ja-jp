---
title: Unicode アプリケーション |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], compiling as Unicode application
- Unicode [ODBC], functions
- compiling Unicode applications [ODBC]
- functions [ODBC], Unicode functions
ms.assetid: 7986c623-2792-4e77-bfee-c86cbf84f08d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 32b4125d0ecb1f15fab00119a8ef4ed361b6db72
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68087737"
---
# <a name="unicode-applications"></a>Unicode アプリケーション
2 つの方法のいずれかで Unicode アプリケーションとしてアプリケーションを再コンパイルすることができます。  
  
-   Unicode を含む **#define** Sqlucode.h ヘッダー ファイルをアプリケーション内に含まれています。  
  
-   コンパイラの Unicode のオプションを使用してアプリケーションをコンパイルします。 (このオプションになります異なるコンパイラによって異なります。)  
  
 Unicode アプリケーションに、ANSI アプリケーションを変換するには、格納、および Unicode データを渡すアプリケーションを作成します。 さらに、バイト数を使用する SQLPOINTER 引数をサポートする関数への呼び出しを変換する必要があります。  
  
 ドライバー マネージャーが Unicode アプリケーションとしてアプリケーションを認識し、(、でUnicode関数の関数呼び出しに変換します(サフィックス)のないODBCAPI関数を呼び出している場合のUnicodeアプリケーションとしてアプリケーションのコンパイル後*W*サフィックス)、基になるドライバーは、Unicode をサポートしている場合。 ANSI アプリケーションが、関数のサフィックスが付いていない呼び出しを行うと、ドライバー マネージャーに変換 ANSI 基になるドライバーには、ANSI がサポートしている場合。 アプリケーションとドライバーの両方と同じ文字エンコーディングをサポートして、ドライバー マネージャーを使用してドライバー (ANSI アプリケーションの特定の例外) をへの呼び出しを渡します。  
  
 アプリケーションは、Unicode 関数の両方を呼び出すことができます (で、 *W*サフィックス) および ANSI 関数 (有無にかかわらず、 *A*サフィックス)。 Unicode と ANSI 関数の呼び出しを混在させることができます。 カーソル ライブラリを使用する場合は、ただし、Unicode と ANSI の関数呼び出しを混在させることはできません。 カーソル ライブラリは、Unicode または ANSI を混在させないようにします。  
  
 Unicode アプリケーションまたは ANSI アプリケーションとしてにコンパイルできるように、アプリケーションを作成できます。 ここでは、SQL_C_TCHAR として文字データ型を宣言することができます。 これは、アプリケーションが Unicode アプリケーションとしてコンパイルされるまたは ANSI アプリケーションとしてコンパイルされている場合は、SQL_C_CHAR を挿入する場合は、SQL_C_WCHAR を挿入するマクロです。 Length 引数のサイズを変更する (文字列データ型) のため、アプリケーション プログラマをその引数としての SQLPOINTER を受け取る関数に注意してくださいにある必要があります、アプリケーションは、ANSI または Unicode かどうかによって異なります。  
  
 関数は、3 つの方法のいずれかで呼び出すことができます: Unicode 専用の関数呼び出しと (で、 *W*サフィックス)、ANSI 専用の関数呼び出しとして (で、 *A*サフィックス)、またはサフィックスなしの ODBC 関数呼び出しとして。 関数の 3 つのフォームへの引数は同じです。 SQLCHAR 関数のみ\*引数または文字列の指す SQLPOINTER 引数が Unicode と ANSI のフォームが必要です。 などの文字型として宣言できる引数を持つ関数の**SQLBindCol**または**SQLGetData** (これがない Unicode と ANSI 形式)、引数は、Unicode 型として宣言できますANSI 型、または C の場合、SQL_C_TCHAR マクロの引数を入力します。 詳細については、次を参照してください。 [Unicode データ](../../../odbc/reference/develop-app/unicode-data.md)します。  
  
 連動するように使用できる Unicode ドライバーがない場合でも、Unicode アプリケーションとしてアプリケーションを作成できます。 ドライバー マネージャーは、Unicode 関数とデータ型を ANSI にマップされます。 Unicode から ANSI へのマッピングにいくつかの制限があります。 Unicode アプリケーションで動作するための Unicode ドライバーの存在を使用して、パフォーマンスを向上させると、Unicode ANSI へのマッピングからに固有の制限が削除されます。
