---
title: SQLBrowseConnect による接続 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], SQLBrowseConnect
- SQLBrowseConnect function [ODBC], connecting
- connecting to data source [ODBC], SQLBrowseConnect
ms.assetid: 6c2e9f76-b766-48df-b109-246bb05ae45d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 04df089b97bf385925c87a98b3f89cdac3ef21e4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083131"
---
# <a name="connecting-with-sqlbrowseconnect"></a>SQLBrowseConnect による接続
**SQLBrowseConnect**と同様に、 **SQLDriverConnect**、接続文字列を使用します。 使用して、ただし、 **SQLBrowseConnect**アプリケーションが実行時に完全な接続文字列を作成できます。 この方法を使用すると、アプリケーションで次の 2 つのことを行えます。  
  
-   詳細については、それによって「ルック アンド フィール」の制御を保持を要求する独自のダイアログ ボックスを作成します。  
  
-   特定のドライバーが使用できるデータ ソースをシステムから参照できます。これは複数の手順になる場合があります。 たとえば、ユーザーは最初にネットワークを介してサーバーを参照して、サーバーを選択します。次に、そのサーバーを介して、ドライバーがアクセスできるデータベースを参照するといった手順です。  
  
 アプリケーション呼び出し**SQLBrowseConnect**と呼ばれる、接続文字列を渡します、*参照要求の接続文字列、* ドライバーまたはデータ ソースを指定します。 ドライバーと呼ばれる、接続文字列を返します、*結果の接続文字列を参照*キーワード (キーワードは、個別の値のセットを受け入れる) 場合の可能な値を格納していると、わかりやすい名前。 アプリケーションがわかりやすい名前を含むダイアログ ボックスにビルドされ、値のユーザーに求めます。 これらの値から新しい参照の要求の接続文字列を作成し、別の呼び出しをドライバーに返さ**SQLBrowseConnect**します。  
  
 接続文字列が前後に渡されるために、ドライバーは複数のレベルのアプリケーションには古いものが返されるときに、新しい接続文字列を返すことによって参照を提供できます。 アプリケーションを呼び出す初めてなど**SQLBrowseConnect**ドライバーは、サーバー名のユーザー入力を求めるキーワードを返す可能性があります。 アプリケーションでは、サーバー名が返される、ときに、ドライバーは、データベースのユーザー入力を求めるキーワードを返す可能性があります。 アプリケーションには、データベース名が返された後、参照プロセスが完了しています。  
  
 毎回**SQLBrowseConnect**新しい参照の結果の接続文字列を返しますとしてそのリターン コード SQL_NEED_DATA が返されます。 これにより、接続プロセスが完了していないアプリケーション。 まで**SQLBrowseConnect**返します SQL_SUCCESS、接続が必要なデータの状態で、使用できません、他の目的など接続属性を設定します。 アプリケーションが呼び出すことによってプロセスを参照する接続を終了できる**SQLDisconnect**します。  
  
 このセクションには、次のトピックが含まれています。  
  
-   [SQL Server の参照の例](../../../odbc/reference/develop-app/sql-server-browsing-example.md)
