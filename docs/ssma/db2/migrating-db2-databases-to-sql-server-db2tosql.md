---
title: SQL Server (DB2ToSQL) にデータベースを移行する DB2 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 14d2e655-af7e-4aa5-ba28-0e3d0d025518
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 79cc961148add0bf2096a716b669199360a565b1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68084652"
---
# <a name="migrating-db2-databases-to-sql-server-db2tosql"></a>SQL Server (DB2ToSQL) への DB2 データベースの移行
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) for DB2 は、DB2 データベースを迅速に移行するのに役立つ包括的な環境[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB します。 SSMA for DB2 を使用してデータベース オブジェクトとデータを確認して、移行対象のデータベースを評価をするデータベース オブジェクトを移行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB へのデータを移行および[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB。 SYS およびシステムの DB2 スキーマを移行できないことに注意してください。  
  
## <a name="recommended-migration-process"></a>移行プロセスをお勧めします。  
DB2 データベースからオブジェクトとデータを正常に移行する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure SQL DB は、次のプロセスを使用します。  
  
1.  [新しい SSMA プロジェクト](https://msdn.microsoft.com/66437b45-4686-4fc7-a91b-ebde45e0f1b0)します。  
  
    プロジェクトを作成した後は、プロジェクトの変換、移行、およびオプションのマッピングの種類を設定できます。 プロジェクトの設定については、次を参照してください。[プロジェクト設定&#40;変換&#41; &#40;DB2ToSQL&#41; ](../../ssma/db2/project-settings-conversion-db2tosql.md)および関連するセクション。 データ型のマッピングをカスタマイズする方法については、次を参照してください。[マッピング DB2 と SQL Server データ型&#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md)します。  
  
2.  [DB2 データベースに接続する](https://msdn.microsoft.com/5eb5801d-f0c3-4127-97c0-0b1ef49f4844)します。  
  
3.  [SQL Server に接続する](https://msdn.microsoft.com/b59803cb-3cc6-41cc-8553-faf90851410e)します。  
  
4.  [SQL Server スキーマへの DB2 スキーマのマップ](https://msdn.microsoft.com/05ff7bd4-e60b-4f48-a893-bc2346aa9a8a)します。  
  
5.  必要に応じて、[評価レポート](https://msdn.microsoft.com/9e13eba0-e3cf-4205-974f-c00f982061de)変換のためのデータベース オブジェクトを評価し、変換にかかる時間を推定します。  
  
6.  [DB2 スキーマの変換](https://msdn.microsoft.com/7947efc3-ca86-4ec5-87ce-7603059c75a0)します。  
  
7.  [SQL Server に変換されたデータベース オブジェクトを読み込む](https://msdn.microsoft.com/f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3)します。  
  
    これは、次の方法のいずれかで行います。  
  
    -   スクリプトを保存しで実行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
    -   データベース オブジェクトを同期します。  
  
8.  [DB2 のデータを SQL Server に移行する](https://msdn.microsoft.com/86cbd39f-6dac-409a-9ce1-7dd54403f84b)します。  
  
9. 必要に応じて、データベース アプリケーションを更新します。  
  
## <a name="see-also"></a>参照  
[SSMA for DB2 のインストール&#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-db2tosql.md)  
[Ssma for DB2 作業の開始&#40;DB2ToSQL&#41;](../../ssma/db2/getting-started-with-ssma-for-db2-db2tosql.md)  
  
