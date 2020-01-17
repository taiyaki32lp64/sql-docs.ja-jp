---
title: メンテナンス クリーンアップ タスク | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.maintenancecleanuptask.f1
helpviewer_keywords:
- deleting files
- removing files
- Maintenance Cleanup task
ms.assetid: 73ad3cd6-9a6d-44cf-905f-c56aa658bf42
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d8b3c3aa4f63018e91370c4e01dada40c35a5f2f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62830801"
---
# <a name="maintenance-cleanup-task"></a>メンテナンス クリーンアップ タスク
  メンテナンス クリーンアップ タスクでは、データベース バックアップ ファイルや、メンテナンス プランによって作成されたレポートなど、メンテナンス プランに関連するファイルを削除します。 詳細については、「 [メンテナンス プラン](../../relational-databases/maintenance-plans/maintenance-plans.md) 」および「 [SQL Server データベースのバックアップと復元](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)」を参照してください。  
  
 パッケージは、メンテナンス クリーンアップ タスクを使用して、指定したサーバー上のバックアップ ファイルやメンテナンス プランのレポートを削除することができます。 メンテナンス クリーンアップ タスクには、特定のファイルを削除したり、1 つのフォルダー内のファイルのグループを削除するオプションがあります。 必要に応じて、削除するファイルの拡張子を指定することもできます。  
  
 メンテナンス クリーンアップ タスクを構成してバックアップ ファイルを削除する場合、既定のファイル名の拡張子は BAK です。 レポート ファイルの場合、既定のファイル名の拡張子は TXT です。 必要に応じて拡張子を更新できます。この場合、唯一の制限事項として、拡張子を 256 文字未満にする必要があります。  
  
 不要になった古いファイルは削除するのが普通です。メンテナンス クリーンアップ タスクは、指定した期限に達したファイルを削除するように構成できます。 たとえば、4 週間を経過したファイルを削除するようにタスクを構成できます。 削除するファイルの期限は、日、週、月、または年を使用して指定できます。 削除するファイルの最小経過期間を指定しないと、指定した種類のファイルがすべて削除されます。  
  
 以前のバージョンのメンテナンス クリーンアップ タスクとは対照的に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バージョンのタスクでは、指定したディレクトリのサブディレクトリにあるファイルは自動的には削除されません。 この制約により、メンテナンス クリーンアップ タスクの機能を悪用して故意にファイルを削除するような外部からの攻撃を防ぐことができます。 直下のサブフォルダーを削除するには、 **[メンテナンス クリーンアップ タスク]** ダイアログ ボックスの **[直下のサブフォルダーを含める]** オプションをオンにして、明示的に指定する必要があります。  
  
## <a name="configuration-of-the-maintenance-cleanup-task"></a>メンテナンス クリーンアップ タスクの構成  
 プロパティは、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから設定できます。 このタスクは、 **デザイナーの** [ツールボックス] **の** [メンテナンス プランのタスク] [!INCLUDE[ssIS](../../includes/ssis-md.md)] に表示されます。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックを参照してください。  
  
-   [[メンテナンス クリーンアップ タスク] (メンテナンス プラン)](../../relational-databases/maintenance-plans/maintenance-cleanup-task-maintenance-plan.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 これらのプロパティを [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定する方法の詳細については、「 [タスクまたはコンテナーのプロパティを設定する](../set-the-properties-of-a-task-or-container.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Integration Services タスク](integration-services-tasks.md)   
 [制御フロー](control-flow.md)  
  
  
