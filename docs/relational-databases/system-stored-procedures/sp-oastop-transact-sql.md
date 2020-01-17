---
title: sp_OAStop (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OAStop
- sp_OAStop_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OAStop
ms.assetid: aa9eab66-c4f7-4ec7-9f0d-5d24d16da654
author: stevestein
ms.author: sstein
ms.openlocfilehash: ead1a768a89e9b43c02d7e80619dbf52165d2a38
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097612"
---
# <a name="spoastop-transact-sql"></a>sp_OAStop (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  サーバー全体の OLE オートメーション ストアド プロシージャの実行環境を停止します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_OAStop      
```  
  
## <a name="return-code-values"></a>リターン コードの値  
 成功した場合は 0、失敗した場合は OLE オートメーション オブジェクトによって返される HRESULT の 0 以外の整数値を返します。  
  
 HRESULT のリターン コードの詳細については、次を参照してください。 [OLE オートメーションのリターン コードとエラー情報](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)します。  
  
## <a name="remarks"></a>コメント  
 OLE オートメーション ストアド プロシージャを使用しているすべてのクライアントで、1 つの実行環境が共有されます。 1 つのクライアントを呼び出す場合**sp_OAStop**共有実行環境がすべてのクライアントを停止します。 すべての呼び出しに、実行環境を停止すると後、 **sp_OACreate**実行環境を再起動します。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーシップが必要です、 **sysadmin**固定サーバー ロールまたはアクセス許可をこのストアド プロシージャを直接実行します。 `Ole Automation Procedures` 構成でなければなりません**有効になっている**OLE オートメーションに関連するすべてのシステム プロシージャを使用します。  
  
## <a name="examples"></a>使用例  
 次の例では、共有している OLE オートメーション実行環境を停止します。  
  
```  
EXEC sp_OAStop;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [OLE オートメーション ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [OLE オートメーションのサンプル スクリプト](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
