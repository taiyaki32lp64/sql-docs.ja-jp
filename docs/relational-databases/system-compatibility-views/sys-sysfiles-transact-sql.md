---
title: sys.sysfiles (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysfiles
- sys.sysfiles_TSQL
- sys.sysfiles
- sysfiles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysfiles system table
- sys.sysfiles compatibility view
ms.assetid: 3b47f38d-1cff-404d-89d3-9342c451c802
author: rothja
ms.author: jroth
ms.openlocfilehash: 2a3554e254be0623e36719fe76b2d811908a939d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053468"
---
# <a name="syssysfiles-transact-sql"></a>sys.sysfiles (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  データベース内の各ファイルの 1 つの行が含まれています。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**fileid**|**smallint**|各データベースで一意なファイル ID 番号です。|  
|**groupid**|**smallint**|ファイル グループ識別番号。|  
|**size**|**int**|8 KB のページで、ファイルのサイズ。|  
|**maxsize**|**int**|最大ファイル サイズ (8 KB ページ単位) です。<br /><br /> 0 = ファイル サイズが拡張しないことを表します。<br /><br /> -1 = ディスクがいっぱいになるまでファイル サイズが拡張します。<br /><br /> 268435456 = ログ ファイルが 2 TB の最大サイズに拡張されます。<br /><br /> 注:無制限のログ ファイルのサイズにアップグレードしたデータベースは、ログ ファイルの最大サイズに達すると-1 に報告されます。|  
|**growth**|**int**|データベースのサイズを増加します。 いずれかのページ数またはの値に応じて、ファイル サイズの割合を指定できます**状態**します。<br /><br /> 0 = ファイル サイズが拡張しないことを表します。|  
|**status**|**int**|ステータス ビットです、**成長**メガバイト (MB) またはキロバイト (KB) のいずれかの値。<br /><br /> 0x2 = ディスク ファイル。<br /><br /> 0x40 = ログ ファイル。<br /><br /> 0x100000 = 拡張します。 この値は、割合とページ数ではありません。|  
|**perf**|**int**|予約済み。|  
|**name**|**sysname**|ファイルの論理名です。|  
|**filename**|**nvarchar(260)**|物理デバイスの名前です。 これには、ファイルの完全なパスが含まれます。|  
  
## <a name="see-also"></a>関連項目  
 [システム ビューへのシステム テーブルのマッピング&#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [互換性ビュー &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
