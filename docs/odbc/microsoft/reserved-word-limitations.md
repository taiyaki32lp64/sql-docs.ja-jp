---
title: 予約済みキーワードの制限事項 |Microsoft Docs
ms.custom: ''
ms.date: 05/01/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ed42f083-c9e8-4ee4-9d64-d879bf955c78
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c884d8594c3c4511bed0e24f9b3dd43092176b4e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67988026"
---
# <a name="reserved-keyword-limitations"></a>予約済みキーワードの制限事項

SQL テーブルまたは関連するオブジェクト識別子として任意の ODBC の予約済みキーワードを使用しないでください。 奇数のケースでは、予約済みキーワードを識別子として使用する必要がありますが発生した場合のペアを使って、識別子を囲む必要があります*バッククォート*(')。 別の名前*バックティック*は*後ろ向き引用符*します。

予約済みキーワードの制限は、予約済みキーワードの任意の短い形式にも適用されます。

ODBC の予約済みキーワードの一覧で提供されています。

- [ODBC の予約済みキーワード](https://docs.microsoft.com/sql/odbc/reference/appendixes/reserved-keywords)します。

- *ODBC プログラマ リファレンス ガイド*を参照してください[付録 c:SQL 文法](https://docs.microsoft.com/sql/odbc/reference/appendixes/appendix-c-sql-grammar)します。

