---
title: sp_prepexecrpc (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepexecrpc
- sp_cursor_prepexecrpc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_prepexecrpc
ms.assetid: 35d686f2-ef31-4eaa-baa9-9cef5d6c87c2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6fea210183ae67179dcc6f686e25f939cd00713b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056333"
---
# <a name="spprepexecrpc-transact-sql"></a>sp_prepexecrpc (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  準備して、RPC 識別子を使用して指定されているパラメーター化されたストアド プロシージャの呼び出しを実行します。 sp_prepexecrpc は、ID によって呼び出される、表形式データ ストリーム (TDS) パケットで 14 の = です。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_prepexecrpc handle OUTPUT, RPCCall  
    [ , bound_param ] [ ,...n]]  
```  
  
## <a name="arguments"></a>引数  
 *handle*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって生成される準備済みハンドル識別子です。 *処理*必須のパラメーターには、 **int**値を返します。  
  
 *RPCCall*  
 ODBC 標準構文を使用してストアド プロシージャ呼び出しを定義します。 *RPCCall*が必要なパラメーターです、 **ntext**文字列入力値。  
  
 *bound_param*  
 追加パラメーターをオプションで使用することを示します。 *bound_param*を使用する追加パラメーターを指定する任意のデータ型の入力値を呼び出します。  
  
## <a name="see-also"></a>関連項目  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
