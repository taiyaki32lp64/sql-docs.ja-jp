---
title: sys.sp_cdc_scan (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_cdc_scan_TSQL
- sp_cdc_scan
- sys.sp_cdc_scan
- sp_cdc_scan_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_scan
ms.assetid: 46e4294c-97b8-47d6-9ed9-b436a9929353
author: rothja
ms.author: jroth
ms.openlocfilehash: a064b49df3f45d9cbc4b148b8d78c3661f9a2bcc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68066734"
---
# <a name="sysspcdcscan-transact-sql"></a>sys.sp_cdc_scan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  変更データ キャプチャのログ スキャン操作を実行します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.sp_cdc_scan [ [ @maxtrans = ] max_trans ]   
     [ , [ @maxscans = ] max_scans ]   
     [ , [ @continuous = ] continuous ]   
     [ , [ @pollinginterval = ] polling_interval ]   
```  
  
## <a name="arguments"></a>引数  
`[ @maxtrans = ] max_trans` 各スキャン サイクルで処理するトランザクションの最大数。 *max_trans*は**int**既定値は 500 です。  
  
`[ @maxscans = ] max_scans` ログからすべての行を抽出するために実行するスキャン サイクルの最大数。 *max_scans*は**int**既定値は 10 です。  
  
`[ @continuous = ] continuous` ストアド プロシージャが単一のスキャン サイクル (0) 後に終了する必要があるかどうか、または連続して実行で指定された時間一時停止かどうかを示す*polling_interval*してスキャン サイクル (1) する前にします。 *継続的な*は**tinyint**既定値は 0。  
  
`[ @pollinginterval = ] polling_interval` ログ スキャン サイクルの間隔の秒数です。 *polling_interval*は**bigint**既定値は 0。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>コメント  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのキャプチャ ジョブが変更データ キャプチャによって使用されている場合、sys.sp_cdc_scan は sys.sp_MScdc_capture_job によって内部的に呼び出されます。 変更データ キャプチャのログ スキャン操作が既にアクティブである場合、またはデータベースのトランザクション レプリケーションが有効になっている場合は、プロシージャは明示的に実行できません。 自動的に構成されているキャプチャ ジョブの動作をカスタマイズする管理者によってこのストアド プロシージャを使用する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 db_owner 固定データベース ロールのメンバーシップが必要です。  
  
## <a name="see-also"></a>関連項目  
 [dbo.cdc_jobs &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)  
  
  
