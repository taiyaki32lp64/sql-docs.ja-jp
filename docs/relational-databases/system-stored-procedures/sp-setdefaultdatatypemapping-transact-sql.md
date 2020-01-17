---
title: sp_setdefaultdatatypemapping (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_setdefaultdatatypemapping
- sp_setdefaultdatatypemapping_TSQL
helpviewer_keywords:
- sp_setdefaultdatatypemapping
ms.assetid: 7394e8ca-4ce1-4e99-a784-205007c2c248
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9f0dfadc3b2b990d999df1d66069c4b68df9e6cf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104410"
---
# <a name="sp_setdefaultdatatypemapping-transact-sql"></a>sp_setdefaultdatatypemapping (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  既存のデータ型マッピングの間のマーク[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース管理システム (DBMS)、既定値として。 このストアド プロシージャは、ディストリビューターのすべてのデータベースで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_setdefaultdatatypemapping [ [ @mapping_id = ] mapping_id ]  
    [ , [ @source_dbms = ] 'source_dbms' ]  
    [ , [ @source_version = ] 'source_version' ]  
    [ , [ @source_type = ] 'source_type' ]   
    [ , [ @source_length_min = ] source_length_min ]  
    [ , [ @source_length_max = ] source_length_max ]  
    [ , [ @source_precision_min = ] source_precision_min ]  
    [ , [ @source_precision_max = ] source_precision_max ]  
    [ , [ @source_scale_min = ] source_scale_min ]  
    [ , [ @source_scale_max = ] source_scale_max ]  
    [ , [ @source_nullable = ] source_nullable ]  
    [ , [ @destination_dbms = ] 'destination_dbms' ]  
    [ , [ @destination_version = ] 'destination_version' ]  
    [ , [ @destination_type = ] 'destination_type' ]  
    [ , [ @destination_length = ] destination_length ]  
    [ , [ @destination_precision = ] destination_precision ]  
    [ , [ @destination_scale = ] destination_scale ]  
    [ , [ @destination_nullable = ] source_nullable ]  
```  
  
## <a name="arguments"></a>引数  
`[ @mapping_id = ] mapping_id` 既存のデータ型マッピングを識別します。  *mapping_id*は**int**既定値は NULL です。 指定した場合*mapping_id*、残りのパラメーターを行う必要はありません。  
  
`[ @source_dbms = ] 'source_dbms'` データ型のマップ元 DBMS の名前です。 *source_dbms*は**sysname**値は次のいずれかを指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**MSSQLSERVER**|ソースが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース。|  
|**ORACLE**|マップ元は Oracle データベース。|  
|NULL (既定値)||  
  
 場合、このパラメーターを指定する必要があります*mapping_id*は NULL です。  
  
`[ @source_version = ] 'source_version'` マップ元 DBMS のバージョン番号です。 *source_version*は**varchar (10)** 既定値は NULL です。  
  
`[ @source_type = ] 'source_type'` マップ元 DBMS のデータ型です。 *source_type*は**sysname**します。 場合、このパラメーターを指定する必要があります*mapping_id*は NULL です。  
  
`[ @source_length_min = ] source_length_min` マップ元 DBMS でのデータ型の最小の長さです。 *source_length_min*は**bigint**既定値は NULL です。  
  
`[ @source_length_max = ] source_length_max` マップ元 DBMS でのデータ型の最大の長さです。 *source_length_max*は**bigint**既定値は NULL です。  
  
`[ @source_precision_min = ] source_precision_min` マップ元 DBMS でのデータ型の最小有効桁数です。 *source_precision_min*は**bigint**既定値は NULL です。  
  
`[ @source_precision_max = ] source_precision_max` マップ元 DBMS でのデータ型の最大有効桁数です。 *source_precision_max*は**bigint**既定値は NULL です。  
  
`[ @source_scale_min = ] source_scale_min` マップ元 DBMS でのデータ型の最小小数点以下桁数です。 *source_scale_min*は**int**既定値は NULL です。  
  
`[ @source_scale_max = ] source_scale_max` マップ元 DBMS でのデータ型の最大小数点以下桁数です。 *source_scale_max*は**int**既定値は NULL です。  
  
`[ @source_nullable = ] source_nullable` マップ元 DBMS でのデータ型が NULL の値をサポートするかどうかです。 *source_nullable*は**ビット**既定値は NULL です。 **1** NULL 値がサポートされていることを意味します。  
  
`[ @destination_dbms = ] 'destination_dbms'` マップ先 DBMS の名前です。 *destination_dbms*は**sysname**値は次のいずれかを指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**MSSQLSERVER**|マップ先は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース。|  
|**ORACLE**|変換先は、Oracle データベースです。|  
|**DB2**|マップ先は IBM DB2 データベース。|  
|**SYBASE**|変換先は、Sybase データベース。|  
|NULL (既定値)||  
  
`[ @destination_version = ] 'destination_version'` マップ先 DBMS の製品バージョンです。 *destination_version*は**varchar (10)** 既定値は NULL です。  
  
`[ @destination_type = ] 'destination_type'` マップ先 DBMS のデータ型が表示されます。 *destination_type*は**sysname**既定値は NULL です。  
  
`[ @destination_length = ] destination_length` マップ先 DBMS でのデータ型の長さです。 *destination_length*は**bigint**既定値は NULL です。  
  
`[ @destination_precision = ] destination_precision` マップ先 DBMS でのデータ型の有効桁数です。 *destination_precision*は**bigint**既定値は NULL です。  
  
`[ @destination_scale = ] destination_scale` マップ先 DBMS でのデータ型の小数点以下桁数です。 *destination_scale*は**int**既定値は NULL です。  
  
`[ @destination_nullable = ] destination_nullable` マップ先 DBMS でのデータ型が NULL の値をサポートするかどうかです。 *destination_nullable*は**ビット**既定値は NULL です。 **1** NULL 値がサポートされていることを意味します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_setdefaultdatatypemapping**はすべての種類の間のレプリケーションで使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]DBMS します。  
  
 既定のデータ型マッピングは、指定した DBMS を含むすべてのレプリケーション トポロジに適用されます。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールが実行できる**sp_setdefaultdatatypemapping**します。  
  
## <a name="see-also"></a>関連項目  
 [Oracle パブリッシャーのデータ型マッピングの指定](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [sp_getdefaultdatatypemapping &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)   
 [sp_helpdatatypemap &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)  
  
  
