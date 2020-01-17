---
title: catalog.operation_messages (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
helpviewer_keywords:
- catalog.operation_messages view [Integration Services]
- operation_messages view [Integration Services]
ms.assetid: 0b3cbe38-ce24-47ca-83ef-6538a5299d1a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: bfad11f3bcba41160fcb46ede37f6e7ea3c5ece4
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295160"
---
# <a name="catalogoperation_messages-ssisdb-database"></a>catalog.operation_messages (SSISDB データベース)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログでの操作中に記録されるメッセージを表示します。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|operation_message_id|**bigint**|メッセージの一意識別子 (ID)。|  
|operation_id|**bigint**|操作の一意の ID。|  
|message_time|**datetimeoffset(7)**|メッセージが作成された日時。|  
|message_type|**smallint**|表示されるメッセージの種類。|  
|message_source_type|**smallint**|メッセージ ソースの種類の ID。|  
|message|**nvarchar(max)**|メッセージのテキストです。|  
|extended_info_id|**bigint**|操作メッセージに関連する追加情報の ID については、[extended_operation_info](../../integration-services/system-views/catalog-extended-operation-info-ssisdb-database.md) ビューを参照してください。|  
  
## <a name="remarks"></a>Remarks  
 このビューには、カタログでの操作中に記録される各メッセージの行が表示されます。 このメッセージは、サーバー、パッケージの実行プロセス、または実行エンジンによって生成されます。  
  
 このビューに表示されるメッセージの種類は次のとおりです。  
  
|**message_type** 値|[説明]|  
|-----------------------------|-----------------|  
|-1|Unknown|  
|120|エラー|  
|110|警告|  
|70|[情報]|  
|10|検証前|  
|20|検証後|  
|30|実行前|  
|40|実行後|  
|60|進行状況|  
|50|StatusChange|  
|100|QueryCancel|  
|130|TaskFailed|  
|90|Diagnostic|  
|200|Custom|  
|140|DiagnosticEx<br /><br /> パッケージ実行タスクでは、子パッケージを実行するたびに、このイベントを記録します。 イベント メッセージは、子パッケージに渡されたパラメーター値で構成されます。<br /><br /> DiagnosticEx のメッセージ列の値は XML テキストです。|  
|400|NonDiagnostic|  
|80|VariableValueChanged|  
  
 このビューに表示されるメッセージ ソースの種類は次のとおりです。  
  
|**message_source_type**|[説明]|  
|-------------------------------|-----------------|  
|10|T-SQL や CLR ストアド プロシージャのようなエントリの API|  
|20|パッケージ (ISServerExec.exe) を実行するために使用する外部プロセス|  
|30|パッケージ レベルのオブジェクト|  
|40|制御フロー タスク|  
|50|制御フロー コンテナー|  
|60|データ フロー タスク|  
  
## <a name="permissions"></a>アクセス許可  
 このビューには、次の権限のいずれかが必要です。  
  
-   この操作の READ 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
> [!NOTE]  
>  サーバー上で操作を実行する権限がある場合は、操作に関する情報を表示する権限もあります。 行レベルのセキュリティが適用されるため、表示する権限がある行のみが表示されます。  
  
  
