---
title: SET TEXTSIZE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/12/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TEXTSIZE_TSQL
- TEXTSIZE
- SET_TEXTSIZE_TSQL
- SET TEXTSIZE
dev_langs:
- TSQL
helpviewer_keywords:
- SET TEXTSIZE statement
- SELECT statement [SQL Server], text size returned
- size [SQL Server], text and image data
- TEXTSIZE option
- text size returned [SQL Server]
ms.assetid: 787154a6-39a6-4dd6-a6d0-67b4364f95d5
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b7e0a949e132f01ce82e46a6e8b4c1d761c1a52a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68100049"
---
# <a name="set-textsize-transact-sql"></a>SET TEXTSIZE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  SELECT ステートメントによって返される **varchar(max)** 、**nvarchar(max)** 、**varbinary(max)** 、**text**、**ntext**、**image** データのサイズを指定します。  
  
> [!IMPORTANT]
>  **ntext**、**text**、および **image** データ型は、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の将来のバージョンで削除される予定です。 新しい開発作業では、これらのデータ型の使用は避け、現在これらのデータ型を使用しているアプリケーションは修正するようにしてください。 代わりに、 **nvarchar(max)** 、 **varchar(max)** 、 **varbinary(max)** を使用してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
SET TEXTSIZE { number }   
```  
  
## <a name="arguments"></a>引数  
 *number*  
 **varchar(max)** 、**nvarchar(max)** 、**varbinary(max)** 、**text**、**ntext**、または **image** データのバイト単位の長さです。 *number* は、最大値が 2147483647 (2 GB) の整数です。  値 -1 は無制限のサイズを示します。 値 0 は、サイズを既定値の 4 KB にリセットします。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client (10.0 以降) および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の ODBC ドライバーは、接続時に自動的に `-1` (無制限) を指定します。  
  
 **Drivers older than [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーおよび [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB Provider (バージョン 9) for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、接続時に自動的に TEXTSIZE が 2147483647 に設定されます。  
  
## <a name="remarks"></a>Remarks  
 SET TEXTSIZE の設定は、@@TEXTSIZE 関数に影響します。  
  
 TEXTSIZE は、解析時ではなく実行時に設定されます。  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="see-also"></a>参照  
 [@@TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/functions/textsize-transact-sql.md)   
 [データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [SET ステートメント &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
