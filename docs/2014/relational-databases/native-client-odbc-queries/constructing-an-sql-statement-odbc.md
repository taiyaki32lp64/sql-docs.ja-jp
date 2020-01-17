---
title: SQL ステートメント (ODBC) の構築 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, statements
- statements [ODBC], constructing
- ODBC applications, statements
ms.assetid: 0acc71e2-8004-4dd8-8592-05c022bdd692
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fa955f31d26c87b39585ddead6bc5899a9e00679
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68206781"
---
# <a name="constructing-an-sql-statement-odbc"></a>SQL ステートメントの構築 (ODBC)
  ODBC アプリケーションでは、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行することで、ほぼすべてのデータベース アクセスを行います。 これらのステートメントの形式は、アプリケーションの要件によって異なります。 SQL ステートメントは、次の方法で構築できます。  
  
-   ハードコーディング  
  
     アプリケーションで固定タスクとして実行される静的ステートメントです。  
  
-   実行時に構築  
  
     実行時に構築される SQL ステートメントで、これによりユーザーは SELECT、WHERE、ORDER BY などの一般的な句を使用してステートメントを調整できます。 これには、ユーザーが入力したアドホック クエリも含まれます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client ODBC ドライバーは、SQL ステートメントを直接サポートされない ODBC と ISO 構文のみを解析し、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]、ドライバーに変換する[!INCLUDE[tsql](../../includes/tsql-md.md)]します。 その他すべての SQL 構文は、変更されずに[!INCLUDE[ssDE](../../includes/ssde-md.md)]に渡されます。ここでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が有効な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] かどうかが判断されます。 この方法には、次の 2 つの利点があります。  
  
-   負荷の減少  
  
     ドライバーの処理オーバーヘッドが最小限に抑えられます。これは、スキャンする必要のある ODBC 句および ISO 句の数が少ないためです。  
  
-   柔軟性  
  
     プログラマは、アプリケーションの移植性を調整できます。 複数のデータベースに対する移植性を強化するには、主に ODBC 構文および ISO 構文を使用します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 固有の強力な機能を使用するには、対応する [!INCLUDE[tsql](../../includes/tsql-md.md)] 構文を使用します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは、完全なサポート[!INCLUDE[tsql](../../includes/tsql-md.md)]構文のすべての機能の ODBC ベースのアプリケーションを利用できるように[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
 SELECT ステートメント内の列リストには、現在のタスクを実行するのに必要な列だけを含める必要があります。 これにより、ネットワーク経由で送信されるデータ量が少なくなるだけでなく、アプリケーションに対するデータベース変更の影響も少なくなります。 アプリケーションでテーブルの列を参照していなければ、アプリケーションは、その列に行われる変更の影響を受けません。  
  
## <a name="see-also"></a>関連項目  
 [クエリの実行&#40;ODBC&#41;](executing-queries-odbc.md)  
  
  
