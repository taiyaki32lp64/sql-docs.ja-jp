---
title: sysmail_help_configure_sp (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_configure_sp
- sysmail_help_configure_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_configure_sp
ms.assetid: e598d4c8-3041-4965-b046-dce3a8e3d3e0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3d07f77c468bb14b28cd003f599bebd636d6f862
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056157"
---
# <a name="sysmail_help_configure_sp-transact-sql"></a>sysmail_help_configure_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  データベース メールの構成設定を表示します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sysmail_help_configure_sp  [ [ @parameter_name = ] 'parameter_name' ]  
```  
  
## <a name="arguments"></a>引数  
取得する構成設定の名前 `[ @parameter_name = ] 'parameter_name'` ます。 指定した場合、構成設定の値が **\@parameter_value**の出力パラメーターに返されます。 **\@parameter_name**が指定されていない場合、このストアドプロシージャは、インスタンス内のすべてのデータベースメール構成設定を含む結果セットを返します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 **\@parameter_name**が指定されていない場合、は次の列を含む結果セットを返します。  
  
||||  
|-|-|-|  
|列名|データ型|[説明]|  
|**paramname**|**nvarchar (256)**|構成パラメーターの名前。|  
|**paramvalue**|**nvarchar (256)**|構成パラメーターの値|  
|**description**|**nvarchar (256)**|構成パラメーターの説明|  
  
## <a name="remarks"></a>Remarks  
 ストアドプロシージャ**sysmail_help_configure_sp**には、インスタンスの現在のデータベースメール構成設定が一覧表示されます。  
  
 **\@parameter_name**が指定されていても、 **\@parameter_value**に出力パラメーターが指定されていない場合、このストアドプロシージャは出力を生成しません。  
  
 ストアドプロシージャ**sysmail_help_configure_sp**は**msdb**データベースにあり、 **dbo**スキーマが所有しています。 現在のデータベースが**msdb**でない場合は、3部構成の名前を使用してプロシージャを呼び出す必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャの実行権限は、既定では**sysadmin**固定サーバーロールのメンバーに与えています。  
  
## <a name="examples"></a>使用例  
 次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスのデータベースメール構成設定を一覧表示します。  
  
```  
EXECUTE msdb.dbo.sysmail_help_configure_sp ;  
```  
  
 次に結果セットを示します。行の長さは編集されています。  
  
```  
paramname                       paramvalue      description  
------------------------------- --------------- -----------------------------------------------------------------------------  
AccountRetryAttempts            1               Number of retry attempts for a mail server  
AccountRetryDelay               5000            Delay between each retry attempt to mail server  
DatabaseMailExeMinimumLifeTime  600             Minimum process lifetime in seconds  
DefaultAttachmentEncoding       MIME            Default attachment encoding  
LoggingLevel                    2               Database Mail logging level: normal - 1, extended - 2 (default), verbose - 3  
MaxFileSize                     1000000         Default maximum file size  
ProhibitedExtensions            exe,dll,vbs,js  Extensions not allowed in outgoing mails  
  
```  
  
## <a name="see-also"></a>参照  
 [データベース メール](../../relational-databases/database-mail/database-mail.md)   
 [ストアドプロシージャ&#40;のデータベースメール transact-sql&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
