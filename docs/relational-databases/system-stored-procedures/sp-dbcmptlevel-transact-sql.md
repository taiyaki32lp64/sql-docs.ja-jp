---
title: sp_dbcmptlevel (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbcmptlevel
- sp_dbcmptlevel_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbcmptlevel
ms.assetid: 508c686d-2bd4-41ba-8602-48ebca266659
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0f6ffcb7a43fbfc2a840cbbbeb95de4bbb875cbe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108209"
---
# <a name="spdbcmptlevel-transact-sql"></a>sp_dbcmptlevel (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  データベースの特定の動作に、指定したバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] との互換性を設定します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 使用[ALTER DATABASE 互換性レベル](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)代わりにします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_dbcmptlevel [ [ @dbname = ] name ]   
    [ , [ @new_cmptlevel = ] version ]  
```  
  
## <a name="arguments"></a>引数  
`[ @dbname = ] name` 互換性レベルを変更するデータベースの名前です。 データベース名は、識別子の規則に従っている必要があります。 *名前* は **sysname** 、既定値は NULL です。  
  
`[ @new_cmptlevel = ] version` バージョンは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に互換性のある、データベースが使用されます。 *バージョン*は**tinyint**、既定値は NULL です。 値は、次のいずれかである必要があります。  
  
 **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
  
 **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
 **110** = [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
 **120** = [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
 **130** = [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 パラメーターが指定されていない場合、または場合、*名前*パラメーターが指定されていない**sp_dbcmptlevel**はエラーを返します。  
  
 場合*名前*なしで指定した*バージョン*、[!INCLUDE[ssDE](../../includes/ssde-md.md)]指定されたデータベースの現在の互換性レベルを表示するメッセージが返されます。  
  
## <a name="remarks"></a>コメント  
 互換性レベルの説明では、次を参照してください。 [ALTER DATABASE 互換性レベル&#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)します。  
  
## <a name="permissions"></a>アクセス許可  
 データベース所有者のメンバーのみ、 **sysadmin**固定サーバー ロール、および**db_owner**固定データベース ロール (現在のデータベースを変更している) 場合は、このプロシージャを実行できます。  
  
## <a name="see-also"></a>参照  
 [データベース エンジン ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [予約済みキーワード &#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
