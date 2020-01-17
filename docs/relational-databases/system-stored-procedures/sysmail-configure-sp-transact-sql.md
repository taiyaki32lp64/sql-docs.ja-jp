---
title: sysmail_configure_sp (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_configure_sp_TSQL
- sysmail_configure_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_configure_sp
ms.assetid: 73b33c56-2bff-446a-b495-ae198ad74db1
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7984fba52f813644c9dcb25bca2beb123be85622
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017723"
---
# <a name="sysmailconfiguresp-transact-sql"></a>sysmail_configure_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  データベース メールの構成設定を変更します。 指定された構成設定**sysmail_configure_sp**全体に適用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンス。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sysmail_configure_sp [ [ @parameter_name = ] 'parameter_name' ]  
    [ , [ @parameter_value = ] 'parameter_value' ]  
    [ , [ @description = ] 'description' ]  
```  
  
## <a name="arguments"></a>引数  
 [ **@parameter_name** =] **'** _parameter_name_ **'**  
 変更するパラメーターの名前。  
  
 [ **@parameter_value** =] **'** _parameter_value_ **'**  
 パラメーターの新しい値を指定します。  
  
 [ **@description** =] **'** _説明_ **'**  
 パラメーターの説明。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>コメント  
 データベース メールでは次のパラメーターが使用されます。  
  
||||  
|-|-|-|  
|パラメーター名|説明|既定値|  
|*AccountRetryAttempts*|指定したプロファイル内の各アカウントを使用して、外部メール処理が電子メール メッセージの送信を試行する回数。|**1**|  
|*AccountRetryDelay*|外部メール処理が次回のメッセージ送信の試行を待機する時間 (秒単位)。|**5000**|  
|*DatabaseMailExeMinimumLifeTime*|外部メール処理がアクティブな状態にとどまる最小時間 (秒単位)。 データベース メールは、多くのメッセージを送信する場合は、データベース メールをアクティブにしておくし、頻繁な開始と停止のオーバーヘッドを回避するには、この値を大ききます。|**600**|  
|*DefaultAttachmentEncoding*|既定の電子メールの添付ファイルのエンコーディングします。|MIME|  
|*MaxFileSize*|添付ファイルの最大サイズ (バイト単位)。|**1000000**|  
|*ProhibitedExtensions*|電子メールへの添付ファイルとして送信できない拡張子のコンマ区切りのリスト。|**exe、dll、vbs、js**|  
|*LoggingLevel*|データベース メール ログに記録されるメッセージ。 数値の値は次のいずれか:<br /><br /> 1-これは、通常モードです。 エラーのみを記録します。<br /><br /> 2-拡張モード。 エラー、警告、および情報メッセージを記録します。<br /><br /> 3-これは、詳細モードです。 エラー、警告、情報メッセージ、成功メッセージ、およびその他の内部メッセージを記録します。 トラブルシューティングを行うには、このモードを使用してください。|**2**|  
  
 ストアド プロシージャ**sysmail_configure_sp**では、 **msdb**が所有するデータベースにあり、 **dbo**スキーマ。 現在のデータベースがない場合、3 つの部分の名前を持つプロシージャを実行する必要があります**msdb**します。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャの既定のメンバーへのアクセス許可を実行、 **sysadmin**固定サーバー ロール。  
  
## <a name="examples"></a>使用例  
 **A.各アカウントを 10 回再試行するデータベース メールを設定します。**  
  
 次の例では、到達できないアカウントを検討する前に各アカウントを 10 回再試行するデータベース メールの設定を示します。  
  
```  
EXECUTE msdb.dbo.sysmail_configure_sp  
    'AccountRetryAttempts', '10' ;  
```  
  
 **B.添付ファイルの最大サイズをメガバイト単位の 2 つに設定します。**  
  
 次の例では、添付ファイルの最大サイズを 2 MB に設定します。  
  
```  
EXECUTE msdb.dbo.sysmail_configure_sp  
    'MaxFileSize', '2097152' ;  
```  
  
## <a name="see-also"></a>関連項目  
 [データベース メール](../../relational-databases/database-mail/database-mail.md)   
 [sysmail_help_configure_sp &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-help-configure-sp-transact-sql.md)   
 [データベース メール ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
