---
title: sp_helpdevice (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpdevice
- sp_helpdevice_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpdevice
ms.assetid: 1a5eafa7-384e-4691-ba05-978eb73bbefb
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0db0242e5bdd9e04d3d7c424382933121c2e0ac2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67902989"
---
# <a name="sphelpdevice-transact-sql"></a>sp_helpdevice (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Microsoft&#xAE; SQL Server&#x2122; のバックアップ デバイスに関する情報をレポートします。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用することをお勧め、 [sys.backup_devices](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md)カタログ ビューを代わりに  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpdevice [ [ @devname = ] 'name' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @devname = ] 'name'` 情報をレポートするバックアップ デバイスの名前です。 値*名前*は常に**sysname**します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**device_name**|**sysname**|論理デバイス名。|  
|**physical_name**|**nvarchar(260)**|物理ファイル名。|  
|**description**|**nvarchar (255)**|デバイスの説明|  
|**status**|**int**|ステータスの説明に対応する番号、**説明**列。|  
|**cntrltype**|**smallint**|デバイスのコントローラーの種類<br /><br /> 2 = ディスク デバイス<br /><br /> 5 = テープ デバイス|  
|**size**|**int**|デバイス 2 KB ページ単位のサイズ。|  
  
## <a name="remarks"></a>コメント  
 場合*名前*が指定されている**sp_helpdevice**指定したダンプ デバイスに関する情報が表示されます。 場合*名前*が指定されていない**sp_helpdevice**内のすべてのダンプ デバイスに関する情報を表示、 **sys.backup_devices**カタログ ビューです。  
  
 ダンプ デバイスを使用して、システムに追加されて**sp_addumpdevice**します。  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例のインスタンス上のすべてのダンプ デバイスに関する情報を報告する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
```  
EXEC sp_helpdevice;  
```  
  
## <a name="see-also"></a>関連項目  
 [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [sp_dropdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdevice-transact-sql.md)   
 [データベース エンジン ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
