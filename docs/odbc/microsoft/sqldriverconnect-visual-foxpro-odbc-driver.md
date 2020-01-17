---
title: SQLDriverConnect (Visual FoxPro ODBC ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLDriverConnect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 10492c8f-3a18-4971-9db8-879e878083b9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c6fd8f3be1213a91195cd74a8b723629e2c5833f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053894"
---
# <a name="sqldriverconnect-visual-foxpro-odbc-driver"></a>SQLDriverConnect (Visual FoxPro ODBC ドライバー)
> [!NOTE]  
>  このトピックでには、Visual FoxPro ODBC ドライバー固有の情報が含まれています。 この関数の詳細については、該当するトピックを参照してください。 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)します。  
  
 サポート:[完全]  
  
 ODBC API 準拠:レベル 1  
  
 いずれかになりますが、既存のデータ ソースに接続する、[データベース](../../odbc/microsoft/visual-foxpro-terminology.md)のディレクトリまたは[テーブルを無料](../../odbc/microsoft/visual-foxpro-terminology.md)します。 UID および PWD ODBC 属性キーワードは無視されます。 次の表では、追加のサポートされている属性のキーワードを示します。  
  
|ODBC 属性のキーワード|属性値|  
|----------------------------|---------------------|  
|DSN||  
|UID|Visual FoxPro ODBC ドライバーでは無視されますが、エラーを生成しません。|  
|PWD|Visual FoxPro ODBC ドライバーでは無視されますが、エラーを生成しません。|  
|Driver|Visual FoxPro ODBC ドライバーの場所と名前ドライバー マネージャーによって実装されています。|  
  
|Visual FoxPro ODBC ドライバー属性のキーワード|属性値|  
|-------------------------------------------------|---------------------|  
|BackgroundFetch|"Yes"または"No"|  
|[部単位で印刷]|「コンピューター」またはその他の照合順序。 サポートされている照合順序の一覧は、次を参照してください。 [COLLATE 設定](../../odbc/microsoft/set-collate-command.md)します。|  
|説明||  
|[Exclusive]|"Yes"または"No"|  
|SourceDB|0 個以上完全修飾パスを含むディレクトリ[テーブルを無料](../../odbc/microsoft/visual-foxpro-terminology.md)、またはの絶対パスとファイル名、[データベース](../../odbc/microsoft/visual-foxpro-terminology.md)します。|  
|[SourceType]|"DBC"または"DBF"|  
|バージョン||  
  
 ドライバー マネージャーをデータ ソース名が指定されていない場合については、ユーザー メッセージが表示されます (の設定に応じて、 *fDriverCompletion*引数) し続行します。 詳細については、必要なは、Visual FoxPro ODBC ドライバーはプロンプト ダイアログを表示します。  
  
 詳細については、次を参照してください。 [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md)で、 *ODBC プログラマ リファレンス*します。
