---
title: SQL の型識別子 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], identifiers
- SQL data types [ODBC], identifiers
- type identifiers [ODBC], SQL
- identifiers [ODBC], SQL type
- SQL type identifiers [ODBC]
ms.assetid: 22f6793b-2f43-4281-b35a-28f48e504dd8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: be36bd8efc059c1a4f9b5ddf2cdd7faf32cf7dd4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107449"
---
# <a name="sql-type-identifiers"></a>SQL の型識別子
各データ ソースは、独自の SQL データ型を定義します。 ODBC では、型識別子を定義し、各種類の識別子にマップすることがあります SQL データ型の一般的な特性について説明します。 ドライバー固有の ODBC SQL 型の識別子に基になるデータ ソース内の各データ型をマップする方法になります。  
  
 たとえば、SQL_CHAR は、通常 1 ~ 254 文字の間の固定長文字型列の型識別子です。 これらの特性は、多くの SQL データ ソースにある CHAR データ型に対応します。 したがって、SQL_CHAR に列の型識別子が検出されると、アプリケーション、char 型の列を処理している可能性があります想定できます。 ただし、まだチェックインと仮定すると前に、のコラムのバイトの長さは、1 ~ 254 の文字。たとえば、非 SQL データ ソースのドライバーはどちらもあるために、SQL_CHAR または SQL_LONGVARCHAR の 500 文字の固定長文字型列をマップ可能性がありますと完全に一致します。  
  
 ODBC では、さまざまな種類の SQL 識別子を定義します。 ただし、ドライバーでは、これらの識別子のすべてを使用する必要はありません。 代わりに、基になるデータ ソースでサポートされている SQL データ型を公開する必要がある識別子のみを使用します。 基になるデータ ソースに SQL データ型をサポートしている場合は、どの型識別子のない対応、ドライバーは、追加の型識別子を定義できます。 詳細については、次を参照してください。[ドライバー固有のデータ型、記述子の種類、情報の種類、診断型、および属性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)します。  
  
 SQL の型識別子の詳細については、次を参照してください[C データ型](../../../odbc/reference/appendixes/c-data-types.md)付録 d:。データ型。
