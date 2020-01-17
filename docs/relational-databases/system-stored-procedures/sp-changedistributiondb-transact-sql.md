---
title: sp_changedistributiondb (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changedistributiondb_TSQL
- sp_changedistributiondb
helpviewer_keywords:
- sp_changedistributiondb
ms.assetid: 66f73185-ea9e-43f9-86ed-9dd933cee2f6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9db4f3a40311e94d94d8910f4d1625f89f29926a
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768961"
---
# <a name="spchangedistributiondb-transact-sql"></a>sp_changedistributiondb (Transact-sql)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  ディストリビューション データベースのプロパティを変更します。 このストアドプロシージャは、ディストリビューター側で任意のデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_changedistributiondb [ @database= ] 'database'   
    [ , [ @property= ] 'property' ]   
    [ , [ @value= ] 'value' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @database = ] 'database'`ディストリビューションデータベースの名前を指定します。 *データベースのデータ*型は**sysname**で、既定値はありません。  
  
`[ @property = ] 'property'`特定のデータベースに対して変更するプロパティを指定します。 *プロパティ*は**sysname**で、次のいずれかの値を指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**history_retention**|履歴テーブルの保持期間です。|  
|**max_distretention**|ディストリビューションの最大保有期間。|  
|**min_distretention**|ディストリビューションの最小保有期間。|  
|NULL (既定値)|使用可能なすべての*プロパティ*値が出力されます。|  
  
`[ @value = ] 'value'`指定したプロパティの新しい値を指定します。 *値*は**nvarchar (255)** ,、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_changedistributiondb**は、すべての種類のレプリケーションで使用されます。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_changedistributiondb](../../relational-databases/replication/codesnippet/tsql/sp-changedistributiondb-_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_changedistributiondb**を実行できるのは、 **sysadmin**固定サーバーロールのメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [View and Modify Distributor and Publisher Properties (ディストリビューターとパブリッシャーのプロパティの表示および変更)](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistributiondb &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)   
 [sp_dropdistributiondb &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md)   
 [sp_helpdistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
