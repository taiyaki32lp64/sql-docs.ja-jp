---
title: SQLTransact (Visual FoxPro ODBC ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLTransact function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 92cf86c0-f7a8-44d7-b59f-a1342677440b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e554a8669b6e6e95e234a5b939477a8bb2f7b8cc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948866"
---
# <a name="sqltransact-visual-foxpro-odbc-driver"></a>SQLTransact (Visual FoxPro ODBC ドライバー)
> [!NOTE]  
>  このトピックでには、Visual FoxPro ODBC ドライバー固有の情報が含まれています。 この関数の詳細については、該当するトピックを参照してください。 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)します。  
  
 サポート:[完全]  
  
 ODBC API 準拠:コア レベル  
  
 すべてのステートメント ハンドルのすべてのアクティブな操作をコミットまたはロールバック操作の要求 (*hstmt*s) 接続または、環境ハンドルに関連付けられているすべての接続に関連付けられた*henv*します。 **SQLTransact**にあるデータ ソースに対してのみ機能[データベース](../../odbc/microsoft/visual-foxpro-terminology.md)します。  
  
 トランザクションはアクティブなまま手動モードの場合、コミットに失敗した場合トランザクションをロールバックまたはコミット操作を再試行することができます。 自動トランザクション モードのときに、コミット操作が失敗した場合、トランザクションは自動的にロールバックします。トランザクションを非アクティブにすることはできません。  
  
 詳細については、次を参照してください。 [SQLTransact](../../odbc/reference/syntax/sqltransact-function.md)で、 *ODBC プログラマ リファレンス*します。
