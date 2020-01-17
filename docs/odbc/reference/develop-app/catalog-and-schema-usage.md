---
title: カタログとスキーマの使用状況 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], catalog names
- catalog names [ODBC]
- interoperability of SQL statements [ODBC], schema names
- schema names in SQL statements [ODBC]
ms.assetid: 84f7ef61-1ef1-46f3-9678-b087aa8e8e34
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4e10460df120451502d798376453d69d111051ec
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68064414"
---
# <a name="catalog-and-schema-usage"></a>カタログとスキーマの使用状況
データ ソースが、すべての SQL ステートメント内でのオブジェクト名の識別子としてのカタログとスキーマ名を必ずしもにサポートしません。 データ ソースは、SQL ステートメントの次のクラスの 1 つ以上のカタログとスキーマ名をサポートする場合があります。データ操作言語 (DML) ステートメント、プロシージャの呼び出し、テーブル定義ステートメント、インデックス定義ステートメント、および特権定義ステートメント。 カタログとスキーマ名を使用できる SQL ステートメントのクラスを確認するには、アプリケーションが呼び出す**SQLGetInfo** SQL_CATALOG_USAGE および SQL_SCHEMA_USAGE のオプションを使用します。
