---
title: sys.sysprotects (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysprotects
- sys.sysprotects_TSQL
- sys.sysprotects
- sysprotects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysprotects compatibility view
- sysprotects system table
ms.assetid: 49c9658d-fb51-4c77-94a0-fba699b0102d
author: rothja
ms.author: jroth
ms.openlocfilehash: ca403b5ad56386252d789ddede007a7293e59a40
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079237"
---
# <a name="syssysprotects-transact-sql"></a>sys.sysprotects (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  GRANT および DENY ステートメントを使用して、データベース内のセキュリティ アカウントに適用されているアクセス許可について説明します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|これらのアクセス許可を適用するオブジェクトの ID。|  
|**uid**|**smallint**|これらのアクセス許可を適用するユーザーまたはグループの ID。 オーバーフローまたはユーザーおよびロールの数が 32,767 を超える場合は NULL を返します。|  
|**action**|**tinyint**|次のアクセス許可のいずれかを設定できます。<br /><br /> 26 = REFERENCES<br /><br /> 178 = 関数の作成<br /><br /> 193 = SELECT<br /><br /> 195 = 挿入<br /><br /> 196 = DELETE<br /><br /> 197 = UPDATE<br /><br /> 198 = CREATE TABLE<br /><br /> 203 = CREATE DATABASE<br /><br /> 207 = CREATE VIEW<br /><br /> 222 = CREATE PROCEDURE<br /><br /> 224 = EXECUTE<br /><br /> 228 = BACKUP DATABASE<br /><br /> 233 = 既定値の作成<br /><br /> 235 = BACKUP LOG<br /><br /> 236 = ルールの作成|  
|**protecttype**|**tinyint**|次の値を持つことができます。<br /><br /> 204 GRANT_W_GRANT を =<br /><br /> 205 = GRANT<br /><br /> 206 = 拒否|  
|**columns**|**varbinary(8000)**|これらの SELECT または UPDATE 権限を適用する列のビットマップです。<br /><br /> ビット 0 = すべての列。<br /><br /> ビット 1 = 権限を適用する列<br /><br /> NULL = 情報はありません。|  
|**権限の許可者**|**smallint**|GRANT または DENY 権限を発行したユーザーのユーザー ID です。 オーバーフローまたはユーザーおよびロールの数が 32,767 を超える場合は NULL を返します。|  
  
## <a name="see-also"></a>関連項目  
 [システム ビューへのシステム テーブルのマッピング&#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [互換性ビュー &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
