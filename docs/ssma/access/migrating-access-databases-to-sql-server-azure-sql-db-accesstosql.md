---
title: SQL Server - Azure SQL DB への Access データベースの移行 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- instructions, migration
- migrating databases, overview
- overview, migration process
- procedure, migration
- recommended migration process
ms.assetid: 76a3abcf-2998-4712-9490-fe8d872c89ca
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: 959af9bcb1879dc19d2bfb99253b4c40d637fd1e
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68260242"
---
# <a name="migrating-access-databases-to-sql-server---azure-sql-db-accesstosql"></a>SQL Server - Azure SQL DB (AccessToSQL) へのアクセス データベースの移行
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) は、すばやくへの Access データベースを移行するのに役立つ包括的な環境を提供するツール[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure です。 SSMA を使用すると、アクセス権をレビューできますと[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure データベース オブジェクト、Access データベースの移行の評価、Access データベース オブジェクトを変換、読み込みに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure、し、データを移行します。  
  
## <a name="recommended-migration-process"></a>推奨される移行プロセス  
アクセスをオブジェクトとデータを正常に移行する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure、次のプロセスを使用します。  
  
1.  [新しい SSMA プロジェクト作成](creating-and-managing-projects-accesstosql.md)です。 後に、プロジェクトを作成する[プロジェクト オプションを設定](setting-conversion-and-migration-options-accesstosql.md)(変換オプションの移行オプション、データ型のマッピングなど)。  
  
2.  [Access データベース ファイルを追加](adding-and-removing-access-database-files-accesstosql.md)をプロジェクトにします。  
  
    コンピューターまたはネットワーク上にあるファイルを含む、個々 のファイルを追加することができます。  
  
3.  [SQL Server のターゲット インスタンスに接続する](connecting-to-sql-server-accesstosql.md)または[SQL Azure のターゲット インスタンスに接続する](connecting-to-azure-sql-db-accesstosql.md)します。  
  
    SQL Server または SQL Azure に接続できます。  
  
4.  1 つ以上の Access データベースの間のマッピングをカスタマイズして[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure のスキーマ、[マップ ソースとターゲット データベース](mapping-source-and-target-databases-accesstosql.md)します。  
  
5.  必要に応じて、できます[評価レポートを作成する](assessing-access-database-objects-for-conversion-accesstosql.md)に Access データベースのオブジェクトを正常に変換するかどうかを判断する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure です。  
  
6.  [Access データベース オブジェクトを変換](converting-access-database-objects-accesstosql.md)に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure のオブジェクトの定義。  
  
7.  [SQL Server に変換されたデータベース オブジェクトを読み込む](loading-converted-database-objects-into-sql-server-accesstosql.md)します。  
  
    データベース オブジェクトを読み込むことができます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]保存、SSMA を使用して SQL Azure または[!INCLUDE[tsql](../../includes/tsql-md.md)]スクリプト。  
  
8.  [SQL Server にデータへのアクセスを移行](migrating-access-data-into-sql-server-azure-sql-db-accesstosql.md)します。  
  
    > [!NOTE]  
    > 変換、読み込み、およびスキーマと 1 つの手順でデータを移行することができます。 1 回のクリックの移行を実行する をクリックして、**変換、読み込み、および移行**ボタンをクリックします。  
  
9. Access アプリケーションのデータを使用する場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure を使用して[Access テーブル、SQL Server テーブルをリンク](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)します。  
  
このプロセスを指示するのに、移行ウィザードを使用することもできます。 詳細については、次を参照してください。[移行ウィザード](migration-wizard-accesstosql.md)します。  
  
## <a name="see-also"></a>関連項目  
[SQL Server Migration Assistant for Access の概要](getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)  
[Access データベースの移行の準備](preparing-access-databases-for-migration-accesstosql.md)
