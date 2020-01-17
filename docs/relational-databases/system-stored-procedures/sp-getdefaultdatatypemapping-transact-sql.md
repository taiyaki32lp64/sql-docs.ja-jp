---
title: sp_getdefaultdatatypemapping (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_getdefaultdatatypemapping_TSQL
- sp_getdefaultdatatypemapping
helpviewer_keywords:
- sp_getdefaultdatatypemapping
ms.assetid: b8401de1-f135-41d0-ba79-ce8fe1f48c00
author: stevestein
ms.author: sstein
ms.openlocfilehash: 32fe9edf5c3d8621046a27937d83f642b1689d1a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68123991"
---
# <a name="spgetdefaultdatatypemapping-transact-sql"></a>sp_getdefaultdatatypemapping (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定したデータ型の間の既定のマッピングに関する情報を返します[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース管理システム (DBMS)。 このストアド プロシージャは、ディストリビューターのすべてのデータベースで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_getdefaultdatatypemapping [ @source_dbms = ] 'source_dbms'   
    [ , [ @source_version = ] 'source_version' ]  
        , [ @source_type = ] 'source_type'    
    [ , [ @source_length = ] source_length ]  
    [ , [ @source_precision = ] source_precision ]  
    [ , [ @source_scale = ] source_scale ]  
    [ , [ @source_nullable = ] source_nullable ]  
        , [ @destination_dbms = ] 'destination_dbms'   
    [ , [ @destination_version = ] 'destination_version' ]  
    [ , [ @destination_type = ] 'destination_type' OUTPUT ]  
    [ , [ @destination_length = ] destination_length OUTPUT ]  
    [ , [ @destination_precision = ] destination_precision OUTPUT ]  
    [ , [ @destination_scale = ] destination_scale OUTPUT ]  
    [ , [ @destination_nullable = ] source_nullable OUTPUT ]  
    [ , [ @dataloss = ] dataloss OUTPUT ]  
```  
  
## <a name="arguments"></a>引数  
`[ @source_dbms = ] 'source_dbms'` データ型のマップ元 DBMS の名前です。 *source_dbms*は**sysname**値は次のいずれかを指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**MSSQLSERVER**|ソースが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース。|  
|**ORACLE**|マップ元は Oracle データベース。|  
  
 このパラメーターを指定する必要があります。  
  
`[ @source_version = ] 'source_version'` マップ元 DBMS のバージョン番号です。 *source_version*は**varchar (10)** 既定値は NULL です。  
  
`[ @source_type = ] 'source_type'` マップ元 DBMS のデータ型です。 *source_type*は**sysname**、既定値はありません。  
  
`[ @source_length = ] source_length` マップ元 DBMS でのデータ型の長さです。 *source_length*は**bigint**既定値は NULL です。  
  
`[ @source_precision = ] source_precision` マップ元 DBMS でのデータ型の有効桁数です。 *source_precision*は**bigint**既定値は NULL です。  
  
`[ @source_scale = ] source_scale` マップ元 DBMS でのデータ型の小数点以下桁数です。 *source_scale*は**int**既定値は NULL です。  
  
`[ @source_nullable = ] source_nullable` マップ元 DBMS でのデータ型が NULL の値をサポートするかどうかです。 *source_nullable*は**ビット**の既定値を持つ**1**NULL 値がサポートされていることを意味します。  
  
`[ @destination_dbms = ] 'destination_dbms'` マップ先 DBMS の名前です。 *destination_dbms*は**sysname**値は次のいずれかを指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**MSSQLSERVER**|マップ先は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース。|  
|**ORACLE**|変換先は、Oracle データベースです。|  
|**DB2**|マップ先は IBM DB2 データベース。|  
|**SYBASE**|変換先は、Sybase データベース。|  
  
 このパラメーターを指定する必要があります。  
  
`[ @destination_version = ] 'destination_version'` マップ先 DBMS の製品バージョンです。 *destination_version*は**varchar (10)** 既定値は NULL です。  
  
`[ @destination_type = ] 'destination_type' OUTPUT` マップ先 DBMS のデータ型が表示されます。 *destination_type*は**sysname**既定値は NULL です。  
  
`[ @destination_length = ] destination_length OUTPUT` マップ先 DBMS でのデータ型の長さです。 *destination_length*は**bigint**既定値は NULL です。  
  
`[ @destination_precision = ] destination_precision OUTPUT` マップ先 DBMS でのデータ型の有効桁数です。 *destination_precision*は**bigint**既定値は NULL です。  
  
`[ @destination_scale = ] _destination_scaleOUTPUT` マップ先 DBMS でのデータ型の小数点以下桁数です。 *destination_scale*は**int**既定値は NULL です。  
  
`[ @destination_nullable = ] _destination_nullableOUTPUT` マップ先 DBMS でのデータ型が NULL の値をサポートするかどうかです。 *destination_nullable*は**ビット**既定値は NULL です。 **1** NULL 値がサポートされていることを意味します。  
  
`[ @dataloss = ] _datalossOUTPUT` マッピングにデータ損失の可能性です。 *データ損失*は**ビット**既定値は NULL です。 **1**データ損失の可能性があることを意味します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_getdefaultdatatypemapping**はすべての種類の間のレプリケーションで使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]DBMS します。  
  
 **sp_getdefaultdatatypemapping**既定のマッピング先データである型指定されたソースのデータ型に最も近い一致を返します。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールが実行できる**sp_getdefaultdatatypemapping**します。  
  
## <a name="see-also"></a>関連項目  
 [sp_helpdatatypemap &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)   
 [sp_setdefaultdatatypemapping &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md)   
 [Data Type Mapping for Oracle Publishers](../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md)   
 [Oracle サブスクライバー](../../relational-databases/replication/non-sql/oracle-subscribers.md)  
  
  
