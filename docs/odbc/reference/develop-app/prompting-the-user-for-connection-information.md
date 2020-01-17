---
title: 接続情報の入力を求める |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to data source [ODBC], SqlConnect
- connecting to driver [ODBC], prompting user for information
- connecting to driver [ODBC], SQLConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SqlDriverConnect
- SQLConnect function [ODBC], prompting user for connection information
- connecting to data source [ODBC], prompting user for information
- prompting user for connection information [ODBC]
- SQLDriverConnect function [ODBC], prompting user for connection information
ms.assetid: da98e9b9-a4ac-4a9d-bae6-e9252b1fe1e5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7dfc63aaa6f162d382d6d8b3c627ff078c76825c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079063"
---
# <a name="prompting-the-user-for-connection-information"></a>接続情報をユーザーに確認する
アプリケーションで使用する場合**SQLConnect**接続についてユーザーに確認する必要がある、ユーザー名やパスワードなど、行う必要があります自体。 これにより、アプリケーションは「ルック アンド フィール」を制御することが、中には、ドライバー固有のコードを格納するアプリケーションを強制的に可能性があります。 これは、アプリケーションは、ドライバー固有の接続情報をユーザーに確認する必要がある場合に発生します。 これは、汎用的なアプリケーションの場合、アプリケーションが書き込まれるときに存在しないドライバーを含むすべてのドライバーを使用するように設計されて不可能な状況を表示します。  
  
 **SQLDriverConnect**接続情報をユーザーに求めることもできます。 たとえば、前に説明した、カスタム プログラムには、次の接続文字列を渡すこともできます**SQLDriverConnect**:  
  
```  
DSN=XYZ Corp;  
```  
  
 ドライバーは、ユーザー Id と、次の図のようにパスワードの入力を求めるダイアログ ボックスを表示し、可能性があります。  
  
 ![ユーザー Id とパスワードの入力を求めるダイアログ ボックス](../../../odbc/reference/develop-app/media/pr18.gif "pr18")  
  
 ドライバーとの接続情報のプロンプトことができますが、ジェネリックと垂直方向のアプリケーションに特に便利です。 これらのアプリケーションは、ドライバー固有の情報を含めることはできませんし、ドライバーのプロンプトに必要な情報を持つアプリケーションからその情報を保持します。 これは、前の 2 つの例で表示されます。 アプリケーションでは、ドライバーにデータ ソース名のみが渡されるとアプリケーション、ドライバー固有の情報が含まれていませんでしたが特定のドライバーに関連付けられていないためです。 アプリケーションがドライバーに完全な接続文字列が渡された場合は、その文字列を解釈することがドライバーに関連付けられました。  
  
 汎用アプリケーションがさらにこの 1 つの手順を実行しであっても、データ ソースを指定します。 ときに**SQLDriverConnect**次のダイアログ ボックスに、ドライバー マネージャーが表示されます、空の接続文字列を受信します。  
  
 ![データ ソース ダイアログ ボックスをオン](../../../odbc/reference/develop-app/media/ch06a.gif "CH06A")  
  
 ユーザーがデータ ソースを選択した後、ドライバー マネージャーがそのデータ ソースを指定する接続文字列を構築し、ドライバーに渡します。 ドライバーでは、ユーザーに必要なその他の情報を求めることもできます。  
  
 ドライバーが、ユーザーを要求する条件がによって制御される、 *DriverCompletion*フラグは常に確認する、必要に応じて、プロンプト、またはメッセージを表示せずにオプションがあります。 このフラグの詳細については、次を参照してください。、 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)関数の説明。
