---
title: SQL Server Native Client ODBC データ ソース |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC data sources, about data sources
- ODBC data sources, names
- data sources [SQL Server Native Client]
- names [ODBC]
- ODBC applications, data sources
- SQL Server Native Client ODBC driver, data sources
- ODBC data sources
ms.assetid: a6a50fd0-d439-43fd-b76f-16ec02f478c5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: de1226d675859312e1ccaf908141586f865c8946
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63028389"
---
# <a name="sql-server-native-client-odbc-data-sources"></a>SQL Server Native Client ODBC データ ソース
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータ ソース名 (DSN) によって ODBC データ ソースが特定されます。ODBC データ ソースには、特定のサーバー上の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに接続するために ODBC アプリケーションで必要となるすべての情報が含まれています。 ODBC データ ソース名を定義するには次の 2 つの方法があります。  
  
-   クライアント コンピューターの コントロール パネルの 管理ツールを開きをダブルクリック**データ ソース (ODBC)** します。 ODBC データ ソース アドミニストレーターが起動します。これを使用して DSN を作成できます。  
  
-   ODBC アプリケーションで呼び出す[SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md)します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータ ソースには次の情報が含まれます。  
  
-   データ ソースの名前です。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の特定のインスタンスとの接続に必要な情報。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の特定のインスタンスで使用する既定のデータベース (省略可)。  
  
-   使用する ANSI オプション、パフォーマンス統計情報をログに記録するかどうかなどの設定 (省略可)。  
  
 データ ソース経由で接続する場合、ODBC アプリケーションは必要ありません。 ただしアプリケーションでは、ドライバーが DSN から検出する接続情報と同じ情報を、ODBC 接続関数に対して指定する必要があります。  
  
## <a name="see-also"></a>参照  
 [SQL Server と通信する&#40;ODBC&#41;](communicating-with-sql-server-odbc.md)  
  
  
