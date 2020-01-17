---
title: システムの要求 (_d) |Microsoft Docs
ms.custom: ''
ms.date: 10/28/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_external_script_requests
- sys.dm_external_script_requests_TSQL
- dm_external_script_requests
- dm_external_script_requests_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_external_script_requests dynamic management view
ms.assetid: e7e7c50f-b8b2-403c-b8c8-1955da5636c3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 33a7b546b9479add67a05f9bb7537f953fa2e9f9
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/24/2019
ms.locfileid: "68476274"
---
# <a name="sysdmexternalscriptrequests"></a>sys.dm_external_script_requests
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

外部スクリプトを実行しているアクティブなワーカー アカウントごとに行を返します。
  
> [!NOTE] 
>  
> この動的管理ビュー (DMV) は、外部スクリプトの実行をサポートする機能をインストールして有効にした場合にのみ使用できます。 詳細については、SQL Server 2017 以降の「 [SQL Server 2016 の R Services](../../advanced-analytics/r/sql-server-r-services.md) 」および「 [Machine Learning Services (r、Python)](../../advanced-analytics/what-is-sql-server-machine-learning.md)」を参照してください。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|external_script_request_id|**一意識別子**|外部スクリプト要求を送信したプロセスの ID です。 これは、によって受信されたプロセス ID に対応します。[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]|  
|language|**nvarchar**|サポートされているスクリプト言語を表すキーワードです。 |  
|degree_of_parallelism|**int**|作成された並列処理の数を示す数値です。 この値は、要求された並列処理の数と異なる場合があります。|  
|external_user_name|**nvarchar**|スクリプトが実行されたときの Windows ワーカー アカウント。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
> [!NOTE]
>   
>  外部スクリプトを実行するユーザーはさらに EXECUTE ANY EXTERNAL SCRIPT 権限も持っている必要がありますが、管理者はこの権限がなくてもこの DMV を使用できます。 
  
## <a name="remarks"></a>コメント  

このビューは、スクリプト言語の識別子を使用してフィルター処理することができます。

このビューはまた、スクリプトが実行されているワーカー アカウントも返します。 外部スクリプトによって使用されるワーカーアカウントの詳細については、 [SQL Server Machine Learning Services の機能拡張フレームワークのセキュリティの概要](../../advanced-analytics/concepts/security.md#sqlrusergroup)に関するトピックの「処理に使用される id」セクションを参照してください。

**external_script_request_id** フィールドに返される GUID はまた、一時ファイルが格納されている、セキュリティで保護されたディレクトリのファイル名も表します。 MSSQLSERVER01 などの各ワーカー アカウントは、単一の SQL ログインまたは Windows ユーザーを表します。複数のスクリプト要求を実行するために使用される場合があります。 既定では、これらの一時ファイルは、要求したスクリプトが完了するとクリーンアップされます。
 
この DMV は、アクティブなプロセスを監視するだけであり、既に完了しているスクリプトをレポートすることはできません。 スクリプトの期間を追跡する必要がある場合は、スクリプト内にタイミング情報を追加し、スクリプトの実行の一部としてキャプチャすることをお勧めします。

## <a name="examples"></a>使用例  
  
### <a name="viewing-the-currently-active-r-scripts-for-a-particular-process"></a>特定のプロセスで現在アクティブな R スクリプトを表示する 
 次の例では、現在のインスタンスで実行されている外部スクリプト実行の数を表示します。  
  
```  
SELECT external_script_request_id 
  , [language]
  , degree_of_parallelism
  , external_user_name
FROM sys.dm_external_script_requests; 
```  

[結果]  


external_script_request_id  |language  |degree_of_parallelism  |external_user_name  
---------|---------|---------|---------
183EE6FC-7399-4318-AA2E-7A6C68E435A8     |     R    |      1   |  MSSQLSERVER01       


  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [実行関連の動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
[sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)
[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)  
  

