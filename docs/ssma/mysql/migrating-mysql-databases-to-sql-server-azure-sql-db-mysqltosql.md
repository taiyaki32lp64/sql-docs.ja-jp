---
title: SQL Server - Azure SQL DB への MySQL データベースの移行 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8006f9a0-394d-4238-8dc5-44255134628b
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 33dd7faf67e82f1259ac87a0ef8e0eb5fdf2927d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67908796"
---
# <a name="migrating-mysql-databases-to-sql-server---azure-sql-db-mysqltosql"></a>SQL Server - Azure SQL DB (MySQLToSql) への MySQL データベースの移行
SQL Server Migration Assistant (SSMA) for MySQL は、SQL Server または SQL Azure に MySQL データベースを迅速に移行するのに役立つ包括的な環境です。 SSMA for MySQL を使用してデータベース オブジェクトとデータを確認して、移行対象のデータベースを評価を SQL Server または SQL Azure のデータベース オブジェクトを移行でき、SQL Server または SQL Azure にデータを移行できます。  
  
## <a name="recommended-migration-process"></a>移行プロセスをお勧めします。  
正常にオブジェクトとデータ MySQL データベースからを SQL Server または SQL Azure に移行するには、次のプロセスを使用します。  
  
1.  [SSMA プロジェクトでの作業&#40;MySQLToSQL&#41;](../../ssma/mysql/working-with-ssma-projects-mysqltosql.md)します。  
  
    プロジェクトを作成した後は、プロジェクトの変換、移行、およびオプションのマッピングの種類を設定できます。 プロジェクト設定の詳細については、次を参照してください。[プロジェクト オプションの設定&#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)します。 データ型のマッピングをカスタマイズする方法については、次を参照してください[マッピング MySQL および SQL Server データ型&#40;MySQLToSQL。&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
2.  [MySQL に接続する&#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
3.  [SQL Server に接続する&#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
4.  [SQL Server スキーマへの MySQL データベースのマッピング&#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
5.  [Azure SQL DB に接続する&#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
  
6.  必要に応じて、[変換のための MySQL データベースを評価する&#40;MySQLToSQL&#41; ](../../ssma/mysql/assessing-mysql-databases-for-conversion-mysqltosql.md)変換のためのデータベース オブジェクトを評価し、変換にかかる時間を推定します。  
  
7.  [MySQL データベースの変換&#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
8.  [同期](loading-converted-database-objects-into-sql-server-mysqltosql.md)  
  
9. これは、次の方法のいずれかで行います。  
  
    -   スクリプトを保存し、SQL Server または SQL Azure で実行します。  
  
    -   データベース オブジェクトを同期します。  
  
10. [SQL Server - Azure SQL DB への MySQL データの移行&#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
11. 必要に応じて、データベース アプリケーションを更新します。  
  
> [!NOTE]  
> Information_schema と MySQL のスキーマを移行することはできません。  
  
## <a name="see-also"></a>参照  
[SSMA for MySQL のインストール&#40;MySqlToSql&#41;](../../ssma/mysql/installing-ssma-for-mysql-mysqltosql.md)  
[Ssma for MySQL 作業の開始&#40;MySQLToSQL&#41;](../../ssma/mysql/getting-started-with-ssma-for-mysql-mysqltosql.md)  
  
