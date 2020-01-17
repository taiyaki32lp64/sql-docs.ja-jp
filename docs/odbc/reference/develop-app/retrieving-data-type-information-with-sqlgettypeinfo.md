---
title: SQLGetTypeInfo による情報を入力するデータを取得する |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL data types [ODBC], identifiers
- SQLGetTypeInfo function [ODBC], retrieving data type information
- retrieving data type information [ODBC]
- type identifiers [ODBC], SQL
- identifiers [ODBC], SQL type
- SQL type identifiers [ODBC]
ms.assetid: d4f8b152-ab9e-4d05-a720-d10a08a6df81
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c4f336a7ebfaf5e76ac464944900231c452809f7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020547"
---
# <a name="retrieving-data-type-information-with-sqlgettypeinfo"></a>SQLGetTypeInfo によるデータ型情報の取得
ODBC 関数は、基になる SQL データ型から ODBC 型識別子へのマッピングは概数であるため (**SQLGetTypeInfo**) を介して、ドライバーは完全にデータ ソース内の各 SQL データ型について説明します。 この関数は、各行は、名前、型識別子、精度、スケール、および null 値許容属性などの 1 つのデータ型の特性を記述します。 結果セットを返します。  
  
 一般に、この情報は、ユーザーの作成し、テーブルの変更を許可する汎用アプリケーションによって使用されます。 このようなアプリケーション呼び出し**SQLGetTypeInfo**データ型情報の取得をユーザーの一部またはすべてを提供します。 このようなアプリケーションは、2 つのことを意識する必要があります。  
  
-   1 つ以上の SQL データ型は、使用するデータの種類を決定する困難になりますが、1 つの型の識別子にマップできます。 これを解決するには、結果セットが順序付けにまず型識別子を使用して、型識別子の定義に近さの程度によって 2 つ目です。 さらに、データ ソース定義のデータ型は、ユーザー定義データ型に優先します。 たとえば、データ ソースが、カウンターが自動的にインクリメントすることを除いて同じである整数とカウンターのデータ型を定義します。 ユーザー定義型 WHOLENUM が整数のシノニムにもあるとします。 これらの型は、SQL_INTEGER にマップされます。 **SQLGetTypeInfo**結果セット、WHOLENUM 続く整数が最初に、表示され、カウンターします。 WHOLENUM は、ユーザー定義ですが、カウンターの前より密接に一致するため、SQL_INTEGER の定義 id を入力するために、整数の後に表示されます。  
  
-   ODBC で使用するためのデータ型の名前を定義しません**CREATE TABLE**と**ALTER TABLE**ステートメント。 アプリケーションがによって返される結果セットの TYPE_NAME 列で返される名前を使用する代わりに、 **SQLGetTypeInfo**します。 この理由は、ことが、SQL のほとんどが一定の Dbms の間で、データ型の名前によって異なります大幅です。 SQL ステートメントを解析し、標準的なデータ型の名前を DBMS 固有のデータ型の名前に置き換えますドライバーではなく、ODBC には、最初に、DBMS 固有の名前を使用するアプリケーションが必要です。  
  
 なお**SQLGetTypeInfo**必ずしもに記載されていないすべてのデータ型が、アプリケーションが発生することができます。 具体的には、結果セットには、直接ではなく、データ ソースでサポートされるデータ型が含まれます。 たとえば、odbc カタログ関数によって返される結果セット内の列のデータ型が定義されているし、これらのデータ型は、データ ソースでサポートされていない可能性があります。 結果セット内のデータ型の特性を判断するには、アプリケーションが呼び出す**SQLColAttribute**します。
