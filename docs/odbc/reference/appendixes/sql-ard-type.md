---
title: SQL_ARD_TYPE |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], pseudo-type identifiers
- pseudo-type identifiers [ODBC], SQL_ARD_TYPE
- SQL_ARD_TYPE [ODBC]
ms.assetid: 8d87ca10-f955-4284-8689-e9f4cc31e7ae
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 802040851259a8537fabcd3cc0da1afdf9b8dbe0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68057052"
---
# <a name="sqlardtype"></a>SQL_ARD_TYPE
SQL_ARD_TYPE 型識別子を使用してを ARD の SQL_DESC_CONCISE_TYPE フィールドで指定した型のバッファー内のデータがなることを示します。 SQL_ARD_TYPE が入力されて、 *TargetType*への呼び出しの引数**SQLGetData**特定のデータ型と記述子を変更することで、データを変更するアプリケーションが入力バッファーの有効ではなくフィールド。 この値のデータ型を結び付ける、  *\*TargetValuePtr*記述子フィールドをバッファーします。 (SQL_ARD_TYPE への呼び出しが入力されていない**SQLBindCol**または**SQLBindParameter**のため、バインドされたバッファーの種類の SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE フィールドに既に関連付けられている、変更できますいつでもこれらのフィールドのいずれかを変更することによって。)  
  
 既定以外の先頭の有効桁数と秒の有効桁数、interval データ型の値を指定する SQL_ARD_TYPE 型識別子を使用でき、SQL_C_NUMERIC データの有効桁数と小数点の値を入力します。 詳細については、次を参照してください。[先頭既定をオーバーライドすると Interval データ型の秒の有効桁数](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md)と[既定の精度をオーバーライドし、数値データ型の小数点以下桁数](../../../odbc/reference/appendixes/overriding-default-precision-and-scale-for-numeric-data-types.md)、この付録で後述します。
