---
title: 転送オクテット長 |Microsoft Docs
ms.custom: ''
ms.date: 10/28/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transfer octet length of data types [ODBC]
- size of data types [ODBC]
- SQL data types [ODBC], column characteristics
- data types [ODBC], transfer octet length
ms.assetid: 9fdc9762-e203-4cff-9212-54f450bf18d9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a92a9ead66736ff2b72813d6d4cbec5acfcda4fe
ms.sourcegitcommit: 82b70c39550402a2b0b327db32bf5ecf88b50d3c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2019
ms.locfileid: "73032970"
---
# <a name="transfer-octet-length"></a>転送オクテット長
列の転送オクテット長は、データが既定の C データ型に転送されるときにアプリケーションに返される最大バイト数です。 文字データの場合、転送オクテット長には null 終端文字のスペースは含まれません。 列の転送オクテット長は、データソースにデータを格納するために必要なバイト数とは異なる場合があります。  
  
 次の表に、各 ODBC SQL データ型に対して定義されている転送オクテット長を示します。  
  
|SQL 型識別子|[データ型]|  
|-------------------------|------------|  
|すべての文字型 [a]|定義された、または列の最大長 (変数型の場合) (バイト単位)。 これは、記述子フィールド SQL_DESC_OCTET_LENGTH と同じ値です。|  
|SQL_DECIMAL<br />SQL_NUMERIC|文字セットが ANSI である場合は、このデータの文字表現を保持するために必要なバイト数。文字セットが UNICODE の場合は、この数を2倍にします。 データが文字列として返され、数字、符号、および小数点に文字が必要なため、これは最大桁数に2を加算した値になります。 たとえば、NUMERIC (10, 3) として定義された列の転送の長さは12です。|  
|SQL_TINYINT|@shouldalert|  
|SQL_SMALLINT|2|  
|SQL_INTEGER|4|  
|SQL_BIGINT| 8 |  
|SQL_REAL|4|  
|SQL_FLOAT|8|  
|SQL_DOUBLE|8|  
|SQL_BIT|@shouldalert|  
|すべてのバイナリ型 [a]|定義された (固定型の場合) または最大値 (変数型の場合) を保持するために必要なバイト数。|  
|SQL_TYPE_DATE<br />SQL_TYPE_TIME|6 (SQL_DATE_STRUCT または SQL_TIME_STRUCT 構造体のサイズ)。|  
|SQL_TYPE_TIMESTAMP|16 (SQL_TIMESTAMP_STRUCT 構造体のサイズ)。|  
|すべての interval データ型|34 (間隔の構造体のサイズ)。|  
|SQL_GUID|16 (GUID 構造体のサイズ)。|  
| &nbsp; | &nbsp; |

 [a] 変数の型の列またはパラメーターの長さをドライバーが判別できない場合は、SQL_NO_TOTAL が返されます。
