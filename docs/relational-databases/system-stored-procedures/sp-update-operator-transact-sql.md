---
title: sp_update_operator (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_operator_TSQL
- sp_update_operator
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_operator
ms.assetid: 231750a6-4828-4d03-afe6-b91d38c42ed3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2a766ad74f42336612859c63cf42df654846ff96
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68084839"
---
# <a name="sp_update_operator-transact-sql"></a>sp_update_operator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  警告とジョブで使用するためには、オペレーター (通知受信者) に関する情報を更新します。  
  
   ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_update_operator   
     [ @name =] 'name'   
     [ , [ @new_name = ] 'new_name' ]   
     [ , [ @enabled = ] enabled]   
     [ , [ @email_address = ] 'email_address' ]  
     [ , [ @pager_address = ] 'pager_number']   
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
 [ @name=] '*名前*'  
 変更するオペレーターの名前を指定します。 *名前*は**sysname**、既定値はありません。  
  
 [ @new_name=] '*new_name*'  
 演算子の新しい名前。 この名前は一意である必要があります。 *新しい名前*は**sysname**、既定値は NULL です。  
  
 [ @enabled=] *enabled*  
 オペレーターの現在の状態を示す数値 (**1**現在有効になっている場合**0**いない場合)。 *有効になっている*は**tinyint**、既定値は NULL です。 有効でない場合、オペレーターは警告通知を受信しません。  
  
 [ @email_address=] '*email_address*'  
 オペレーターの電子メール アドレス。 この文字列はメール システムに直接渡されます。 *email_address*は**nvarchar (100)** 、既定値は NULL です。  
  
 [ @pager_address=] '*pager_number*'  
 オペレーターのポケットベル アドレス。 この文字列はメール システムに直接渡されます。 *pager_number*は**nvarchar (100)** 、既定値は NULL です。  
  
 [ @weekday_pager_start_time=] *weekday_pager_start_time*  
 ポケットベルによる通知できますを開始する、このオペレーターを月曜日から金曜日までから時間を指定します。 *weekday_pager_start_time*は**int**、既定値は null の場合、24 時間制の hhmmss で入力する必要があります。  
  
 [ @weekday_pager_end_time=] *weekday_pager_end_time*  
 月曜日から金曜日までの間で、指定したオペレーターに対してポケットベル通知を終了する時間を指定します。 *エージェント*は**int**、既定値は null の場合、24 時間制の hhmmss で入力する必要があります。  
  
 [ @saturday_pager_start_time=] *saturday_pager_start_time*  
 ポケットベルによる通知できますを開始する指定したオペレーターに対して毎週土曜日の時間を指定します。 *エージェント*は**int**、既定値は null の場合、24 時間制の hhmmss で入力する必要があります。  
  
 [ @saturday_pager_end_time=] *saturday_pager_end_time*  
 ポケットベルによる通知できませんを開始する指定したオペレーターに対して毎週土曜日の時間を指定します。 *@saturday_pager_end_time*は**int**、既定値は null の場合、24 時間制の hhmmss で入力する必要があります。  
  
 [ @sunday_pager_start_time=] *sunday_pager_start_time*  
 ポケットベルによる通知できますを開始する指定したオペレーターに対して毎週日曜日、時間を指定します。 *エージェント*は**int**、既定値は null の場合、24 時間制の hhmmss で入力する必要があります。  
  
 [ @sunday_pager_end_time=] *sunday_pager_end_time*  
 毎週日曜日に、指定したオペレーターに対してポケットベル通知を終了する時間を指定します。 *エージェント*は**int**、既定値は null の場合、24 時間制の hhmmss で入力する必要があります。  
  
 [ @pager_days=] *pager_days*  
 オペレーターがポケットベルの指定した開始/終了時間) を受信できる曜日を指定します。 *pager_days*は**tinyint**、既定値は null の場合、値を指定する必要がありますと**0**を通じて**127**。 *pager_days*必要となる曜日の個々 の値を加算して計算されます。 たとえば、月曜日から金曜日までからは**2**+**4**+**8**+**16** + **32** = **64**します。  
  
|値|説明|  
|-----------|-----------------|  
|**1**|日曜日|  
|**2**|月曜日|  
|**4**|火曜日|  
|**8**|水曜日|  
|**16**|木曜日|  
|**32**|金曜日|  
|**64**|土曜日|  
  
 [ @netsend_address=] '*netsend_address*'  
 ネットワーク メッセージを送信するオペレーターのネットワーク アドレス。 *netsend_address*は**nvarchar (100)** 、既定値は NULL です。  
  
 [ @category_name=] '*category*'  
 このアラートのカテゴリの名前。 *category*は**sysname**、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 sp_update_operator は、msdb データベースから実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 Sysadmin 固定サーバー ロールのメンバーにこのプロシージャの既定値を実行する権限。  
  
## <a name="examples"></a>使用例  
 次の例では、無効であったオペレーターの状態を有効に更新し、ポケットベルを受信できる曜日 (月曜～金曜日、 午前 8 時～午後 5 時) を設定します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_operator   
    @name = N'François Ajenstat',  
    @enabled = 1,  
    @email_address = N'françoisa',  
    @pager_address = N'5551290AW@pager.Adventure-Works.com',  
    @weekday_pager_start_time = 080000,  
    @weekday_pager_end_time = 170000,  
    @pager_days = 64 ;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [sp_add_operator &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [sp_delete_operator &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)   
 [sp_help_operator &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
