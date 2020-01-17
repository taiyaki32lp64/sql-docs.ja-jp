---
title: fn_syscollector_get_execution_details (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_syscollector_get_execution_details_TSQL
- fn_syscollector_get_execution_details
dev_langs:
- TSQL
helpviewer_keywords:
- fn_syscollector_get_execution_details function
ms.assetid: d59ddf0c-72c0-4c57-bc83-aef260e4e105
author: rothja
ms.author: jroth
ms.openlocfilehash: b2ed385026d2bd47912a1a95d237b2adedafa26d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68042821"
---
# <a name="fnsyscollectorgetexecutiondetails-transact-sql"></a>fn_syscollector_get_execution_details (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssIS](../../includes/ssis-md.md)] ログ (sysssislog) で、指定されたパッケージの package_execution_id と一致する部分を返します。 テーブルには、パッケージ、タスク、およびコンテナーによって実行時に生成される各ログ エントリの 1 つの行が含まれています。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
fn_syscollector_get_execution_details ( log_id )  
```  
  
## <a name="arguments"></a>引数  
 *log_id*  
 実行ログの一意なローカル識別子を指定します。 *log_id*は**int**します。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|id|**int**|ログ エントリの一意の識別子。|  
|イベント|**sysname**|ログ エントリを生成したイベントの名前。|  
|コンピューター|**nvarchar**|ログ エントリの生成時にパッケージが実行されていたコンピューター。|  
|演算子 (operator)|**nvarchar**|ユーザーまたはしたパッケージを実行するエージェントのユーザー名は、ログ エントリを生成します。|  
|source|**nvarchar**|ログ エントリを生成する実行可能ファイルの名前。|  
|sourceid|**uniqueidentifier**|ログ エントリを生成する実行可能ファイルの GUID です。|  
|executionid|**uniqueidentifier**|ログ エントリを生成する実行可能ファイルの実行インスタンスの GUID です。|  
|開始時刻|**datetime**|パッケージの実行を開始した時刻。|  
|終了時刻|**datetime**|パッケージが完了した時刻。|  
|datacode|**int**|ログ エントリに関連付けられたイベントを識別する整数値。 「0」は、イベントに識別子が指定されていないことを示します。|  
|databytes|**image**|戻り値を識別するバイト配列。|  
|メッセージ|**nvarchar**|イベントとイベントに関連付けられている情報の説明。|  
  
## <a name="permissions"></a>アクセス許可  
 に対する SELECT 権限が必要です**dc_operator**します。  
  
## <a name="see-also"></a>関連項目  
 [パッケージの SQL Server データ ツールにログ記録を有効にします。](../../integration-services/performance/integration-services-ssis-logging.md#server_logging)   
 [[データ コレクション]](../../relational-databases/data-collection/data-collection.md)  
  
  
