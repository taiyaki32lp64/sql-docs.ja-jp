---
title: DBCC dllname (FREE) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- dbcc_dllname_(FREE)_TSQL
- dllname
- dbcc dllname (FREE)
- FREE
- dbcc_dllname(FREE)_TSQL
- FREE_TSQL
- dllname_TSQL
- dbcc dllname(FREE)
dev_langs:
- TSQL
helpviewer_keywords:
- DLL unloading [SQL Server]
- DBCC dllname (FREE)
- freeing DLLs
- unloading DLLs
ms.assetid: 1eb71c17-fe15-430b-8916-e4e312dcf9c0
author: pmasl
ms.author: umajay
ms.openlocfilehash: cc9716cbd1e27c6589b964c3c3d6208105f4863c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68101947"
---
# <a name="dbcc-dllname-free-transact-sql"></a>DBCC dllname (FREE) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
指定された拡張ストアド プロシージャ DLL をメモリからアンロードします。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
```sql
DBCC <dllname> ( FREE ) [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>引数  
 \<*dllname*>  
 メモリから解放する DLL の名前を指定します。  
  
 WITH NO_INFOMSGS  
 すべての情報メッセージを表示しないようにします。  
  
## <a name="remarks"></a>Remarks
拡張ストアド プロシージャを実行すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスによって DLL が読み込まれ、サーバーがシャットダウンされるまで読み込まれたままになります。 このステートメントを使うと、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をシャットダウンせずに DLL をメモリからアンロードできます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で現在読み込まれている DLL ファイルを表示するには、**sp_helpextendedproc** を実行します。
  
## <a name="result-sets"></a>結果セット  
有効な DLL を指定した場合、DBCC *dllname* (FREE) は次のメッセージを返します。
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>アクセス許可  
**sysadmin** 固定サーバー ロールまたは **db_owner** 固定データベース ロールのメンバーシップが必要です。
  
## <a name="examples"></a>使用例  
次の例では、`xp_sample` が xp_sample.dll として実装され、実行されているものとします。 DBCC \<*dllname*> (FREE) は、`xp_sample` 拡張プロシージャに関連付けられた xp_sample.dll ファイルをアップロードします。
  
```sql  
DBCC xp_sample (FREE);  
```  
  
## <a name="see-also"></a>参照  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[拡張ストアド プロシージャの実行における特性](../../relational-databases/extended-stored-procedures-programming/execution-characteristics-of-extended-stored-procedures.md)  
[sp_addextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)  
[sp_dropextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
[sp_helpextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)  
[拡張ストアド プロシージャ DLL のアンロード](../../relational-databases/extended-stored-procedures-programming/unloading-an-extended-stored-procedure-dll.md)
  
  
