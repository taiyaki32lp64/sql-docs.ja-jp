---
title: sp_polybase_join_group |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sp_polybase_join_group
helpviewer_keywords:
- PolyBase
ms.assetid: 48066431-fed2-4a8a-85af-ac704689e183
author: rothja
ms.author: jroth
ms.openlocfilehash: ba22ffe282e6b4248ed58bed850bc6ac08255df5
ms.sourcegitcommit: 710d60e7974e2c4c52aebe36fceb6e2bbd52727c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/11/2019
ms.locfileid: "72278113"
---
# <a name="sp_polybase_join_group-transact-sql"></a>sp_polybase_join_group (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  スケールアウト計算用に PolyBase グループにコンピューティングノードとして SQL Server インスタンスを追加します。  
  
 SQL Server インスタンスに[PolyBase](../../relational-databases/polybase/polybase-guide.md)機能がインストールされている必要があります。  PolyBase を使用すると、Hadoop や Azure blob ストレージなどの非 SQL Server データソースを統合できます。 「 [Sp_polybase_leave_group &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-leave-group.md)」も参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sp_polybase_join_group (@head_node_address = N'head_node_address',  
    @dms_control_channel_port = dms_control_channel_port,  
    @head_node_sql_server_instance_name = head_node_sql_server_instance_name)  
[ ; ]          
```  
  
## <a name="arguments"></a>引数  
 *\@head_node_address* = N '*head_node_address*'  
 PolyBase スケールアウトグループの SQL Server ヘッドノードをホストするコンピューターの名前。 *\@head_node_address*は nvarchar (255) です。  
  
 *\@dms_control_channel_port* = dms_control_channel_port  
 ヘッドノード PolyBase Data Movement サービスのコントロールチャネルが実行されているポート。 *\@dms_control_channel_port*は、署名されていない __int16 です。 既定値は**16450**です。  
  
 *\@head_node_sql_server_instance_name* = head_node_sql_server_instance_name  
 PolyBase スケールアウトグループのヘッドノード SQL Server インスタンスの名前。 *\@head_node_sql_server_instance_name*は nvarchar (16) です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="permissions"></a>アクセス許可  
 CONTROL SERVER 権限が必要です。  
  
## <a name="remarks"></a>Remarks  
 ストアドプロシージャを実行した後、PolyBase エンジンをシャットダウンし、マシン上の PolyBase Data Movement サービスを再起動します。 検証するには、ヘッドノードで次の DMV を実行します: **dm_exec_compute_nodes**。  
  
## <a name="example"></a>例  
 この例では、現在のコンピューターを計算ノードとして PolyBase グループに参加させます。  ヘッドノードの名前は**HST01**で、ヘッドノード上の SQL Server インスタンスの名前は**MSSQLSERVER**です。  
  
```  
EXEC sp_polybase_join_group N'HST01', 16450, N'MSSQLSERVER'   
```  
  
## <a name="see-also"></a>参照  
 [PolyBase の概要](../../relational-databases/polybase/get-started-with-polybase.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
