---
title: sp_add_operator (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_operator
- sp_add_operator_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_operator
ms.assetid: 817cd98a-4dff-4ed8-a546-f336c144d1e0
author: stevestein
ms.author: sstein
ms.openlocfilehash: f410024e1458d20e436df72cc2978ce41b5d60df
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095510"
---
# <a name="sp_add_operator-transact-sql"></a>sp_add_operator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  警告およびジョブで使用するオペレーター (通知受信者) を作成します。  
  
 
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_add_operator [ @name = ] 'name'   
     [ , [ @enabled = ] enabled ]   
     [ , [ @email_address = ] 'email_address' ]   
     [ , [ @pager_address = ] 'pager_address' ]   
     [ , [ @weekday_pager_start_time = ] weekday_pager_start_time ]   
     [ , [ @weekday_pager_end_time = ] weekday_pager_end_time ]   
     [ , [ @saturday_pager_start_time = ] saturday_pager_start_time ]   
     [ , [ @saturday_pager_end_time = ] saturday_pager_end_time ]   
     [ , [ @sunday_pager_start_time = ] sunday_pager_start_time ]   
     [ , [ @sunday_pager_end_time = ] sunday_pager_end_time ]   
     [ , [ @pager_days = ] pager_days ]   
     [ , [ @netsend_address = ] 'netsend_address' ]   
     [ , [ @category_name = ] 'category' ]   
```  
  
## <a name="arguments"></a>引数  
オペレーター (通知受信者) の名前 `[ @name = ] 'name'` ます。 この名前は一意である必要があり、パーセント ( **%** ) 文字を含めることはできません。 *名前*は**sysname**,、既定値はありません。  
  
`[ @enabled = ] enabled` 演算子の現在の状態を示します。 *有効*になっているは**tinyint**,、既定値は**1** (有効) です。 **0**の場合、オペレーターは無効になり、通知を受信しません。  
  
オペレーターの電子メールアドレスを `[ @email_address = ] 'email_address'` します。 この文字列はメール システムに直接渡されます。 *email_address*は**nvarchar (100)** ,、既定値は NULL です。  
  
 *Email_address*には、物理電子メールアドレスまたはエイリアスを指定できます。 例 :  
  
 '**jdoe**' または '**jdoe\@xyz.com**'  
  
> [!NOTE]  
>  データベース メールには電子メール アドレスを使用する必要があります。  
  
オペレーターのポケットベルアドレスを `[ @pager_address = ] 'pager_address'` します。 この文字列はメール システムに直接渡されます。 *pager_address*は**nvarchar (100)** ,、既定値は NULL です。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが平日の月曜日から金曜日までの、指定されたオペレーターにポケットベルによる通知を送信するまでの時間を `[ @weekday_pager_start_time = ] weekday_pager_start_time` します。 *weekday_pager_start_time*は**int**,、既定値は**090000**,、9:00 A.M. を示す を 24 時間形式で表したものです。HHMMSS 形式で入力する必要があります。  
  
月曜日から金曜日までの平日に、 **SQLServerAgent**サービスが、指定されたオペレーターにポケットベルによる通知を送信しなくなる時刻を `[ @weekday_pager_end_time = ] weekday_pager_end_time` します。 *weekday_pager_end_time*は**int**,、既定値は 18万,、6:00 pm を示す を 24 時間形式で表したものです。HHMMSS 形式で入力する必要があります。  
  
土曜日に、 **SQLServerAgent**サービスが、指定されたオペレーターにポケットベルによる通知を送信するまでの時間を `[ @saturday_pager_start_time = ] saturday_pager_start_time` します。 *saturday_pager_start_time*は**int**,、既定値は 090000,、9:00 A.M. を示す を 24 時間形式で表したものです。HHMMSS 形式で入力する必要があります。  
  
土曜日に、 **SQLServerAgent**サービスが、指定されたオペレーターにポケットベルによる通知を送信しなくなる時刻を `[ @saturday_pager_end_time = ] saturday_pager_end_time` します。 *saturday_pager_end_time*は**int**,、既定値は**18万**,、6:00 pm を示す を 24 時間形式で表したものです。HHMMSS 形式で入力する必要があります。  
  
毎週日曜日に、 **SQLServerAgent**サービスが、指定されたオペレーターにポケットベルによる通知を送信するまでの時間を `[ @sunday_pager_start_time = ] sunday_pager_start_time` します。 *sunday_pager_start_time*は**int**,、既定値は**090000**,、9:00 A.M. を示す を 24 時間形式で表したものです。HHMMSS 形式で入力する必要があります。  
  
毎週日曜日に、 **SQLServerAgent**サービスが、指定されたオペレーターにポケットベルによる通知を送信しなくなる時刻を `[ @sunday_pager_end_time = ] sunday_pager_end_time` します。 *sunday_pager_end_time*は**int**,、既定値は**18万**,、6:00 pm を示す を 24 時間形式で表したものです。HHMMSS 形式で入力する必要があります。  
  
`[ @pager_days = ] pager_days` は、指定された開始/終了時刻に従って、ページでオペレーターが使用できる日数を示す数値です。 *pager_days*は**tinyint**,、既定値は**0**の場合、操作がページを受信できないことを示します。 有効な値は**0** ~ **127**です。 *pager_days*は、必要な日数の個々の値を加算することによって計算されます。 たとえば、月曜日から金曜日までは**2**+**4**+**8**+**16**+**32** = **62**になります。 次の表は、各曜日の値を示しています。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**1**|日曜日|  
|**2**|月曜日|  
|**4**|火曜日|  
|**8**|水曜日|  
|**16**|木曜日|  
|**32**|金曜日|  
|**64**|土曜日|  
  
ネットワークメッセージを送信するオペレーターのネットワークアドレスを `[ @netsend_address = ] 'netsend_address'` します。 *netsend_address*は**nvarchar (100)** ,、既定値は NULL です。  
  
このオペレーターのカテゴリの名前 `[ @category_name = ] 'category'` ます。 *category*は**sysname**,、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 [InclusionThresholdSetting]  
  
## <a name="remarks"></a>Remarks  
 **sp_add_operator**は、 **msdb**データベースから実行する必要があります。  
  
 ページングは電子メールシステムでサポートされています。ページングを使用する場合は、電子メールとポケットベルの機能が必要です。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] は、ジョブを簡単に管理できるグラフィカルなツールです。ジョブのインフラストラクチャを作成し、管理するには、このツールを使用することをお勧めします。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_add_operator**を実行できるのは、 **sysadmin**固定サーバーロールのメンバーだけです。  
  
## <a name="examples"></a>使用例  
 次の例では、`danwi` に対してオペレーター情報を設定します。 オペレーターは有効になっています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは、月曜日から金曜日の午前 8 時から午後 5 時まで、 ポケットベルによる通知を送信します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_operator  
    @name = N'Dan Wilson',  
    @enabled = 1,  
    @email_address = N'danwi',  
    @pager_address = N'5551290AW@pager.Adventure-Works.com',  
    @weekday_pager_start_time = 080000,  
    @weekday_pager_end_time = 170000,  
    @pager_days = 62 ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [transact-sql &#40;  の&#41; sp_delete_operator](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)  
 [transact-sql &#40;  の&#41; sp_help_operator](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)  
 [transact-sql &#40;  の&#41; sp_update_operator](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
