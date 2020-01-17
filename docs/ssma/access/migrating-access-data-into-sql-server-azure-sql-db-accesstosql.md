---
title: SQL Server - Azure SQL DB (AccessToSQL) に移行するデータにアクセス |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- bulk loading data
- data, loading into SQL Azure
- data, loading into SQL Server
- migrating databases, loading data
- migrating databases, options
- options, migrating data
- SQL Azure, migrating data into
- SQL Server, migrating data into
ms.assetid: f3b18af7-1af0-499d-a00d-a0af94895625
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 8f0e93efee0c57c904c32ec52fbb560f973f21b8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67907145"
---
# <a name="migrating-access-data-into-sql-server---azure-sql-db-accesstosql"></a>SQL Server - Azure SQL DB (AccessToSQL) に移行するデータにアクセス
データベース オブジェクトを正常に作成した後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]へのアクセスからデータを移行する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure です。  
  
## <a name="setting-migration-options"></a>移行オプションの設定  
データを移行する前に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure、プロジェクトの移行オプションの確認、**プロジェクト設定** ダイアログ ボックス。 このダイアログ ボックスでは、移行のバッチ サイズ、テーブルのロック、制約チェック、挿入トリガーを起動、id および処理するには、null 値と日付のうちを処理する方法を設定できます、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]範囲。 詳細については、次を参照してください。[プロジェクトの設定 (移行)](https://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d)します。  
  
## <a name="migrating-data"></a>データの移行  
移行データは、一括読み込み操作へのデータの行を移動する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure でのトランザクション。 読み込まれる行の数[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure の各トランザクションではプロジェクトの設定で構成されます。  
  
移行のメッセージを表示するには、出力ウィンドウが表示されていることを確認します。 そうでない場合に、**ビュー**メニューの **出力**します。  
  
**データを移行するには**  
  
1.  Access データベース オブジェクトが読み込まれているかどうかを確認[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure です。  
  
2.  アクセス メタデータ エクスプ ローラーでは、移行するデータを含むオブジェクトを選択します。  
  
    -   データベース全体のデータを移行するには、データベース名の横にあるチェック ボックスを選択します。  
  
    -   個々 のテーブルからデータを移行するデータベースを展開し、**テーブル**、テーブルの横にあるチェック ボックスを選択します。 個々 のテーブルからデータを省略するには、チェック ボックスをオフにします。  
  
3.  右クリック**データベース**選び**Migrate Data**。  
  
移行することもできます SSMA 以外のデータを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **bcp**コマンド ライン ユーティリティまたは[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]します。 これらのツールの詳細については、次を参照してください。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オンライン ブックの「します。  
  
## <a name="next-step"></a>次の手順  
リンクする Access データベースのテーブルの移行後に使用を続行するデータベース アプリケーションにアクセスした場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure テーブル。 詳細については、次を参照してください。 [SQL Server への Access アプリケーションのリンク](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)します。  
  
## <a name="see-also"></a>参照  
[SQL Server へのアクセス データベースの移行](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[設定の変換と移行のオプション](setting-conversion-and-migration-options-accesstosql.md)  
  
