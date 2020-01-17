---
title: sysssislog (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdtslog90_TSQL
- sysdtslog90
dev_langs:
- TSQL
helpviewer_keywords:
- sysssislog system table
ms.assetid: 7fa288a1-81e3-42a0-82f6-8a59019693d0
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: d837049f36e4f7925f8e62a18987f51235f19c14
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029609"
---
# <a name="sysssislog-transact-sql"></a>sysssislog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  実行時に、パッケージ、タスク、およびコンテナーによって生成される各ログ エントリの 1 つの行が含まれています。 このテーブルは、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] をインストールするときに msdb データベースに作成されます。 ログ記録が別の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに記録されるように構成する場合、ここで説明する形式の sysssislog テーブルが、指定されたデータベースに作成されます。  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] このテーブルにログ エントリを書き込みます**のみ**パッケージを使用すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログ プロバイダー。  
  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|id|**int**|ログ エントリの一意の識別子。|  
|event|**sysname**|ログ エントリを生成したイベントの名前。|  
|computer|**nvarchar**|ログ エントリの生成時にパッケージが実行されていたコンピューター。|  
|operator|**nvarchar**|パッケージを実行したユーザーのユーザー名は、ログ エントリを生成します。|  
|source|**nvarchar**|ログ エントリを生成すると、パッケージの実行可能ファイルの名前。|  
|sourceid|**uniqueidentifier**|ログ エントリを生成したパッケージ内の実行可能ファイルの GUID。|  
|executionid|**uniqueidentifier**|ログ エントリを生成する実行可能ファイルの実行インスタンスの GUID です。|  
|starttime|**datetime**|パッケージの実行が開始された時刻。|  
|endtime|**datetime**|パッケージが完了した時刻。<br /><br /> この機能は実装されていません。 Endtime 列の値は、starttime 列の値と同じでは常にします。|  
|datacode|**int**|通常、コンテナーまたはタスクの実行結果を示す省略可能な整数値。|  
|databytes|**image**|追加情報を格納しているバイト配列 (省略可能)。|  
|message|**nvarchar**|イベントとイベントに関連付けられている情報の説明。|  
  
## <a name="see-also"></a>関連項目  
 [Integration Services &#40;SSIS&#41; のログ記録](../../integration-services/performance/integration-services-ssis-logging.md)   
  
  
