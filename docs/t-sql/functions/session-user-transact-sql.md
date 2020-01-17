---
title: SESSION_USER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SESSION_USER_TSQL
- SESSION_USER
dev_langs:
- TSQL
helpviewer_keywords:
- usernames [SQL Server]
- current user names
- sessions [SQL Server], user names
- displaying user names
- viewing user names
- SESSION_USER function
ms.assetid: 3dbe8532-31b6-4862-8b2a-e58b00b964de
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c4bdf8b5057fcbf405d78872f7329c70c754ff76
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843339"
---
# <a name="session_user-transact-sql"></a>SESSION_USER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  SESSION_USER では現在のデータベースに含まれる現在のコンテキストのユーザー名が返されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
SESSION_USER  
```  
  
## <a name="return-types"></a>戻り値の型  
 **nvarchar(128)**  
  
## <a name="remarks"></a>Remarks  
 SESSION_USER は、DEFAULT 制約と共に CREATE TABLE または ALTER TABLE ステートメント内で使用するか、標準の関数として使用します。 SESSION_USER は、既定値が指定されていなければテーブルに挿入できます。 この関数は引数を取りません。 SESSION_USER はクエリで使用できます。  
  
 コンテキスト切り替え後に SESSION_USER が呼び出された場合、SESSION_USER では借用したコンテキストのユーザー名が返されます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-session_user-to-return-the-user-name-of-the-current-session"></a>A. SESSION_USER を使用して現在のセッションのユーザー名を返す  
 次の例では、変数を `nchar` 型として宣言し、`SESSION_USER` の現在値をこの変数に割り当てた後、テキストの説明と共にこの変数を出力します。  
  
```  
DECLARE @session_usr nchar(30);  
SET @session_usr = SESSION_USER;  
SELECT 'This session''s current user is: '+ @session_usr;  
GO  
```  
  
 セッション ユーザーが `Surya` の場合の結果セットは次のとおりです。  
  
 ```
--------------------------------------------------------------
This session's current user is: Surya

(1 row(s) affected)
```  
  
### <a name="b-using-session_user-with-default-constraints"></a>B. SESSION_USER を DEFAULT 制約と共に使用する  
 次の例では、荷物の受領記録者の名前に対し、`SESSION_USER` を `DEFAULT` 制約として使用するテーブルを作成します。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE deliveries3  
(  
 order_id int IDENTITY(5000, 1) NOT NULL,  
 cust_id  int NOT NULL,  
 order_date smalldatetime NOT NULL DEFAULT GETDATE(),  
 delivery_date smalldatetime NOT NULL DEFAULT   
    DATEADD(dd, 10, GETDATE()),  
 received_shipment nchar(30) NOT NULL DEFAULT SESSION_USER  
);  
GO  
```  
  
 テーブルに追加されたレコードに対して、現在のユーザーのユーザー名が設定されます。 この例では、`Wanida`、`Sylvester`、`Alejandro` が荷物の受領を確認します。 `EXECUTE AS` を使用してユーザー コンテキストを切り替えることでも、同様の機能を実現できます。  
  
```  
EXECUTE AS USER = 'Wanida'  
INSERT deliveries3 (cust_id)  
VALUES (7510);  
INSERT deliveries3 (cust_id)  
VALUES (7231);  
REVERT;  
EXECUTE AS USER = 'Sylvester'  
INSERT deliveries3 (cust_id)  
VALUES (7028);  
REVERT;  
EXECUTE AS USER = 'Alejandro'  
INSERT deliveries3 (cust_id)  
VALUES (7392);  
INSERT deliveries3 (cust_id)  
VALUES (7452);  
REVERT;  
GO  
```  
  
 次のクエリでは、`deliveries3` テーブルからすべての情報を選択します。  
  
```  
SELECT order_id AS 'Order #', cust_id AS 'Customer #',   
   delivery_date AS 'When Delivered', received_shipment   
   AS 'Received By'  
FROM deliveries3  
ORDER BY order_id;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Order #   Customer #  When Delivered       Received By
--------  ----------  -------------------  -----------
5000      7510        2005-03-16 12:02:14  Wanida
5001      7231        2005-03-16 12:02:14  Wanida
5002      7028        2005-03-16 12:02:14  Sylvester
5003      7392        2005-03-16 12:02:14  Alejandro
5004      7452        2005-03-16 12:02:14  Alejandro

(5 row(s) affected)
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-session_user-to-return-the-user-name-of-the-current-session"></a>C: SESSION_USER を使用して現在のセッションのユーザー名を返す  
 次の例では、現在のセッションのセッション ユーザーを返します。  
  
```  
SELECT SESSION_USER;  
```  
  
## <a name="see-also"></a>参照  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CURRENT_TIMESTAMP &#40;Transact-SQL&#41;](../../t-sql/functions/current-timestamp-transact-sql.md)   
 [CURRENT_USER &#40;Transact-SQL&#41;](../../t-sql/functions/current-user-transact-sql.md)   
 [SYSTEM_USER &#40;Transact-SQL&#41;](../../t-sql/functions/system-user-transact-sql.md)   
 [システム関数 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)   
 [USER &#40;Transact-SQL&#41;](../../t-sql/functions/user-transact-sql.md)   
 [USER_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/user-name-transact-sql.md)  
  
  

