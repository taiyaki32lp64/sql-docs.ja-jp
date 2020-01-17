---
title: 履歴クリーンアップ タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.historycleanuptask.f1
helpviewer_keywords:
- history tables [SQL Server]
- History Cleanup task [Integration Services]
ms.assetid: 5defc5b9-dfd3-4859-a7fe-ac8c2b5480f8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1844f4088c026dda5636cd31a7f90b5effe4bfbc
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298247"
---
# <a name="history-cleanup-task"></a>履歴クリーンアップ タスク

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  履歴クリーンアップ タスクは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb データベースの、次の履歴テーブル内のエントリを削除します。  
  
-   backupfile  
  
-   backupfilegroup  
  
-   backupmediafamily  
  
-   backupmediaset  
  
-   backupset  
  
-   restorefile  
  
-   restorefilegroup  
  
-   restorehistory  
  
 履歴クリーンアップ タスクを使用すると、パッケージは、バックアップ操作と復元操作、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブ、およびデータベース メンテナンス プランに関連する履歴データを削除できます。  
  
 このタスクは、sp_delete_backuphistory システム ストアド プロシージャをカプセル化し、指定した日付を引数として渡します。 詳細については、「[sp_delete_backuphistory (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md)」を参照してください。  
  
## <a name="configuration-of-the-history-cleanup-task"></a>履歴クリーンアップ タスクの構成  
 このタスクには、履歴テーブルに保持されるデータの、最も古い日付を指定するプロパティが含まれます。 日付は、現在の日付から起算して、日、週、月、または年数単位で指定できます。タスクは、その間隔を自動的に日付に変換します。  
  
 プロパティは、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから設定できます。 このタスクは、 **デザイナーの** [ツールボックス] **の** [メンテナンス プランのタスク] [!INCLUDE[ssIS](../../includes/ssis-md.md)] に表示されます。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックを参照してください。  
  
-   [履歴クリーンアップ タスク (メンテナンス プラン)](../../relational-databases/maintenance-plans/history-cleanup-task-maintenance-plan.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="see-also"></a>参照  
 [Integration Services タスク](../../integration-services/control-flow/integration-services-tasks.md)   
 [制御フロー](../../integration-services/control-flow/control-flow.md)  
  
  
