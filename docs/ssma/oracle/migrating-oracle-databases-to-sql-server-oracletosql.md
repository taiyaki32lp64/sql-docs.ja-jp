---
title: SQL Server (OracleToSQL) にデータベースの移行の Oracle |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 04/22/2018
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1d196dd6-4322-4c98-bb72-602c57d96134
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: e1021643d503e1ca77f120b81046b3773f8ff458
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68259100"
---
# <a name="migrating-oracle-databases-to-sql-server-oracletosql"></a>SQL Server への Oracle のデータの移行 (OracleToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) for Oracle は Oracle データベースを迅速に移行するのに役立つ包括的な環境[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、Azure SQL DB、または Azure SQL Data Warehouse。 SSMA for Oracle を使用してデータベース オブジェクトとデータを確認して、移行対象のデータベースを評価をするデータベース オブジェクトを移行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、Azure SQL DB、または Azure SQL Data Warehouse へのデータを移行し、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、Azure SQL DB、または Azure SQL データウェアハウス。 SYS および Oracle のシステム スキーマを移行することはできませんに注意してください。
  
## <a name="recommended-migration-process"></a>移行プロセスをお勧めします。  
Oracle データベースからオブジェクトとデータを正常に移行する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、Azure SQL DB、または Azure SQL Data Warehouse では、次のプロセスを使用します。
  
1.  [新しい SSMA プロジェクト作成](working-with-ssma-projects-oracletosql.md)です。  
  
    プロジェクトを作成した後は、プロジェクトの変換、移行、およびオプションのマッピングの種類を設定できます。 プロジェクトの設定については、次を参照してください。[プロジェクト オプションの設定&#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md)します。 データ型のマッピングをカスタマイズする方法については、次を参照してください。[マッピング Oracle および SQL Server データ型&#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md)します。  
  
2.  [Oracle データベース サーバーに接続する](connecting-to-oracle-database-oracletosql.md)します。  
  
3.  [SQL Server のインスタンスに接続する](connecting-to-sql-server-oracletosql.md)します。  
  
4.  [SQL Server データベースのスキーマに Oracle データベース スキーマを割り当てる](mapping-oracle-schemas-to-sql-server-schemas-oracletosql.md)します。  
  
5.  必要に応じて、[評価レポートを作成する](assessing-oracle-schemas-for-conversion-oracletosql.md)変換のためのデータベース オブジェクトを評価し、変換にかかる時間を推定します。  
  
6.  [SQL Server スキーマに Oracle データベース スキーマを変換](converting-oracle-schemas-oracletosql.md)します。  
  
7.  [SQL Server に変換されたデータベース オブジェクトを読み込む](loading-converted-database-objects-into-sql-server-oracletosql.md)します。  
  
    これは、次の方法のいずれかで行います。  
  
    -   スクリプトを保存しで実行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
    -   データベース オブジェクトを同期します。  
  
8.  [SQL Server にデータを移行](migrating-oracle-data-into-sql-server-oracletosql.md)します。  
  
9. 必要に応じて、データベース アプリケーションを更新します。  
  
## <a name="see-also"></a>参照  
[SSMA for Oracle のインストール&#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-oracletosql.md)  
[Ssma for Oracle 作業の開始&#40;OracleToSQL&#41;](../../ssma/oracle/getting-started-with-ssma-for-oracle-oracletosql.md)  
  
