---
title: sp_xml_removedocument (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_xml_removedocument_TSQL
- sp_xml_removedocument
dev_langs:
- TSQL
helpviewer_keywords:
- sp_xml_removedocument
ms.assetid: f9dca50a-8baf-4170-90bc-e72783ce5b73
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6219f18bee08d5c20431cb87a2cb30795c515d7a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67950473"
---
# <a name="spxmlremovedocument-transact-sql"></a>sp_xml_removedocument (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  ドキュメント ハンドルで指定された XML ドキュメントの内部表現を削除し、ドキュメント ハンドルを無効にします。  
  
> [!NOTE]  
>  解析済みドキュメントがの内部キャッシュに格納されている[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 MSXML パーサー (Msxmlsql.dll) では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に割り当てられている総メモリの 8 分の 1 が使用されます。 メモリ不足を回避するには、実行**sp_xml_removedocument**メモリを解放します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_xml_removedocument hdoc  
```  
  
## <a name="arguments"></a>引数  
 *hdoc*  
 新しく作成されたドキュメントへのハンドルを指定します。 無効なハンドルには、エラーが返されます。 *hdoc*は整数です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または > 0 (失敗)  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、XML ドキュメントの内部表現を削除します。 ドキュメントを識別するハンドルは、入力として提供されます。  
  
```  
EXEC sp_xml_removedocument @hdoc;  
```  
  
## <a name="see-also"></a>関連項目      
 <br>[システム ストアド プロシージャ (TRANSACT-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)
 <br>[XML ストアド プロシージャ (TRANSACT-SQL)](../../relational-databases/system-stored-procedures/xml-stored-procedures-transact-sql.md)
 <br>[sys.dm_exec_xml_handles (TRANSACT-SQL)](../system-dynamic-management-views/sys-dm-exec-xml-handles-transact-sql.md)
 <br>[sp_xml_preparedocument(Transact-SQL)](../../relational-databases/system-stored-procedures/sp-xml-preparedocument-transact-sql.md)
 <br>[OPENXML (TRANSACT-SQL)](../../t-sql/functions/openxml-transact-sql.md)
  
  
