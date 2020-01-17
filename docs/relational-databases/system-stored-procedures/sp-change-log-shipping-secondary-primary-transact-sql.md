---
title: sp_change_log_shipping_secondary_primary (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_change_log_shipping_secondary_primary
- sp_change_log_shipping_secondary_primary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_log_shipping_secondary_primary
ms.assetid: 5bcb4df7-6df3-4f2b-9207-b97b5addf2a6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 757d842dfe0521bd8195bf85e02a3ed0eee2b5b5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68045806"
---
# <a name="spchangelogshippingsecondaryprimary-transact-sql"></a>sp_change_log_shipping_secondary_primary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  セカンダリ データベースの設定を変更します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_change_log_shipping_secondary_primary  
[ @primary_server = ] 'primary_server',  
[ @primary_database = ] 'primary_database',  
[, [ @backup_source_directory = ] 'backup_source_directory']  
[, [ @backup_destination_directory = ] 'backup_destination_directory']  
[, [ @file_retention_period = ] file_retention_period]  
[, [ @monitor_server_security_mode = ] monitor_server_security_mode]  
[, [ @monitor_server_login = ] 'monitor_server_login']  
[, [ @monitor_server_password = ] 'monitor_server_password']  
```  
  
## <a name="arguments"></a>引数  
`[ @primary_server = ] 'primary_server'` プライマリ インスタンスの名前、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]ログ配布構成にします。 *primary_server*は**sysname** NULL にすることはできません。  
  
`[ @primary_database = ] 'primary_database'` プライマリ サーバー上のデータベースの名前です。 *primary_database*は**sysname**、既定値はありません。  
  
`[ @backup_source_directory = ] 'backup_source_directory'` プライマリ サーバーからのトランザクション ログ バックアップ ファイルの保存先ディレクトリ。 *backup_source_directory*は**nvarchar (500)** NULL にすることはできません。  
  
`[ @backup_destination_directory = ] 'backup_destination_directory'` バックアップ ファイルがコピー先のセカンダリ サーバー上のディレクトリ。 *backup_destination_directory*は**nvarchar (500)** NULL にすることはできません。  
  
`[ @file_retention_period = ] 'file_retention_period'` 分の履歴を保持する時間の長さです。 *history_retention_period*は**int**、既定値は NULL です。 指定されていない場合、値 14420 が使用されます。  
  
`[ @monitor_server_security_mode = ] 'monitor_server_security_mode'` 監視サーバーへの接続に使用されるセキュリティ モード。  
  
 1 = Windows 認証です。  
  
 0 =[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証します。 *monitor_server_security_mode*は**ビット**NULL にすることはできません。  
  
`[ @monitor_server_login = ] 'monitor_server_login'` 監視サーバーへのアクセスに使用するアカウントの username です。  
  
`[ @monitor_server_password = ] 'monitor_server_password'` 監視サーバーへのアクセスに使用するアカウントのパスワードです。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>コメント  
 **sp_change_log_shipping_secondary_primary**から実行する必要があります、**マスター**セカンダリ サーバー上のデータベース。 このストアド プロシージャでは次の処理が行われます。  
  
1.  設定を変更、 **log_shipping_secondary**に応じてを記録します。  
  
2.  変更が内のレコードを監視して、監視サーバーがセカンダリ サーバーと異なる場合は、 **log_shipping_monitor_secondary**モニターでサーバーを使用して、指定された引数に必要な場合。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールは、この手順を実行できます。  
  
## <a name="see-also"></a>関連項目  
 [ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
