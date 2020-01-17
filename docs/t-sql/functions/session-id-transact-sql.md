---
title: SESSION_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/23/2018
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
author: VanMSFT
ms.author: vanto
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 3b63cbd1498021fdf9ed8418c3ff36ddec9143f0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68022230"
---
# <a name="sessionid-transact-sql"></a>SESSION_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  現在の [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] または [!INCLUDE[ssPDW_md](../../includes/sspdw-md.md)] セッションの ID を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
-- Azure SQL Data Warehouse and Parallel Data Warehouse  
SESSION_ID ( )  
```  
  
## <a name="return-value"></a>戻り値  
 **nvarchar(32)** 値を返します。  
  
## <a name="general-remarks"></a>全般的な解説  
 セッション ID は、接続が行われたときに、各ユーザー接続に割り当てられます。 これは、接続の間の永続化します。 接続の終了時に、セッション ID は解放されます。  
  
 セッション ID は、アルファベット文字 'SID' で開始します。 これらは大文字と小文字の区別があり、セッション ID が [!INCLUDE[DWsql](../../includes/dwsql-md.md)] コマンドで使われるときは大文字にする必要があります。  
  
 ビュー [sys.dm_pdw_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) をクエリして、この関数と同じ情報を取得できます。  
  
## <a name="examples"></a>使用例  
 次の例では、現在のセッション ID を返します。  
  
```  
SELECT SESSION_ID();  
```  
  
## <a name="see-also"></a>参照  
 [DB_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/db-name-transact-sql.md)   
 [VERSION &#40;SQL Data Warehouse&#41;](../../t-sql/functions/version-transact-sql-configuration-functions.md)
  
  
