---
title: sp_changesubscriptiondtsinfo (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changesubscriptiondtsinfo
- sp_changesubscriptiondtsinfo_TSQL
helpviewer_keywords:
- sp_changesubscriptiondtsinfo
ms.assetid: 64fc085f-f81b-493b-b59a-ee6192d9736d
author: stevestein
ms.author: sstein
ms.openlocfilehash: a091df0cbbeb2883ff9905d7c5b3718d50efa86b
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68762548"
---
# <a name="spchangesubscriptiondtsinfo-transact-sql"></a>sp_changesubscriptiondtsinfo (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  サブスクリプションのデータ変換サービス (DTS) パッケージのプロパティを変更します。 このストアドプロシージャは、サブスクライバー側のサブスクリプションデータベースで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_changesubscriptiondtsinfo [ [ @job_id = ] job_id ]  
    [ , [ @dts_package_name= ] 'dts_package_name' ]  
    [ , [ @dts_package_password= ] 'dts_package_password' ]  
    [ , [ @dts_package_location= ] 'dts_package_location' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @job_id = ] job_id`プッシュサブスクリプションのディストリビューションエージェントのジョブ ID を示します。 *job_id*は**varbinary (16)** ,、既定値はありません。 配布ジョブ ID を検索するには、 **sp_helpsubscription**または**sp_helppullsubscription**を実行します。  
  
`[ @dts_package_name = ] 'dts_package_name'`DTS パッケージの名前を指定します。 *dts_package_name*は**sysname**,、既定値は NULL です。 たとえば、 **DTSPub_Package**という名前のパッケージを指定するには`@dts_package_name = N'DTSPub_Package'`、を指定します。  
  
`[ @dts_package_password = ] 'dts_package_password'`パッケージのパスワードを指定します。 *dts_package_password*は**sysname**既定値は NULL です。これは、password プロパティを変更せずに残すことを指定します。  
  
> [!NOTE]  
>  DTS パッケージには、パスワードが必要です。  
  
`[ @dts_package_location = ] 'dts_package_location'`パッケージの場所を指定します。 *dts_package_location*は**nvarchar (12)** ,、既定値は NULL の場合、パッケージの場所を変更しないことを指定します。 パッケージの場所は、**ディストリビューター**または**サブスクライバー**に変更できます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_changesubscriptiondtsinfo**は、プッシュサブスクリプションのみのスナップショットレプリケーションおよびトランザクションレプリケーションに使用されます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_changesubscriptiondtsinfo**を実行できるのは、 **sysadmin**固定サーバーロールのメンバー、 **db_owner**固定データベースロールのメンバー、またはサブスクリプションの作成者だけです。  
  
## <a name="see-also"></a>関連項目  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
