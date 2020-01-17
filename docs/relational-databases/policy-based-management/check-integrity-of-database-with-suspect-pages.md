---
title: 問題のあるページを含むデータベースの整合性のチェック | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 3b1ec9fe-f6c5-46f7-aa63-6e671be1572d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: f0be2586d83aaf859ba6b5f4b57f08a4d679b9be
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68109881"
---
# <a name="check-integrity-of-database-with-suspect-pages"></a>問題のあるページを含むデータベースの整合性のチェック
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このルールでは、データベースの状態が問題ありに設定されているユーザー データベースがないか確認します。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] が 824 エラーを含むデータベース ページを読み取ると、そのページは問題があると見なされ、そのページ ID が msdb の suspect_pages テーブルに記録されます。また、そのページを含むデータベースは問題ありに設定されます。  
  
 エラー 824 は、読み取り操作中に論理的な一貫性エラーが検出されたことを示します。 このエラーは、多くの場合、I/O サブシステムのコンポーネントの障害によりデータが破損したことを示します。 このエラー状態は深刻で、データベースの整合性を損なう可能性があるので、すぐに解決する必要があります。  
  
## <a name="best-practices-recommendations"></a>ベスト プラクティスと推奨事項  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエラー ログを調査して、このデータベースの 824 エラーの詳細を確認します。  
  
-   完全なデータベース整合性確認 ([DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)) を実行します。  
  
-   [MSSQLSERVER_824](https://go.microsoft.com/fwlink/?LinkId=81397)で定義されているユーザー操作を実装します。  
  
## <a name="for-more-information"></a>詳細情報  
 [suspect_pages テーブルの管理 &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  
