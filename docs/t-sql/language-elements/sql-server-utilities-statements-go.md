---
title: GO (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GO
- GO_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- batches [SQL Server], ending
- ending batches [SQL Server]
- GO command
ms.assetid: b2ca6791-3a07-4209-ba8e-2248a92dd738
author: rothja
ms.author: jroth
ms.openlocfilehash: 48bca691f10822176c5169cf6bf9a052d7675478
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68072305"
---
# <a name="sql-server-utilities-statements---go"></a>SQL Server のユーティリティのステートメント - GO
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントではありませんが、**sqlcmd** ユーティリティ、**osql** ユーティリティ、および [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のコード エディターで認識されるコマンドがあります。 これらのコマンドを使用すると、バッチおよびスクリプトの読み取りと実行が容易になります。  
  
  GO は、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントのバッチの終了を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティに通知します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
GO [count]  
```  
  
## <a name="arguments"></a>引数  
 *count*  
 正の整数を指定します。 GO の前のバッチが、指定された回数実行されます。  
  
## <a name="remarks"></a>Remarks  
 GO は [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントではなく、**sqlcmd** および **osql** ユーティリティと [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] コード エディターで認識されるコマンドです。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のユーティリティでは、GO は、現在の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントのバッチを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに送信するためのシグナルとして解釈されます。 現在のステートメントのバッチは、前回の GO の後に入力されたすべてのステートメントで構成されます。最初の GO の場合、現在のバッチは、アドホック セッションまたはスクリプトの開始後に入力されたすべてのステートメントで構成されます。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを GO コマンドと同じ行に入力することはできません。 ただし、この行にコメントは入力できます。  
  
 ユーザーは、バッチの規則に従う必要があります。 たとえば、バッチの最初のステートメント以降でストアド プロシージャを実行する場合は、バッチに EXECUTE キーワードを含める必要があります。 ローカル (ユーザー定義) 変数のスコープはバッチ内に限られ、GO コマンドの後では参照できません。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyMsg VARCHAR(50)  
SELECT @MyMsg = 'Hello, World.'  
GO -- @MyMsg is not valid after this GO ends the batch.  
  
-- Yields an error because @MyMsg not declared in this batch.  
PRINT @MyMsg  
GO  
  
SELECT @@VERSION;  
-- Yields an error: Must be EXEC sp_who if not first statement in   
-- batch.  
sp_who  
GO  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アプリケーションでは、複数の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに送信し、バッチとして実行できます。 バッチ内のステートメントは、1 つの実行プランにコンパイルされます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティでアドホック ステートメントを実行する場合、または [!INCLUDE[tsql](../../includes/tsql-md.md)] ユーティリティを介して実行する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ステートメントのスクリプトを作成する場合、プログラマは GO を使用してバッチの終了を知らせる必要があります。  
  
 ODBC または OLE DB API に基づくアプリケーションで、GO コマンドを実行しようとすると、構文エラーになります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティは、サーバーに GO コマンドを送信することはありません。  
  
 GO の後、ステートメントのターミネータとしてセミコロンを使用しません。
 
```
-- Yields an error because ; is not permitted after GO  
SELECT @@VERSION;  
GO;  
```
  
## <a name="permissions"></a>アクセス許可  
 GO は、権限を必要としないユーティリティ コマンドです。 すべてのユーザーが実行できます。    
  
## <a name="examples"></a>使用例  
 次の例では、2 つのバッチを作成します。 最初のバッチは、データベース コンテキストを設定する `USE AdventureWorks2012` ステートメントのみで構成されます。 その他のステートメントではローカル変数が使用されます。 このため、すべてのローカル変数宣言を 1 つのバッチにまとめる必要があります。 これには、変数を参照する最後のステートメントが実行されてから `GO` コマンドを実行するようにします。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @NmbrPeople int  
SELECT @NmbrPeople = COUNT(*)  
FROM Person.Person;  
PRINT 'The number of people as of ' +  
      CAST(GETDATE() AS char(20)) + ' is ' +  
      CAST(@NmbrPeople AS char (10));  
GO  
```  
  
 次の例では、バッチ内のステートメントを 2 回実行します。  
  
```  
SELECT DB_NAME();  
SELECT USER_NAME();  
GO 2  
```  
  
  
