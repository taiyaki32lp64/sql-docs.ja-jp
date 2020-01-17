---
title: 引数値のチェック |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- argument value checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 37a65f8b-83aa-456c-b7cf-500404abb38a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 013c8f80a672ed691e7519b318206c406171cfbc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077115"
---
# <a name="argument-value-checks"></a>引数の値のチェック
ドライバー マネージャーは、次の種類の引数を確認します。 明記されない限り、ドライバー マネージャーは、引数の値でエラーの SQL_ERROR を返します。  
  
-   通常、環境、接続、およびステートメントのハンドルは、null ポインターをすることはできません。 ドライバー マネージャーは、null のハンドルを見つけたときに、SQL_INVALID_HANDLE を返します。  
  
-   など、ポインター引数を必要な*OutputHandlePtr*で**SQLAllocHandle**と*カーソル名*で**SQLSetCursorName**、することはできませんnull ポインター。  
  
-   ドライバー固有の値をサポートしないオプション フラグは、有効な値である必要があります。 たとえば、*操作*で**SQLSetPos** SQL_POSITION、SQL_REFRESH、SQL_UPDATE、SQL_DELETE、または SQL_ADD にする必要があります。  
  
-   ODBC ドライバーでサポートされているのバージョンでは、オプション フラグをサポートする必要があります。 たとえば、*情報の種類*で**SQLGetInfo** SQL_ASYNC_MODE (ODBC 3.0 で導入) にすることはできません、2.0 の ODBC ドライバーを呼び出すときにします。  
  
-   0 より大きいまたはより大きいまたは 0 で、関数によって、列とパラメーターの番号がある必要があります。 ドライバーは、現在の結果セットまたは SQL ステートメントに基づいて、これらの引数値の数の上限を確認する必要があります。  
  
-   長さまたはインジケーターの引数とデータ バッファー長の引数は、適切な値を含める必要があります。 内のテーブル名の長さを指定する引数など**SQLColumns** (*NameLength3*) SQL_NTS または値より大きくなければなりません 0 になります。*BufferLength*で**SQLDescribeCol** 0 以上にする必要があります。 ドライバーは、これらの引数を確認する必要もあります。 たとえば、その可能性があることを確認*NameLength3*がデータ ソース内のテーブル名の最大長未満です。
