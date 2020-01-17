---
title: SET ARITHABORT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ARITHABORT_TSQL
- ARITHABORT
- SET ARITHABORT
- SET_ARITHABORT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- terminating queries
- queries [SQL Server], terminating
- overflow errors [SQL Server]
- ARITHABORT option
- divide-by-zero errors
- SET ARITHABORT statement
- ending queries [SQL Server]
- stopping queries
ms.assetid: f938a666-fdd1-4233-b97f-719f27b1a0e6
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: da408c690622f5ba1ef45fa2466ed396d0022599
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68064615"
---
# <a name="set-arithabort-transact-sql"></a>SET ARITHABORT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

クエリ実行中にオーバーフローまたは 0 除算のエラーが発生した場合に、クエリを終了します。  
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```
-- Syntax for SQL Server and Azure SQL Database
  
SET ARITHABORT { ON | OFF }
```

```
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse

SET ARITHABORT ON
```
  
## <a name="remarks"></a>Remarks  
ログオン セッションでは、ARITHABORT を常に ON に設定します。 ARITHABORT を OFF に設定すると、クエリ最適化に悪影響を与え、パフォーマンスに関する問題が発生する可能性があります。  
  
> [!WARNING]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の ARITHABORT の既定値は ON です。 ARITHABORT が OFF に設定されているクライアント アプリケーションは異なるクエリ プランを受け取り、パフォーマンスに問題のあるクエリのトラブルシューティングが困難になる場合があります。 つまり、同じクエリでも Management Studio 内では高速実行できますが、アプリケーション内では実行速度が低下する可能性があります。 トラブルシューティングを行うとき、[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を使用するクエリは常に、クライアントの ARITHABORT 設定と一致します。  
  
SET ARITHABORT と SET ANSI WARNINGS が ON の場合、これらのエラー状態が発生するとクエリが終了します。  
  
SET ARITHABORT が ON で SET ANSI WARNINGS が OFF の場合、これらのエラー状態が発生するとバッチが終了します。 エラーがトランザクション内で発生した場合、トランザクションはロールバックされます。 SET ARITHABORT が OFF の場合に、これらのいずれかのエラーが発生すると、警告メッセージが表示され、算術演算の結果が NULL になります。  
  
SET ARITHABORT と SET ANSI WARNINGS が OFF の場合に、これらのいずれかのエラーが発生すると、警告メッセージが表示され、算術演算の結果が NULL になります。  
  
> [!NOTE]  
>  SET ARITHABORT と SET ARITHIGNORE の両方とも ON でない場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では NULL が返され、クエリの実行後に警告メッセージが表示されます。  
  
ANSI_WARNINGS を ON に設定すると、データベース互換性レベルが 90 以上に設定されている場合、暗黙的に ARITHABORT が ON に設定されます。 データベース互換性レベルが 80 以下に設定されている場合は、ARITHABORT オプションを明示的に ON に設定する必要があります。  
  
式の評価では、SET ARITHABORT が OFF の場合に、INSERT、UPDATE、または DELETE ステートメントで算術演算エラー、オーバーフロー エラー、0 除算エラー、またはドメイン エラーが検出されると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では NULL 値が挿入または更新されます。 出力先の列で NULL 値が許容されない場合は、挿入または更新処理は失敗し、エラーが表示されます。  
  
SET ARITHABORT と SET ARITHIGNORE のいずれかが OFF でも、SET ANSI_WARNINGS が ON の場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で 0 除算やオーバーフロー エラーが検出されるとエラー メッセージが返されます。  
  
SET ARITHABORT が OFF で、IF ステートメントのブール条件の評価中に中止エラーが発生すると、FALSE の分岐が実行されます。
  
計算列やインデックス付きビューのインデックスを作成または変更するときには、SET ARITHABORT を ON に設定する必要があります。 SET ARITHABORT が OFF の場合、計算列にインデックスが設定されているテーブルやインデックス付きビューに対して CREATE、UPDATE、INSERT、または DELETE ステートメントを実行すると失敗します。
  
SET ARITHABORT は、解析時ではなく実行時に設定されます。  
  
SET ARITHABORT の現在の設定を表示するには、次のクエリを実行します。
  
```  
DECLARE @ARITHABORT VARCHAR(3) = 'OFF';  
IF ( (64 & @@OPTIONS) = 64 ) SET @ARITHABORT = 'ON';  
SELECT @ARITHABORT AS ARITHABORT;  
  
```  
  
## <a name="permissions"></a>アクセス許可  
ロール **public** のメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
次の例では、`SET ARITHABORT` を ON に設定した場合の 0 除算のエラーおよびオーバーフロー エラーをそれぞれ示しています。  
  
```  
-- SET ARITHABORT  
-------------------------------------------------------------------------------  
-- Create tables t1 and t2 and insert data values.  
CREATE TABLE t1 (  
   a TINYINT,   
   b TINYINT  
);  
CREATE TABLE t2 (  
   a TINYINT  
);  
GO  
INSERT INTO t1   
VALUES (1, 0);  
INSERT INTO t1   
VALUES (255, 1);  
GO  
  
PRINT '*** SET ARITHABORT ON';  
GO  
-- SET ARITHABORT ON and testing.  
SET ARITHABORT ON;  
GO  
  
PRINT '*** Testing divide by zero during SELECT';  
GO  
SELECT a / b AS ab   
FROM t1;  
GO  
  
PRINT '*** Testing divide by zero during INSERT';  
GO  
INSERT INTO t2  
SELECT a / b AS ab    
FROM t1;  
GO  
  
PRINT '*** Testing tinyint overflow';  
GO  
INSERT INTO t2  
SELECT a + b AS ab   
FROM t1;  
GO  
  
PRINT '*** Resulting data - should be no data';  
GO  
SELECT *   
FROM t2;  
GO  
  
-- Truncate table t2.  
TRUNCATE TABLE t2;  
GO  
  
-- SET ARITHABORT OFF and testing.  
PRINT '*** SET ARITHABORT OFF';  
GO  
SET ARITHABORT OFF;  
GO  
  
-- This works properly.  
PRINT '*** Testing divide by zero during SELECT';  
GO  
SELECT a / b AS ab    
FROM t1;  
GO  
  
-- This works as if SET ARITHABORT was ON.  
PRINT '*** Testing divide by zero during INSERT';  
GO  
INSERT INTO t2  
SELECT a / b AS ab    
FROM t1;  
GO  
PRINT '*** Testing tinyint overflow';  
GO  
INSERT INTO t2  
SELECT a + b AS ab   
FROM t1;  
GO  
  
PRINT '*** Resulting data - should be 0 rows';  
GO  
SELECT *   
FROM t2;  
GO  
  
-- Drop tables t1 and t2.  
DROP TABLE t1;  
DROP TABLE t2;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [SET ステートメント &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ARITHIGNORE &#40;Transact-SQL&#41;](../../t-sql/statements/set-arithignore-transact-sql.md)   
 [SESSIONPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/sessionproperty-transact-sql.md)  
  
  
