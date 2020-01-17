---
title: catalog.validations (SSISDB データベース) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: dbafe110-b480-48f3-b45f-31d71ca68f62
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 086b4503289c01f8b0022633361e7ce72dff73e1
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295253"
---
# <a name="catalogvalidations-ssisdb-database"></a>catalog.validations (SSISDB データベース)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログのすべてのプロジェクトおよびパッケージ検証の詳細を表示します。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|validation_id|**bigint**|検証の一意識別子 (ID)。|  
|environment_scope|**Char(1)**|検証が考慮する環境参照を示します。 値が `A` の場合は、プロジェクトに関連するすべての環境参照が検証に含まれます。 値が `S` の場合は、1 つの環境参照のみが含まれます。 値が `D` の場合、環境参照は含まれず、各パラメーターには、検証に合格するため、既定のリテラル値を指定する必要があります。|  
|validate_type|**Char(1)**|実行する検証の種類。 検証で使用される種類は、依存関係の検証 (`D`) または完全検証 (`F`) です。 パッケージの検証では、常に完全検証が実施されます。|  
|folder_name|**nvarchar(128)**|対応するプロジェクトを含むフォルダーの名前。|  
|project_name|**nvarchar(128)**|プロジェクトの名前。|  
|project_lsn|**bigint**|検証されるプロジェクトのバージョン。|  
|use32bitruntime|**bit**|64 ビット オペレーティング システムで 32 ビットのランタイムを使用してパッケージを実行するかどうかを示します。 値が `1` の場合、実行は 32 ビット ランタイムで実行されます。 値が `0` の場合、実行は 64 ビット ランタイムで実行されます。|  
|reference_id|**bigint**|環境を参照するためプロジェクトによって使用されるプロジェクト環境参照の ID。|  
|operation_type|**smallint**|操作の種類。 このビューに表示される操作には、プロジェクト検証 (`300`) とパッケージ検証 (`301`) が含まれます。|  
|object_name|**nvarhcar(260)**|オブジェクトの名前。|  
|object_type|**smallint**|オブジェクトの種類。 オブジェクトは、プロジェクト (`20`) またはパッケージ (`30`) です。|  
|object_id|**bigint**|操作の影響を受けるオブジェクトの ID。|  
|start_time|**datetimeoffset(7)**|操作が開始したときの日時。|  
|end_time|**datetimeoffsset(7)**|操作が終了したときの日時。|  
|ステータス|**int**|操作の状態。 使用される可能性がある値は、作成済み (`1`)、実行中 (`2`)、取り消し済み (`3`)、失敗 (`4`)、保留中 (`5`)、予期しない終了 (`6`)、成功 (`7`)、停止 (`8`)、および完了 (`9`) です。|  
|caller_sid|**varbinary(85)**|ログオンに Windows 認証が使用された場合はユーザーのセキュリティ ID (SID)。|  
|caller_name|**nvarchar(128)**|操作を実行したアカウントの名前。|  
|process_id|**int**|外部プロセスのプロセス ID (該当する場合)。|  
|stopped_by_sid|**varbinary(85)**|操作を停止したユーザーの SID。|  
|stopped_by_name|**nvarchar(128)**|操作を停止したユーザーの名前。|  
|server_name|**nvarchar(128)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の指定されたインスタンスに関する Windows サーバーとインスタンスの情報。|  
|machine_name|**nvarchar(128)**|サーバー インスタンスが稼働しているコンピューターの名前。|  
|dump_id|**uniqueidentifier**|実行ダンプの ID。|  
  
## <a name="remarks"></a>Remarks  
 このビューは、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログの各検証に対して 1 つの行を表示します。  
  
## <a name="permissions"></a>アクセス許可  
 このビューには、次の権限のいずれかが必要です。  
  
-   対応する操作に対する READ 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
> [!NOTE]  
>  サーバー上で操作を実行する権限がある場合は、操作に関する情報を表示する権限もあります。 行レベルのセキュリティが適用されるため、表示する権限がある行のみが表示されます。  
  
  
