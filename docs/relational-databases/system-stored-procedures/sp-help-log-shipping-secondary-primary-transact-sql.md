---
title: sp_help_log_shipping_secondary_primary (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_log_shipping_secondary_primary
- sp_help_log_shipping_secondary_primary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_secondary_primary
ms.assetid: 1310fdaf-edb5-4294-9739-7fb37c2c2cb5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 16753620fa4185d3f488db340aeb4858c28f6d69
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68066759"
---
# <a name="sphelplogshippingsecondaryprimary-transact-sql"></a>sp_help_log_shipping_secondary_primary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  セカンダリ サーバーにある指定されたプライマリ データベースの設定を取得します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_log_shipping_secondary_primary  
[ @primary_server = ] 'primary_server' OR  
[ @primary_database = ] 'primary_database'  
```  
  
## <a name="arguments"></a>引数  
`[ @primary_server = ] 'primary_server'` プライマリ インスタンスの名前、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]ログ配布構成にします。 *primary_server*は**sysname** NULL にすることはできません。  
  
`[ @primary_database = ] 'primary_database'` プライマリ サーバー上のデータベースの名前です。 *primary_database*は**sysname**、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 結果セットには、列が含まれています**secondary_id**、 **primary_server**、 **primary_database**、 **backup_source_directory**、 。**backup_destination_directory**、 **file_retention_period**、 **copy_job_id**、 **restore_job_id**、 **monitor_server**、 **monitor_server_security_mode**から**log_shipping_secondary**します。  
  
## <a name="remarks"></a>コメント  
 **sp_help_log_shipping_secondary_primary**から実行する必要があります、**マスター**セカンダリ サーバー上のデータベース。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールは、この手順を実行できます。  
  
## <a name="see-also"></a>関連項目  
 [ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
