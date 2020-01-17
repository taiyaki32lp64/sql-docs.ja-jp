---
title: catalog.execution_data_taps | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 54226c01-5b8f-4730-8a5f-1da2613f9689
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5f3450320f28a2f0abd133c93d1b43512484d446
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296572"
---
# <a name="catalogexecution_data_taps"></a>catalog.execution_data_taps 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  実行で定義されたデータ タップごとに情報が表示されます。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|data_tap_id|**bigint**|データ タップの一意識別子 (ID)。|  
|execution_id|**bigint**|実行のインスタンスの一意識別子 (ID)。|  
|package_path|**nvarchar(max)**|データがタップされたデータ フロー タスクのパッケージ パス。|  
|dataflow_path_id_string|**nvarchar (4000)**|データ フロー パスの識別文字列です。|  
|dataflow_task_guid|**uniqueidentifier**|データ フロー タスクの一意の ID。|  
|max_rows|**int**|キャプチャする行の数。 この値が指定されていない場合は、すべての行がキャプチャされます。|  
|filename|**nvarchar (4000)**|データ ダンプ ファイルの名前。 詳細については、「 [パッケージ実行用のダンプ ファイルを生成する](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)」を参照してください。|  
  
## <a name="permissions"></a>アクセス許可  
 このビューには、次の権限のいずれかが必要です。  
  
-   実行のインスタンスの READ 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
> [!NOTE]  
>  サーバー上で操作を実行する権限がある場合は、操作に関する情報を表示する権限もあります。 行レベルのセキュリティが適用されるため、表示する権限がある行のみが表示されます。  
  
## <a name="see-also"></a>参照  
 [パッケージ実行用のダンプ ファイルを生成する](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  
