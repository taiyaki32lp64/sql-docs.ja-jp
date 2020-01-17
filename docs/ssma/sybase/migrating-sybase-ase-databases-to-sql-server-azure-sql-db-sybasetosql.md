---
title: SQL Server - Azure SQL DB への Sybase ASE データベースの移行 |Microsoft Docs
ms.custom: ''
ms.date: 11/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ed7952d4-8331-44d7-bccf-3440e17238b2
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: c3735e03e3196f899ab33ca152364244e3331ac5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68028852"
---
# <a name="migrating-sap-ase-databases-to-sql-server---azure-sql-database-sybasetosql"></a>SQL Server - Azure SQL Database (SybaseToSQL) に SAP ASE データベースを移行します。
SQL Server Migration Assistant (SSMA) for SAP Adaptive Server Enterprise (ASE) は、すぐに SAP ASE データベースを移行するのに役立つ包括的な環境[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL Database。 SAP ASE の SSMA を使用してデータベース オブジェクトとデータを確認して、移行対象のデータベースを評価をするデータベース オブジェクトを移行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]や Azure SQL Database へのデータを移行および[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL Database。  
  
## <a name="recommended-migration-process"></a>推奨される移行プロセス  
SAP ASE データベースからオブジェクトとデータを正常に移行する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL Database に、次のプロセスを使用します。  
  
1.  [新しい SSMA プロジェクト作成](working-with-ssma-projects-sybasetosql.md)です。  
  
    プロジェクトを作成した後は、プロジェクトの変換、移行、およびオプションのマッピングの種類を設定できます。 プロジェクトの設定については、次を参照してください。[プロジェクト オプションの設定&#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md)します。 データ型のマッピングをカスタマイズする方法については、次を参照してください。[マッピングの Sybase ASE と SQL Server データ型&#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)します。  
  
2.  [SAP ASE データベース サーバーに接続する](connecting-to-sybase-ase-sybasetosql.md)します。  
  
3.  [SQL Server インスタンスへの接続](connecting-to-sql-server-sybasetosql.md)または[Azure SQL Database のインスタンスへの接続](connecting-to-azure-sql-db-sybasetosql.md)します。  
  
4.  [SQL Server に SAP ASE データベース スキーマを割り当てる Azure SQL Database のデータベース スキーマ/](https://msdn.microsoft.com/2c927003-c49d-4fe1-8e3e-5b2899166268)します。  
  
5.  必要に応じて、[評価レポートを作成する](assessing-sybase-ase-database-objects-for-conversion-sybasetosql.md)変換のためのデータベース オブジェクトを評価し、変換にかかる時間を推定します。  
  
6.  [SQL Server に SAP ASE データベース スキーマを変換/Azure SQL Database スキーマ](https://msdn.microsoft.com/509cb65d-2f54-427a-83d7-37919cc4e3e3)します。  
  
7.  [SQL Server に変換されたデータベース オブジェクトを読み込むと Azure SQL Database](https://msdn.microsoft.com/4c59256f-99a8-4351-9559-a455813dbd06)します。  
  
    スクリプトを保存するかで実行して[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL Database、またはデータベース オブジェクトを同期します。  
  
8.  [SQL Server にデータを移行または Azure SQL Database](https://msdn.microsoft.com/54a39f5e-9250-4387-a3ae-eae47c799811)します。  
  
9. 必要に応じて、データベース アプリケーションを更新します。  
  
## <a name="see-also"></a>関連項目  
[SSMA for SAP ASE のインストール&#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
[SSMA で SAP ASE の概要&#40;SybaseToSQL&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)  
  
