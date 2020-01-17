---
title: データベースのバックアップ タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.backupdatabasetask.f1
helpviewer_keywords:
- database backups [Integration Services]
- Back Up Database task [Integration Services]
- backing up databases [Integration Services]
- transaction log backups [Integration Services]
- backing up transaction logs [Integration Services]
ms.assetid: b8839d71-13b7-41f2-a434-cb95020e79d7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e45060a494fad2fbd0310a31bdf433e624becdc2
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294303"
---
# <a name="back-up-database-task"></a>データベースのバックアップ タスク

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  データベースのバックアップ タスクは、さまざまな種類の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのバックアップを実行します。 詳細については、「 [Back Up and Restore of SQL Server Databases](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)」をご覧ください。  
  
 データベースのバックアップ タスクを使用すると、パッケージは単一データベースまたは複数データベースをバックアップできます。 タスクにより単一データベースのみをバックアップする場合、バックアップ対象となるデータベース、ファイル、またはファイル グループなどのコンポーネントを選択できます。  
  
## <a name="supported-recover-models-and-backup-types"></a>サポートされている復旧モデルとバックアップの種類  
 次の表に、データベースのバックアップ タスクがサポートする復旧モデルとバックアップの種類を示します。  
  
|復旧モデル|データベース|データベースの差分|[トランザクション ログ]|ファイルまたはファイルの差分|  
|--------------------|--------------|---------------------------|---------------------|-------------------------------|  
|Simple|Required|省略可|サポートされていません|サポートされていません|  
|[完全]|Required|省略可|Required|省略可|  
|一括ログ|Required|省略可|Required|省略可|  
  
 データベースのバックアップ タスクは、Transact-SQL BACKUP ステートメントをカプセル化します。 詳細については、「[BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)」を参照してください。  
  
## <a name="configuration-of-the-back-up-database-task"></a>データベースのバックアップ タスクの構成  
 プロパティは、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから設定できます。 このタスクは、 **デザイナーの** [ツールボックス] **の** [メンテナンス プランのタスク] [!INCLUDE[ssIS](../../includes/ssis-md.md)] に表示されます。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックを参照してください。  
  
-   [[データベースのバックアップ タスク] &#40;メンテナンス プラン&#41;](../../relational-databases/maintenance-plans/options-in-the-back-up-database-task-for-maintenance-plan.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
  
