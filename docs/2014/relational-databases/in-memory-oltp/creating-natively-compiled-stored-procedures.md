---
title: ネイティブ コンパイル ストアド プロシージャの作成 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e6b34010-cf62-4f65-bbdf-117f291cde7b
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 9525ef65973baa38ae19ba4681e4a93f949c004a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63071822"
---
# <a name="creating-natively-compiled-stored-procedures"></a>ネイティブ コンパイル ストアド プロシージャの作成
  ネイティブ コンパイル ストアド プロシージャには、 [!INCLUDE[tsql](../../includes/tsql-md.md)] のプログラミングとクエリのセキュリティ構成が完全には実装されていません。 ネイティブ コンパイル ストアド プロシージャ内部で使用できない特定の [!INCLUDE[tsql](../../includes/tsql-md.md)] 構造が存在します。 詳細については、次を参照してください。[ネイティブ コンパイル ストアド プロシージャでサポートされる構造](../in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)します。  
  
 ただし、ネイティブ コンパイル ストアド プロシージャに対してのみサポートされる [!INCLUDE[tsql](../../includes/tsql-md.md)] 機能がいくつかあります。  
  
-   ATOMIC ブロック。 詳細については、「 [Atomic Blocks](atomic-blocks-in-native-procedures.md)」を参照してください。  
  
-   ネイティブ コンパイル ストアド プロシージャのパラメーターおよび変数の `NOT NULL` 制約。 `NULL` として宣言されているパラメーターまたは変数に `NOT NULL` 値を割り当てることはできません。 詳細については、「[DECLARE @local_variable &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/declare-local-variable-transact-sql)」を参照してください。  
  
-   ネイティブ コンパイル ストアド プロシージャのスキーマ バインド。  
  
 ネイティブ コンパイル ストアド プロシージャは、[CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql) を使用して作成します。 次の例は、メモリ最適化テーブルと、このテーブルに行を挿入するために使用されるネイティブ コンパイル ストアド プロシージャを示します。  
  
```sql  
create table dbo.Ord  
(OrdNo integer not null primary key nonclustered,   
 OrdDate datetime not null,   
 CustCode nvarchar(5) not null)   
 with (memory_optimized=on)  
go  
  
create procedure dbo.OrderInsert(@OrdNo integer, @CustCode nvarchar(5))  
with native_compilation, schemabinding, execute as owner  
as   
begin atomic with  
(transaction isolation level = snapshot,  
language = N'English')  
  
  declare @OrdDate datetime = getdate();  
  insert into dbo.Ord (OrdNo, CustCode, OrdDate) values (@OrdNo, @CustCode, @OrdDate);  
end  
go  
```  
  
 コード サンプルの `NATIVE_COMPILATION` は、この [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャがネイティブ コンパイル ストアド プロシージャであることを示しています。 以下のオプションは必須です。  
  
|オプション|説明|  
|------------|-----------------|  
|`SCHEMABINDING`|ネイティブ コンパイル ストアド プロシージャは、参照するオブジェクトのスキーマにバインドする必要があります。 つまり、プロシージャによってテーブル参照を削除することはできません。 プロシージャで参照されるテーブルは、そのスキーマ名、およびワイルドカードを含める必要があります (\*) クエリでは許可されません。 このバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、ネイティブ コンパイル ストアド プロシージャに対してのみ `SCHEMABINDING` がサポートされます。|  
|`EXECUTE AS`|ネイティブ コンパイル ストアド プロシージャでは、既定の実行コンテキストである `EXECUTE AS CALLER` はサポートされません。 したがって、実行コンテキストの指定は必須です。 オプション`EXECUTE AS OWNER`、 `EXECUTE AS`*ユーザー*、および`EXECUTE AS SELF`はサポートされています。|  
|`BEGIN ATOMIC`|ネイティブ コンパイル ストアド プロシージャの本体は、厳密に 1 つの ATOMIC ブロックで構成されている必要があります。 ATOMIC ブロックでは、ストアド プロシージャのアトミック実行が保証されます。 プロシージャをアクティブなトランザクションのコンテキストの外部で呼び出した場合、新しいトランザクションが開始され、ATOMIC ブロックの末尾でコミットされます。 ネイティブ コンパイル ストアド プロシージャの ATOMIC ブロックには、次の 2 つの必須オプションがあります。<br /><br /> `TRANSACTION ISOLATION LEVEL` 。 参照してください[トランザクション分離レベル](../../database-engine/transaction-isolation-levels.md)の分離レベルをサポートします。<br /><br /> `LANGUAGE` 。 ストアド プロシージャの言語は、使用可能な言語または言語の別名の 1 つに設定されている必要があります。|  
  
 `EXECUTE AS` と Windows ログインについては、`EXECUTE AS` を通じて行われた権限借用によって、エラーが発生する場合があります。 ユーザー アカウントに対して Windows 認証が使用される場合は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスに使用されるサービス アカウントと Windows ログインのドメインとの間に完全信頼が必要です。 完全な信頼がない場合は、ストアド プロシージャのネイティブ コンパイルを作成するときに、次のエラー メッセージが返されます。メッセージ 15404、Windows NT グループ/ユーザー 'username' が、エラー コード 0x5 に関する情報を取得できませんでした。  
  
 このエラーを解決するには、次のいずれかを使用します。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスの Windows ユーザーと同じドメインからのアカウントを使用します。  
  
-   場合[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]は Network Service や Local System、コンピューターなどのコンピューター アカウントを信頼する必要がありますを使用して、Windows ユーザーが含まれるドメインによって。  
  
-   使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]認証します。  
  
 ネイティブ コンパイル ストアド プロシージャを作成するときに、エラー 15517 が発生することもあります。 詳細については、次を参照してください。 [MSSQLSERVER_15517](../errors-events/mssqlserver-15517-database-engine-error.md)します。  
  
## <a name="updating-a-natively-compiled-stored-procedure"></a>ネイティブ コンパイル ストアド プロシージャの更新  
 ネイティブ コンパイル ストアド プロシージャに対する変更操作はサポートされていません。 ネイティブ コンパイル ストアド プロシージャを変更する方法の 1 つは、ストアド プロシージャを削除してから再作成することです。  
  
1.  ストアド プロシージャに対する権限用のスクリプトを生成します。  
  
2.  ストアド プロシージャ用のスクリプトを生成し、バックアップとして保存することもできます。  
  
3.  ストアド プロシージャを削除します。  
  
4.  変更したストアド プロシージャを作成します。  
  
5.  ストアド プロシージャにスクリプト化した権限を再適用します。  
  
 この手順の欠点は、手順 3. を開始して手順 5. を完了するまでアプリケーションがオフラインになることです。 これには数秒かかる場合があり、アプリケーションを使用するクライアントに対してエラー メッセージが表示されることがあります。  
  
 ネイティブ コンパイル ストアド プロシージャを効率的に変更する別の方法は、まずストアド プロシージャの新しいバージョンを作成することです。 ネイティブ コンパイル ストアド プロシージャには関連付けられたバージョン番号があります。 古いバージョンを SP_Vold、新しいバージョンを SP_Vnew とします。  
  
1.  SP_Vold に対する権限用のスクリプトを生成します。  
  
2.  SP_Vnew を作成します。  
  
3.  SP_Vold の権限を SP_Vnew に適用します。  
  
4.  SP_Vold への参照を SP_Vnew を指すように更新します。 これは別の方法でも行うことができます。たとえば次のとおりです。  
  
     ラッパー (ディスク ベース) ストアド プロシージャを使用し、SP_Vnew を指すようにそのプロシージャを変更します。 この方法の欠点は、間接指定によってパフォーマンスに影響することです。  
  
    ```sql  
    ALTER PROCEDURE dbo.SP p1,...,pn  
    AS  
      EXEC dbo.SP_Vnew p1,...,pn  
    GO  
    ```  
  
5.  SP_Vold を削除することもできます。  
  
 この方法の利点は、アプリケーションがオフラインにならないことです。 しかし、参照の保持と、ストアド プロシージャの最新バージョンを常にポイントさせるために、より多くの作業が必要となります。  
  
## <a name="see-also"></a>参照  
 [ネイティブ コンパイル ストアド プロシージャ](natively-compiled-stored-procedures.md)  
  
  
