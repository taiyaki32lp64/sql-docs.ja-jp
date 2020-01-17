---
title: リストの引数の値 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], value list
- value list arguments [ODBC]
ms.assetid: 863837be-603b-4c7a-8b96-b71014037ee5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 646d2724489140080a673f31e22429cc7ca39d4e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68022098"
---
# <a name="value-list-arguments"></a>値リストの引数
リスト引数の値は、照合に使用する値のコンマ区切りの一覧で構成されます。 ODBC カタログ関数の 1 つの値リストの引数がある: *TableType*引数**SQLTables**します。 設定*TableType* null ポインターには、場合と同じ値の一覧のすべての可能なメンバーを列挙する、SQL_ALL_TABLE_TYPES に設定されています。 この引数は、SQL_ATTR_METADATA_ID ステートメント属性の影響を受けません。 詳細については、次を参照してください。、 [SQLTables](../../../odbc/reference/syntax/sqltables-function.md)関数の説明。
