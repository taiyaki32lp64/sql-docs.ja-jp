---
title: sp_msx_defect (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_msx_defect
- sp_msx_defect_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_msx_defect
ms.assetid: 0dfd963a-3bc5-4b58-94f7-aec976da2883
author: stevestein
ms.author: sstein
ms.openlocfilehash: c8f2e34d15f7cca4443680b2d8b8a9fa2c7c6199
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67952318"
---
# <a name="spmsxdefect-transact-sql"></a>sp_msx_defect (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  マルチ サーバー操作から現在のサーバーを削除します。  
  
> [!CAUTION]  
>  **sp_msx_defect**はレジストリを編集します。 レジストリは手動で編集しないでください。不適切または不正確な変更を加えると、システム構成に重大な問題が生じる場合があります。 熟練したユーザーのみがレジストリ エディターを使用してレジストリを編集することをお勧めします。 詳細については、Microsoft Windows のマニュアルを参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_msx_defect [@forced_defection =] forced_defection  
```  
  
## <a name="arguments"></a>引数  
`[ @forced_defection = ] forced_defection` 強制的に、マスター SQLServerAgent が、致命的に破損した完全に失われた場合に発生する参加解除するかどうかを指定します**msdb**データベース、または いいえ**msdb**データベースのバックアップ。 *forced_defection*は**ビット**、既定値は**0**、強制的な参加解除が発生しないことを示します。 値**1**強制的に参加解除します。  
  
 強制的に実行することによって、参加解除した後は**sp_msx_defect**のメンバー、 **sysadmin**マスター sqlserveragent の固定サーバー ロールは、参加解除を完了するには、次のコマンドを実行する必要があります。  
  
```  
EXECUTE msdb.dbo.sp_delete_targetserver @server_name = 'tsx-server', @post_defection =  0;  
```  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>コメント  
 ときに**sp_msx_defect**正常に完了すると、メッセージが返されます。  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャを実行するには、 **sysadmin** 固定サーバー ロールのメンバーであることが必要です。  
  
## <a name="see-also"></a>関連項目  
 [sp_msx_enlist &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
