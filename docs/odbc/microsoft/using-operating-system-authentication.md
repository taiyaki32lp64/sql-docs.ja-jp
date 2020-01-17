---
title: オペレーティング システムの認証を使用して |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], authentication
- authentication [ODBC]
ms.assetid: 613daef7-3171-42d0-b7e3-3879280f864d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 56f09a82c2e67ee74ce140f4742bfaf0bcce247f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088125"
---
# <a name="using-operating-system-authentication"></a>オペレーティング システムの認証の使用
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle によって提供される ODBC ドライバーを使用します。  
  
 Oracle オペレーティング システムの認証は、データベース アカウントへのアクセスを制御する、基になるオペレーティング システムに依存します。 この種類のログインを使用する場合、ユーザーはパスワードを入力しない必要があります。  
  
 この機能を利用するには指定ユーザー ID として「/」を使用して次の Api 接続のいずれかを接続するときにパスワードを指定しないでください。[SQLBrowseConnect](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md)、 [SQLConnect](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md)、または[SQLDriverConnect](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md)します。  
  
 Oracle データベースを使用して、SQL * Net の認証サービスにログオンしたユーザーを認証します。 このサービスは、ユーザーが SQLPlus; から Oracle にログインしている場合に適していますただし、ログインしているユーザーは、インターネット インフォメーション サービスなどのサービスが、認証は失敗します。 これは、SQL の既知の制限事項\*Net 認証し、次のエラーを生成します:"[Microsoft] [Oracle 用 ODBC driver] [Oracle] の ORA 12641。TNS:authentication サービスを初期化できませんでした。"  
  
 この問題を修正するには、Sqlnet.ora ファイルを編集します。 この構成ファイルは通常、Oracle ホーム ディレクトリの Network\Admin サブディレクトリに格納されます。 Sqlnet.ora には、次の行を追加します。  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```
