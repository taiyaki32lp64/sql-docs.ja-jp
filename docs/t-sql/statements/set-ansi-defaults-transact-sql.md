---
title: SET ANSI_DEFAULTS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/04/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET ANSI_DEFAULTS
- ANSI_DEFAULTS
- SET_ANSI_DEFAULTS_TSQL
- ANSI_DEFAULTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ANSI_DEFAULTS option
- SET ANSI_DEFAULTS statement
ms.assetid: bd721d97-6e23-488b-8c8c-c0453d5b3b86
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 02353688efb79b4c2dbb7c4bc3d9ed0d4d5e0a37
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67913940"
---
# <a name="set-ansidefaults-transact-sql"></a>SET ANSI_DEFAULTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  一部の ISO 標準動作を集合的に指定する、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定のグループを制御します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

## <a name="syntax"></a>構文

```
-- Syntax for SQL Server

SET ANSI_DEFAULTS { ON | OFF }
```

```
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse

SET ANSI_DEFAULTS ON
```

## <a name="remarks"></a>Remarks  
ANSI_DEFAULTS は、クライアントで変更できない、サーバー側の設定です。 クライアントは自身の設定を管理します。 既定では、これらの設定はサーバー設定と対照的です。 サーバー設定は、ユーザーが変更するものではありません。 ユーザーがクライアントの動作を変更するには、SQL_COPT_SS_PRESERVE_CURSORS を使用します。 詳細については、「[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)」を参照してください。  
  
有効 (ON) に設定すると、次の ISO 設定が有効になります。  
  
|||  
|-|-|  
|[SET ANSI_NULLS]|[SET CURSOR_CLOSE_ON_COMMIT]|  
|[SET ANSI_NULL_DFLT_ON]|[SET IMPLICIT_TRANSACTIONS]|  
|[SET ANSI_PADDING]|[SET QUOTED_IDENTIFIER]|  
|[SET ANSI_WARNINGS]||  
  
また、ユーザーの作業セッション時や、トリガーまたはストアド プロシージャの実行時は、これらの ISO 標準 SET オプションは、クエリ処理環境を定義します。 ただし、これらの SET オプションには ISO 標準に準拠するために必要なオプションがすべて含まれているわけではありません。  
  
計算列およびインデックス付きビューにおいてインデックスを操作する場合は、4 つの既定オプション (ANSI_NULLS、ANSI_PADDING、ANSI_WARNINGS、および QUOTED_IDENTIFIER) を ON に設定する必要があります。 これは、計算列とインデックス付きビューにおいてインデックスを作成および変更するときに、指定された値に設定する必要がある 7 つの SET オプションの中の 4 つのオプションです。 その他の SET オプションは、ARITHABORT (ON)、CONCAT_NULL_YIELDS_NULL (ON)、および NUMERIC_ROUNDABORT (OFF) です。 インデックス付きビューおよび計算列上のインデックスに必要な SET オプション設定の詳細については、「[SET ステートメントの使用に関する留意事項](../../t-sql/statements/set-statements-transact-sql.md#considerations-when-you-use-the-set-statements)」を参照してください。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーおよび [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、接続時に自動的に ANSI_DEFAULTS が ON に設定されます。 次に、このドライバーとプロバイダーによって、CURSOR_CLOSE_ON_COMMIT と IMPLICIT_TRANSACTIONS が OFF に設定されます。 CURSOR_CLOSE_ON_COMMIT と IMPLICIT_TRANSACTIONS を OFF にする設定は、ODBC データ ソース、ODBC 接続属性、OLE DB 接続プロパティのいずれかで構成できます。OLE DB 接続プロパティは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続する前に、アプリケーションの内部で設定されます。 DB-Library アプリケーションからの接続に対しては、ANSI_DEFAULTS は既定で OFF に設定されています。  
  
SET ANSI_DEFAULTS を実行すると、QUOTED_IDENTIFIER は解析時に設定され、次のオプションは実行時に設定されます。  
  
|||  
|-|-|  
|[SET ANSI_NULLS]|[SET ANSI_WARNINGS]|  
|[SET ANSI_NULL_DFLT_ON]|[SET CURSOR_CLOSE_ON_COMMIT]|  
|[SET ANSI_PADDING]|[SET IMPLICIT_TRANSACTIONS]|  
  
## <a name="permissions"></a>アクセス許可  
ロール **public** のメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
次の例では、ANSI_DEFAULTS を ON に設定し、`DBCC USEROPTIONS` ステートメントを使用して、影響を受ける設定を表示します。  
  
```sql  
-- SET ANSI_DEFAULTS ON.  
SET ANSI_DEFAULTS ON;  
GO  

-- Display the current settings.  
DBCC USEROPTIONS;  
GO 

-- SET ANSI_DEFAULTS OFF.  
SET ANSI_DEFAULTS OFF;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [DBCC USEROPTIONS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-useroptions-transact-sql.md)   
 [SET ステートメント &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_NULL_DFLT_ON &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-null-dflt-on-transact-sql.md)   
 [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)   
 [SET CURSOR_CLOSE_ON_COMMIT &#40;Transact-SQL&#41;](../../t-sql/statements/set-cursor-close-on-commit-transact-sql.md)   
 [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)   
 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)  
  
  
