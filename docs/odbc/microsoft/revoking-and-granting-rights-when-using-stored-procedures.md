---
title: ストアド プロシージャの使用時に権限の付与と取り消し |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 24070039-03ab-4623-a681-6308802eb399
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 91fcf722554fe1840465329e707c792a6bbab6db
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67987953"
---
# <a name="revoking-and-granting-rights-when-using-stored-procedures"></a>ストアド プロシージャ使用時の権限の取り消しと付与
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle によって提供される ODBC ドライバーを使用します。  
  
 Microsoft ODBC Driver for Oracle では、ユーザー権限の付与し、ストアド プロシージャがアクセスするテーブルで、取り消すときに、次のエラー メッセージが返されます。  
  
 SQL_ERROR = 1  
  
 szErrorMsg="[Microsoft][ODBC driver for Oracle]Wrong number of parameters"  
  
 szErrorMsg="[Microsoft][ODBC driver for Oracle]Syntax error or access violation"  
  
 Oracle OCI 関数 Odessp() への呼び出しがこのシナリオでは失敗が既定のパラメーターを実装するために必要です。 基になるテーブルのアクセス許可を変更した後に、もう一度実行する前に、ストアド プロシージャが再コンパイルする必要があります。
