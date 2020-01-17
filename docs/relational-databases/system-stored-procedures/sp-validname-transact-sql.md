---
title: sp_validname (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_validname
- sp_validname_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_validname
ms.assetid: d51c53c2-1332-407f-b725-4983f2e710eb
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c559c8a6af6add669e1cc4630b7bcfc9fc0aacc2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936734"
---
# <a name="spvalidname-transact-sql"></a>sp_validname (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  有効な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別子名かどうかをチェックします。 非バイナリおよび 0 以外の場合、すべてのデータを使用して格納できる Unicode データを含む、 **nchar**、 **nvarchar**、または**ntext 型**の有効な文字として、データ型を許可します。識別子の名前です。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_validname [@name =] 'name'   
     [, [@raise_error =] raise_error]  
```  
  
## <a name="arguments"></a>引数  
`[ @name = ] 'name'` 名前を指定します、[識別子](../../relational-databases/databases/database-identifiers.md)の有効性をチェックします。 *名前*は**sysname**、既定値はありません。 *名前*NULL にすることはできません、空の文字列にすることはできませんし、バイナリおよび 0 の文字を含めることはできません。  
  
`[ @raise_error = ] raise_error` エラーが発生するかどうかを指定します。 *raise_error*は**ビット**、既定値は 1 です。 つまり、エラーが表示されます。 0 の場合、エラー メッセージは表示されません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="see-also"></a>参照  
 [データベース エンジン ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [NCHAR &#40;Transact-SQL&#41;](../../t-sql/functions/nchar-transact-sql.md)   
 [nchar および nvarchar &#40;Transact SQL&#41;](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)   
 [ntext 型、テキスト、およびイメージ&#40;Transact SQL&#41;](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
