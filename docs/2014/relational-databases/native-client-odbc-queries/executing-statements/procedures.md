---
title: プロシージャ |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC]
- stored procedures [ODBC], about ODBC stored procedures
- ODBC applications, statements
- statements [ODBC], stored procedures
- ODBC applications, stored procedures
ms.assetid: c64d5f3a-376b-48ef-84f3-b6148ac8600a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d030d4fb12ce9217bbdb88f501a0b0674c5a5828
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68206751"
---
# <a name="procedures"></a>手順
  ストアド プロシージャは、1 つ以上の [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントを含むプリコンパイルされた実行可能オブジェクトです。 ストアド プロシージャは、入力パラメーターと出力パラメーターを使用でき、整数のリターン コードを出力することもできます。 アプリケーションは、カタログ関数を使用することで、使用可能なストアド プロシージャを列挙できます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を対象とする ODBC アプリケーションからストアド プロシージャを呼び出す場合、直接実行だけを使用する必要があります。 以前のバージョンに接続されているときに[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーの実装[SQLPrepare 関数](https://go.microsoft.com/fwlink/?LinkId=59360)、一時ストアド プロシージャを作成しと呼ばれるで**SQLExecute**. 追加オーバーヘッドが増加**SQLPrepare**呼び出し対象のストアド プロシージャではなく、ターゲットを実行するストアド プロシージャを直接だけ一時ストアド プロシージャを作成します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスに接続している場合でも、呼び出しの準備には、ネットワーク経由のやり取りが増え、ストアド プロシージャ実行プランを呼び出すだけの実行プランの構築が必要になります。  
  
 ODBC アプリケーションでは、ストアド プロシージャの実行時に ODBC CALL 構文を使用する必要があります。 ドライバーは、ODBC CALL 構文の使用時に、リモート プロシージャ コールのメカニズムを使用してプロシージャを呼び出すように最適化されます。 これは、[!INCLUDE[tsql](../../../includes/tsql-md.md)] EXECUTE ステートメントをサーバーに送信するときに使用するメカニズムよりも効率的です。  
  
 詳細については、次を参照してください。[ストアド プロシージャを実行している](../../native-client-odbc-stored-procedures/running-stored-procedures.md)します。  
  
## <a name="see-also"></a>参照  
 [ステートメントを実行する&#40;ODBC&#41;](executing-statements-odbc.md)  
  
  
