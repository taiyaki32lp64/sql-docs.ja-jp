---
title: SQLExtendedFetch (Visual FoxPro ODBC ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLExtendedFetch function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b28af112-fb47-4143-b11e-3b743b2ae1b8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d58d7885eed1a8ed0611470f29cb24e8072afcb9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053802"
---
# <a name="sqlextendedfetch-visual-foxpro-odbc-driver"></a>SQLExtendedFetch (Visual FoxPro ODBC ドライバー)
> [!NOTE]  
>  このトピックでには、Visual FoxPro ODBC ドライバー固有の情報が含まれています。 この関数の詳細については、該当するトピックを参照してください。 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)します。  
  
 サポート:[完全]  
  
 ODBC API 準拠:レベル 2  
  
 ような[SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md)が各列の配列を使用して複数の行を返します。 結果セットは前方スクロールし、旧バージョンとのスクロール可能な静的、順方向専用カーソルが定義されている場合に行んだことができます。  
  
 既定では、Visual FoxPro ODBC ドライバーでは、FoxPro テーブルで削除済みとしてマークされている行は返されません。 結果セットのカーソルでは、削除対象としてマークが、テーブルから削除されていない行は含まれません。 使用してこの動作を変更することができます、[削除設定](../../odbc/microsoft/set-deleted-command.md)コマンド。  
  
 詳細については、次を参照してください。 [SQLExtendedFetch](../../odbc/reference/syntax/sqlextendedfetch-function.md)で、 *ODBC プログラマ リファレンス*します。
