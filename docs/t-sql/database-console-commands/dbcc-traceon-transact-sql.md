---
title: DBCC TRACEON (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC_TRACEON_TSQL
- TRACEON
- DBCC TRACEON
- TRACEON_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DBCC TRACEON statement
- trace flags [SQL Server], enabling
ms.assetid: 93085324-ebaa-4e38-aac8-5e57b4b0d36d
author: pmasl
ms.author: umajay
ms.openlocfilehash: 3831a9244b3e946dcba01b7d8c31825a75f7b39f
ms.sourcegitcommit: 57e20b7d02853ec9af46b648106578aed133fb45
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2019
ms.locfileid: "69553259"
---
# <a name="dbcc-traceon-transact-sql"></a>DBCC TRACEON (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

指定されたトレース フラグを有効にします。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
DBCC TRACEON ( trace# [ ,...n ][ , -1 ] ) [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>引数  
*trace#*  
有効にするトレース フラグの番号を指定します。  
  
*n*  
複数のトレース フラグを指定できることを示すプレースホルダーです。  
  
-1  
指定されたトレース フラグをグローバルに有効にします。 Azure SQL Managed Instance では、この引数は必須です。 
  
WITH NO_INFOMSGS  
すべての情報メッセージを表示しないようにします。  
  
## <a name="remarks"></a>Remarks  
稼働サーバーでは、予期しない動作を避けるため、次のいずれかの方法を使用してトレース フラグをサーバー規模でのみ有効にすることをお勧めします。
-   Sqlservr.exe のコマンド ライン スタートアップ オプション **-T** を使用します。 すべてのステートメントがトレース フラグを有効にした状態で実行されるので、この方法をお勧めします。 これらはスタートアップ スクリプトのコマンドに含まれています。 詳細については、「 [sqlservr Application](../../tools/sqlservr-application.md)」を参照してください。  
-   DBCC TRACEON **(** _trace#_ [ **,** ... *.n*] **,-1)** は、システムでユーザーまたはアプリケーションが同時にステートメントを実行していない場合にのみ使用します。  

トレース フラグは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の動作を制御して特定の特性をカスタマイズするために使用されます。 トレース フラグは、有効になると、DBCC TRACEOFF ステートメントを実行して無効にするまで、サーバー内では有効のままです。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、セッションとグローバルという 2 種類のトレース フラグがあります。 セッション トレース フラグは、1 つの接続についてアクティブで、その接続に対してのみ表示可能です。 グローバル トレース フラグは、サーバー レベルで設定され、サーバー上のすべての接続に対して表示可能です。 トレース フラグの状態を確認するには、DBCC TRACESTATUS を使用します。 トレース フラグを無効にするには、DBCC TRACEOFF を使用します。
  
クエリ プランに影響を与えるトレース フラグをオンにした後、`DBCC FREEPROCCACHE;` を実行すると、新しいプランに影響を与える動作を使用して、キャッシュされているプランが再コンパイルされます。

Azure SQL Database Managed Instance では、次のグローバル トレース フラグがサポートされています。460、2301、2389、2390、2453、2467、7471、8207、9389、10316、および 11024

## <a name="result-sets"></a>結果セット  
 DBCC TRACEON は次の結果セット (メッセージ) を返します。  
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>アクセス許可  
**sysadmin** 固定サーバー ロールのメンバーシップが必要です。
  
## <a name="examples"></a>使用例  
次の例では、トレース フラグ `3205` を有効にすることにより、テープ ドライバーのハードウェア圧縮を無効にします。 このフラグは、現在の接続に対してのみオンとなります。
  
```sql  
DBCC TRACEON (3205);  
GO  
```  
  
次の例では、トレース フラグ `3205` をグローバルに有効にします。
  
```sql  
DBCC TRACEON (3205, -1);  
GO  
```  
  
次の例では、トレース フラグ `3205` および `260` をグローバルに有効にします。
  
```sql  
DBCC TRACEON (3205, 260, -1);  
GO  
```  
  
## <a name="see-also"></a>参照  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC TRACEOFF &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceoff-transact-sql.md)  
[DBCC TRACESTATUS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-tracestatus-transact-sql.md)  
[トレース フラグ &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
[特定のクエリ レベルに対応するさまざまなトレース フラグを使用して制御できる、プランが影響を及ぼす SQL Server クエリ オプティマイザーの動作の有効化](https://support.microsoft.com/kb/2801413)
  
  
