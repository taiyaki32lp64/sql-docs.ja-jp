---
title: SET NOCOUNT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- NOCOUNT
- SET_NOCOUNT_TSQL
- NOCOUNT_TSQL
- SET NOCOUNT
dev_langs:
- TSQL
helpviewer_keywords:
- NOCOUNT option
- number of rows affected by statement
- row affected by statements [SQL Server]
- counting rows
- SET NOCOUNT statement
ms.assetid: eb3e6727-cb26-4bc2-84c7-171cbac02029
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f3593709dfbae0406e9952392ef82e184f205208
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68034955"
---
# <a name="set-nocount-transact-sql"></a>SET NOCOUNT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントまたはストアド プロシージャで処理された行数を示すメッセージが結果セットの一部として返されないようにします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
SET NOCOUNT { ON | OFF }   
```  
  
## <a name="remarks"></a>Remarks  
 SET NOCOUNT が ON の場合、カウントは返されません。 SET NOCOUNT が OFF の場合、行数が返されます。  
  
 SET NOCOUNT が ON の場合でも、@@ROWCOUNT 関数は更新されます。  
  
 SET NOCOUNT ON を指定すると、ストアド プロシージャ内の各ステートメントに対する DONE_IN_PROC メッセージは、クライアントに送信されなくなります。 このため、実際に返すデータが少量のステートメントで構成されるストアド プロシージャ、または [!INCLUDE[tsql](../../includes/tsql-md.md)] ループを含むプロシージャの場合、ネットワーク通信量が大きく減少するので、SET NOCOUNT を ON に設定するとパフォーマンスが大きく向上します。  
  
 SET NOCOUNT で指定される設定は、解析時ではなく実行時に有効になります。  
  
 この設定の現在の設定を表示するには、次のクエリを実行します。  
  
```  
DECLARE @NOCOUNT VARCHAR(3) = 'OFF';  
IF ( (512 & @@OPTIONS) = 512 ) SET @NOCOUNT = 'ON';  
SELECT @NOCOUNT AS NOCOUNT;  
  
```  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、影響を受けた行数に関するメッセージを表示しないようにします。  
  
```  
USE AdventureWorks2012;  
GO  
SET NOCOUNT OFF;  
GO  
-- Display the count message.  
SELECT TOP(5)LastName  
FROM Person.Person  
WHERE LastName LIKE 'A%';  
GO  
-- SET NOCOUNT to ON to no longer display the count message.  
SET NOCOUNT ON;  
GO  
SELECT TOP(5) LastName  
FROM Person.Person  
WHERE LastName LIKE 'A%';  
GO  
-- Reset SET NOCOUNT to OFF  
SET NOCOUNT OFF;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [@@ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md)   
 [SET ステートメント &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
