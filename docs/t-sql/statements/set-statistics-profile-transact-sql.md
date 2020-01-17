---
title: SET STATISTICS PROFILE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PROFILE
- SET_STATISTICS_PROFILE_TSQL
- PROFILE_TSQL
- SET STATISTICS PROFILE
dev_langs:
- TSQL
helpviewer_keywords:
- profiles [SQL Server], displaying
- statements [SQL Server], profile information
- SET STATISTICS PROFILE statement
- STATISTICS PROFILE option
- statistical information [SQL Server], profiles
ms.assetid: c635e262-35fa-421a-aa6f-a1c30f351647
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b3d48de1a5feef4a00b087fded311a2b57169047
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68131928"
---
# <a name="set-statistics-profile-transact-sql"></a>SET STATISTICS PROFILE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  ステートメントのプロファイル情報を表示します。 STATISTICS PROFILE は、アドホック クエリ、ビュー、ストアド プロシージャに対して機能します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
SET STATISTICS PROFILE { ON | OFF }  
```  
  
## <a name="remarks"></a>Remarks  
 STATISTICS PROFILE が ON の場合、クエリを実行すると、それぞれ通常の結果セットに加えて、クエリ実行のプロファイルを示す追加の結果セットが返されます。  
  
 追加の結果セットには、クエリに関する SHOWPLAN_ALL 列と次の追加列が含まれます。  
  
|列名|[説明]|  
|-----------------|-----------------|  
|**行数**|それぞれの演算子によって作成された実際の行数|  
|**Executes**|演算子が実行された回数|  
  
## <a name="permissions"></a>アクセス許可  
 SET STATISTICS PROFILE を使用して出力を表示するには、次の権限が必要です。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行するための適切な権限。  
  
-   SHOWPLAN 権限。これは、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントで参照されるオブジェクトを含むすべてのデータベースに対して必要です。  
  
 STATISTICS PROFILE の結果セットを生成しない [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの場合は、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行するための適切な権限のみで十分です。 STATISTICS PROFILE の結果セットを生成する [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの場合は、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行する権限と、SHOWPLAN の権限の両方を持っていることを確認してください。これらの 2 つの権限がないと、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの実行は中断され、プラン表示に関する情報は生成されません。  
  
## <a name="see-also"></a>参照  
 [SET ステートメント &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET SHOWPLAN_ALL &#40;Transact-SQL&#41;](../../t-sql/statements/set-showplan-all-transact-sql.md)   
 [SET STATISTICS TIME &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-time-transact-sql.md)   
 [SET STATISTICS IO &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-io-transact-sql.md)  
  
  
