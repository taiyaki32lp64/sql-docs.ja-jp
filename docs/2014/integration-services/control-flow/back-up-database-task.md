---
title: データベースのバックアップ タスク | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.backupdatabasetask.f1
helpviewer_keywords:
- database backups [Integration Services]
- Back Up Database task [Integration Services]
- backing up databases [Integration Services]
- transaction log backups [Integration Services]
- backing up transaction logs [Integration Services]
ms.assetid: b8839d71-13b7-41f2-a434-cb95020e79d7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d4b6aabb1f44c2a25704b7079074a5600c4d52d4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62833130"
---
# <a name="back-up-database-task"></a>データベースのバックアップ タスク
  データベースのバックアップ タスクは、さまざまな種類の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのバックアップを実行します。 詳細については、「 [Back Up and Restore of SQL Server Databases](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)」をご覧ください。  
  
 データベースのバックアップ タスクを使用すると、パッケージは単一データベースまたは複数データベースをバックアップできます。 タスクにより単一データベースのみをバックアップする場合、バックアップ対象となるデータベース、ファイル、またはファイル グループなどのコンポーネントを選択できます。  
  
## <a name="supported-recover-models-and-backup-types"></a>サポートされている復旧モデルとバックアップの種類  
 次の表に、データベースのバックアップ タスクがサポートする復旧モデルとバックアップの種類を示します。  
  
|復旧モデル|[データベース]|データベースの差分|[トランザクション ログ]|ファイルまたはファイルの差分|  
|--------------------|--------------|---------------------------|---------------------|-------------------------------|  
|Simple|必須|省略可|サポートされていません|サポートされていません|  
|[完全]|必須|省略可|必須|省略可|  
|一括ログ|必須|省略可|必須|省略可|  
  
 データベースのバックアップ タスクは、Transact-SQL BACKUP ステートメントをカプセル化します。 詳細については、「[BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)」を参照してください。  
  
## <a name="configuration-of-the-back-up-database-task"></a>データベースのバックアップ タスクの構成  
 プロパティは、 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーから設定できます。 このタスクは、 **デザイナーの** [ツールボックス] **の** [メンテナンス プランのタスク] [!INCLUDE[ssIS](../../../includes/ssis-md.md)] に表示されます。  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックを参照してください。  
  
-   [[データベースのバックアップ タスク] &#40;メンテナンス プラン&#41;](../../relational-databases/maintenance-plans/options-in-the-back-up-database-task-for-maintenance-plan.md)  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](../set-the-properties-of-a-task-or-container.md)  
  
  
