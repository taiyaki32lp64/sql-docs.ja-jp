---
title: sp_markpendingschemachange (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_markpendingschemachange
- sp_markpendingschemachange_TSQL
helpviewer_keywords:
- sp_markpendingschemachange
ms.assetid: 01100309-7bef-4154-85bf-f18489577e37
author: stevestein
ms.author: sstein
ms.openlocfilehash: 56ed176d8b4b29e1ed4caafabd0893b7a33b1293
ms.sourcegitcommit: eae9efe2a2d3758685e85039ffb8fa698aa47f9b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73962392"
---
# <a name="sp_markpendingschemachange-transact-sql"></a>sp_markpendingschemachange (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  選択した保留中のスキーマ変更がレプリケートされないように、管理者がそのスキーマ変更をスキップできるようにします。これは、マージ パブリケーションをサポートするための操作です。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。  
  
> [!CAUTION]  
>  このストアドプロシージャによって、スキーマの変更がレプリケートされない可能性があります。 再初期化などの他の方法が既に試行されているか、パフォーマンスの面でコストが高すぎる場合にのみ、問題を解決するために使用する必要があります。  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_markpendingschemachange [@publication = ] 'publication'  
    [ , [ @schemaversion = ] schemaversion ]  
    [ , [ @status = ] 'status' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` パブリケーションの名前を指定します。 *publication* は **sysname** 、既定値はありません。  
  
`[ @schemaversion = ] schemaversion` は、保留中のスキーマ変更を識別します。 *schemaversion*は**int**,、既定値は**0**です。 [Transact-sql&#41; sp_enumeratependingschemachanges &#40;](../../relational-databases/system-stored-procedures/sp-enumeratependingschemachanges-transact-sql.md)使用して、パブリケーションの保留中のスキーマ変更を一覧表示します。  
  
`[ @status = ] 'status'` は、保留中のスキーマ変更をスキップするかどうかです。 *状態*は**nvarchar (10)** で、既定値は**アクティブ**です。 *Status*の値が**スキップ**された場合、選択したスキーマの変更はレプリケートされません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>Remarks  
 **sp_markpendingschemachange**は、マージレプリケーションで使用します。  
  
 **sp_markpendingschemachange**は、マージレプリケーションのサポートを目的としたストアドプロシージャであり、再初期化などの他の是正措置が状況を修正できなかった場合、またはパフォーマンスの面でコストが高すぎる場合にのみ使用してください。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_markpendingschemachange**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [sysmergeschemachange &#40;transact-sql&#41;](../../relational-databases/system-tables/sysmergeschemachange-transact-sql.md)  
  
  
