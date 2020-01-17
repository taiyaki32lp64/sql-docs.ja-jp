---
title: ISO オプションの効果 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ISO options (ODBC)
- ODBC applications, ISO options
- ODBC applications, statements
- SQL Server Native Client ODBC driver, ISO options
- statements [ODBC], ISO options
ms.assetid: 813f1397-fa0b-45ec-a718-e13fe2fb88ac
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 43347e4fcf517dc52c8791dc81220a8990e1655d
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73779868"
---
# <a name="effects-of-iso-options"></a>ISO オプションの効果
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ODBC 標準は、ISO 標準と密接に対応しています。ODBC アプリケーションは、ODBC ドライバーの動作が標準に準拠していることを前提としています。 ODBC 標準で定義されている動作により厳密に対応するために、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、接続先の SQL Server のバージョンで使用可能な ISO オプションが常に使用されます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のインスタンスに接続すると、サーバーは、クライアントが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーを使用していることを検出し、いくつかのオプションをに設定します。  
  
 ステートメント自体はドライバーが実行します。ODBC アプリケーションはステートメントの実行に対して何の要求も行いません。 ISO オプションを設定することで、SQL Native Client ODBC ドライバーを使用する ODBC アプリケーションの移植性が高まります。これは、サーバーの動作が ISO 標準に準拠するためです。  
  
 DB-Library ベースのアプリケーションは、通常これらのオプションを有効にしません。 ODBC または DB-LIBRARY クライアントが同じ SQL ステートメントを実行しているときに異なる動作を観察するサイトでは、これが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーの問題を指しているとは限りません。 最初に、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーで使用されるのと同じ SET オプションを使用して、DB-LIBRARY 環境でステートメントを再実行する必要があります。  
  
 SET オプションはユーザーやアプリケーションがいつでも有効または無効にできるので、ストアド プロシージャやトリガーの開発者は、上記の SET オプションを有効にした場合と無効にした場合の両方で、開発したプロシージャやトリガーをテストする必要があります。 これにより、プロシージャやトリガーの起動時に、接続に設定されているオプションに関係なく、プロシージャやトリガーが適切に動作することを確認できます。 これらのオプションのいずれかについて特定の設定が必要なトリガーやストアド プロシージャは、そのトリガーやストアド プロシージャの起動時に SET ステートメントを実行する必要があります。 この SET ステートメントは、トリガーやストアド プロシージャが実行されている間だけ有効になり、トリガーやストアド プロシージャが終了すると元の設定が復元されます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスに接続しているときは、4 番目の SET オプションの CONCAT_NULL_YIELDS_NULL も有効になります。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、データソースに AnsiNPW = NO が指定されている場合、または[SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md)または[SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)のいずれかで、これらのオプションが設定されていません。  
  
 前に説明した ISO オプションと同様に、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、データソースに QuotedID = NO が指定されている場合、または**SQLDriverConnect**または**SQLBrowseConnect**のいずれかに対して、QUOTED_IDENTIFIER オプションが有効になりません。  
  
 ドライバーが SET オプションの現在の状態を確認できるようにするために、ODBC アプリケーションでは、[!INCLUDE[tsql](../../../includes/tsql-md.md)] SET ステートメントを使用して SET オプションを設定しないようにします。 これらのオプションを設定する場合は、データ ソースまたは接続オプションのみを使用するようにします。 アプリケーションが SET ステートメントを実行した場合、ドライバーは不正な SQL ステートメントを生成する可能性があります。  
  
## <a name="see-also"></a>参照  
 [ &#40;ステートメントの実行&#41; ODBC](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)   
 [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md)   
 [SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)  
  
  
