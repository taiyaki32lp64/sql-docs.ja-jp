---
title: '[データベースの作成] (SQL Server インポートおよびエクスポート ウィザード) | Microsoft Docs'
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.createdatabase.f1
ms.assetid: 56a8a79f-086c-4bdc-8888-0045bb4b0cbf
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a80526b0f4a1b9f122ff79bbbb5a5a8ac08a2d07
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62893108"
---
# <a name="create-database-sql-server-import-and-export-wizard"></a>[データベースの作成] (SQL Server インポートおよびエクスポート ウィザード)
  使用して、 **Create Database**ページは、新しいデータベースをコピー先のファイルを定義します。  
  
 このページでは、新しいデータベースの作成に利用できるオプションのサブセットが提供されます。 すべてのオプションを表示する使用[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]します。  
  
 このウィザードの詳細については、次を参照してください。 [SQL Server インポートおよびエクスポート ウィザード](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)します。 ウィザードを正常に実行するために必要なアクセス許可と、ウィザードを起動するオプションについて説明しますを参照してください。 [、SQL Server インポートおよびエクスポート ウィザードを実行](start-the-sql-server-import-and-export-wizard.md)します。  
  
 SQL Server インポートおよびエクスポート ウィザードの目的は、変換元から変換先にデータをコピーすることです。 また、このウィザードでは、変換先データベースと変換先テーブルも作成できます。 ただし、複数のデータベースやテーブルまたは他の種類のデータベース オブジェクトをコピーする必要がある場合は、データベース コピー ウィザードを使用してください。 詳細については、「 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)」を参照してください。  
  
## <a name="options"></a>および  
 **名前**  
 対象になる SQL Server データベースの一意な名前を指定します。 データベースに名前を付けるときは、必ず SQL Server の規約に従ってください。  
  
 **データ ファイル名**  
 データ ファイルの名前を表示します。 この名前は、指定されたデータベース名から派生されます。  
  
 **ログ ファイルの名前**  
 ログ ファイルの名前を表示します。 この名前は、指定されたデータベース名から派生されます。  
  
 **初期サイズ (データ ファイル)**  
 データ ファイルの初期サイズを MB 単位で指定します。  
  
 **拡張 (データ ファイル) を許可しません。**  
 指定した初期サイズを超えるデータ ファイルの拡張を許可するかどうかを示します。  
  
 **比率で拡張 (データ ファイル)**  
 データ ファイルの拡張を許可する比率を指定します。  
  
 **サイズ (データ ファイル) で拡張します。**  
 データ ファイルの拡張を許可するサイズを MB 単位で指定します。  
  
 **初期サイズ (ログ ファイル)**  
 ログ ファイルの初期サイズを MB 単位で指定します。  
  
 **拡張を許可しない (ログ ファイル)**  
 指定した初期サイズを超えるログ ファイルの拡張を許可するかどうかを示します。  
  
 **(ログ ファイル) の比率で拡張します。**  
 ログ ファイルの拡張を許可する比率を指定します。  
  
 **サイズ (ログ ファイル) で拡張します。**  
 ログ ファイルの拡張を許可するサイズを MB 単位で指定します。  
  
  
