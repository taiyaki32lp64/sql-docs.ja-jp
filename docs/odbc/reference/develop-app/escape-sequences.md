---
title: エスケープ シーケンス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- escape sequences [ODBC], determining if supported
- interoperability of SQL statements [ODBC], escape sequences
ms.assetid: 5913abfa-d280-43e4-a2f1-05a924388bf9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d73282cde4d0598d7e6a35ac6273935626b96969
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001373"
---
# <a name="escape-sequences"></a>エスケープ シーケンス
ODBC 標準の文法、日付、時刻、タイムスタンプ、および datetime interval のリテラルのスカラー関数の呼び出しを含むエスケープ シーケンスを定義する**など**述語のエスケープ文字、外部結合、およびプロシージャの呼び出し。 相互運用可能なアプリケーションでは、可能であれば、これらのシーケンスを使用する必要があります。  
  
 アプリケーションを呼び出すドライバーが、日付、時刻、タイムスタンプ、または datetime interval のリテラルのエスケープ シーケンスをサポートしているかを判断する**SQLGetTypeInfo**します。 データ ソースは、日付、時刻、タイムスタンプ、または datetime 間隔のデータ型をサポートする場合、対応するエスケープ シーケンスもサポートする必要があります。 アプリケーションを呼び出す他のエスケープ シーケンスはサポートされているかどうかを判断する**SQLGetInfo**します。  
  
 詳細については、次を参照してください。 [odbc エスケープ シーケンス](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)、このセクションで後述します。
