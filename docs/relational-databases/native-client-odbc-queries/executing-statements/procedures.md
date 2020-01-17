---
title: プロシージャ |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 66db10c8ac64fee4e6e9ccbc405ab5b804adb32a
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73779525"
---
# <a name="procedures"></a>手順
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ストアド プロシージャは、1 つ以上の [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントを含むプリコンパイルされた実行可能オブジェクトです。 ストアド プロシージャは、入力パラメーターと出力パラメーターを使用でき、整数のリターン コードを出力することもできます。 アプリケーションは、カタログ関数を使用することで、使用可能なストアド プロシージャを列挙できます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を対象とする ODBC アプリケーションからストアド プロシージャを呼び出す場合、直接実行だけを使用する必要があります。 以前のバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]に接続されている場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは、 [SQLPrepare 関数](https://go.microsoft.com/fwlink/?LinkId=59360)を実装します。このストアドプロシージャは、 **sqlexecute**で呼び出されます。 **SQLPrepare**によって、対象のストアドプロシージャを呼び出すだけでなく、対象のストアドプロシージャを直接実行する一時ストアドプロシージャを作成することにより、オーバーヘッドが増加します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスに接続している場合でも、呼び出しの準備には、ネットワーク経由のやり取りが増え、ストアド プロシージャ実行プランを呼び出すだけの実行プランの構築が必要になります。  
  
 ODBC アプリケーションでは、ストアド プロシージャの実行時に ODBC CALL 構文を使用する必要があります。 ドライバーは、ODBC CALL 構文の使用時に、リモート プロシージャ コールのメカニズムを使用してプロシージャを呼び出すように最適化されます。 これは、[!INCLUDE[tsql](../../../includes/tsql-md.md)] EXECUTE ステートメントをサーバーに送信するときに使用するメカニズムよりも効率的です。  
  
 詳細については、「[ストアドプロシージャの実行](../../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ステートメント&#40;の実行 ODBC&#41;](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
  
