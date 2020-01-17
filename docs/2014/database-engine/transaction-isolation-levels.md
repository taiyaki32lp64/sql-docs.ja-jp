---
title: トランザクション分離レベルメモリ最適化テーブル |Microsoft Docs
ms.custom: seo-dt-2019
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 8a6a82bf-273c-40ab-a101-46bd3615db8a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: eea34b8ad278447d9e9085d99acb8500d14d5e7a
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73637782"
---
# <a name="transaction-isolation-levels-in-memory-optimized-tables"></a>メモリ最適化テーブルのトランザクション分離レベル

  メモリ最適化テーブルにアクセスするトランザクションでは、次の分離レベルがサポートされます。  
  
-   SNAPSHOT  
  
-   REPEATABLE READ  
  
-   SERIALIZABLE  
  
-   READ COMMITTED  
  
 トランザクション分離レベルは、ネイティブ コンパイル ストアド プロシージャの ATOMIC ブロックの一部として指定できます。 詳細については、「[CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql)」を参照してください。 解釈された [!INCLUDE[tsql](../includes/tsql-md.md)] からメモリ最適化テーブルにアクセスするときに、テーブル レベルのヒントを使用して分離レベルを指定することもできます。  
  
 ネイティブ コンパイル ストアド プロシージャを定義する際には、トランザクション分離レベルを指定する必要があります。 解釈された [!INCLUDE[tsql](../includes/tsql-md.md)] のユーザー トランザクションからメモリ最適化テーブルにアクセスするときは、テーブル ヒントで分離レベルを指定する必要があります。 詳細については、「[メモリ最適化テーブルを使用したトランザクション分離レベルのガイドライン](../relational-databases/in-memory-oltp/memory-optimized-tables.md)」を参照してください。  
  
 自動コミット トランザクションを使用するメモリ最適化テーブルでは、READ COMMITTED 分離レベルがサポートされます。 READ COMMITTED は、ユーザー トランザクションまたは ATOMIC ブロックでは無効です。 READ COMMITTED は、明示的または暗黙的なユーザー トランザクションではサポートされません。 自動コミット トランザクションを使用するメモリ最適化テーブルについては、クエリがどのディスク ベース テーブルにもアクセスできない場合にのみ、分離レベル READ_COMMITTED_SNAPSHOT がサポートされます。 また、解釈された [!INCLUDE[tsql](../includes/tsql-md.md)] を使用して SNAPSHOT 分離で開始されるトランザクションでは、メモリ最適化テーブルにアクセスできません。 REPEATABLE READ 分離または SERIALIZABLE 分離が指定された、解釈された [!INCLUDE[tsql](../includes/tsql-md.md)] を使用するトランザクションでは、SNAPSHOT 分離を使用してメモリ最適化テーブルにアクセスする必要があります。 このシナリオの詳細については、「[複数コンテナーにまたがるトランザクション](cross-container-transactions.md)」を参照してください。  
  
 READ COMMITTED は、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の既定の分離レベルです。 セッションの分離レベルが READ COMMITED (またはそれ以下) の場合は、次のいずれかの操作を実行できます。  
  
-   メモリ最適化テーブルにアクセスするためにより高い分離レベルのヒントを明示的に指定する (WITH (SNAPSHOT) など)。  
  
-   `MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT` 設定オプションを指定する。これにより、(各メモリ最適化テーブルに WITH(SNAPSHOT) ヒントを含めた場合のように) メモリ最適化テーブルの分離レベルが SNAPSHOT に設定されます。 `MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT`の詳細については、「 [ALTER database &#40;の SET オプション&#41;transact-sql](/sql/t-sql/statements/alter-database-transact-sql-set-options)」を参照してください。  
  
 または、セッションの分離レベルが READ COMMITTED である場合は、自動コミット トランザクションを使用できます。  
  
 解釈された [!INCLUDE[tsql](../includes/tsql-md.md)] で開始される SNAPSHOT トランザクションは、メモリ最適化テーブルにアクセスできません。  
  
 メモリ最適化テーブルでサポートされるトランザクション分離レベルでは、ディスク ベース テーブルの場合と同じ論理的な保証が得られます。 ただし、分離レベルの保証を提供するために使用されるメカニズムは異なります。  
  
 ディスク ベース テーブルの場合、ほとんどの分離レベルの保証は、ブロックを通じて競合を回避するロックを使用して実装されます。 メモリ最適化テーブルの場合、保証は競合検出メカニズムを使用して適用され、ロックを使用する必要はなくなります。 例外は、ディスク ベース テーブルでの SNAPSHOT 分離です。 この場合は、競合検出メカニズムを使用して、メモリ最適化テーブルでの SNAPSHOT 分離と同じように実装されます。  
  
 SNAPSHOT  
 この分離レベルでは、トランザクションの任意のステートメントによって読み取られるデータが、トランザクションの開始時に存在していたトランザクション上の一貫性のあるバージョンのデータであることを指定します。 データの変更は、トランザクションの開始前にコミットされたものだけが認識されます。 現在のトランザクションの開始後に、他のトランザクションによってデータが変更されても、現在のトランザクションを実行しているステートメントではデータの変更は認識されません。 トランザクション内のステートメントは、トランザクションの開始時に存在していたコミット済みデータのスナップショットを取得します。  
  
 書き込み操作 (更新、挿入、および削除) は、他のトランザクションから常に完全に分離されます。 したがって、SNAPSHOT トランザクションの書き込み操作は、他のトランザクションの書き込み操作と競合する場合があります。 現在のトランザクションの開始以降にコミットされた他のトランザクションによって更新または削除された行を現在のトランザクションで更新または削除しようとすると、トランザクションは次のエラー メッセージにより終了されます。  
  
 エラー 41302。 現在のトランザクションが、トランザクションが開始してから更新されたテーブル X のレコードを更新しようとしました。 トランザクションは中止されました。  
  
 現在のトランザクションの前にコミットされた他のトランザクションによって挿入された行と同じ主キー値を持つ行を現在のトランザクションで挿入しようとすると、次のエラー メッセージによりコミットが失敗します。  
  
 エラー41325。 現在のトランザクションは、SERIALIZABLE の検証の失敗が原因でコミットされませんでした。  
  
 トランザクションのコミット前に削除されたテーブルにトランザクションで書き込む場合、トランザクションは、次のエラー メッセージにより終了します。  
  
 エラー41305。 現在のトランザクションは、REPEATABLE READ の検証の失敗が原因でコミットされませんでした。  
  
 REPEATABLE READ  
 この分離レベルには、SNAPSHOT 分離レベルで適用される保証が含まれています。 また、REPEATABLE READ では、トランザクションで読み取られる任意の行について、トランザクションのコミット時にこの行が他のトランザクションによって変更されていないことが保証されます。 トランザクションのそれぞれの読み取り操作は、トランザクションが完了するまで反復可能です。  
  
 現在のトランザクションの前にコミットされた他のトランザクションによって更新された行を現在のトランザクションで読み取った場合、コミットは次のエラー メッセージにより失敗します。  
  
 エラー41305。 現在のトランザクションは、REPEATABLE READ の検証の失敗が原因でコミットされませんでした。  
  
 SERIALIZABLE  
 この分離レベルには、REPEATABLE READ で適用される保証が含まれています。 スナップショットとトランザクション終了の間にファントム行は表示されていません。 ファントム行は、選択、更新、または削除のフィルター条件に一致します。  
  
 トランザクションは、同時実行トランザクションがないものであるかのように実行されます。 すべてのアクションは、単一のシリアル化ポイント (コミット時) で実質的に発生します。  
  
 これらの保証のいずれかに違反すると、トランザクションは次のエラー メッセージによりコミットされません。  
  
 エラー41325。 現在のトランザクションは、SERIALIZABLE の検証の失敗が原因でコミットされませんでした。  
  
## <a name="see-also"></a>参照  
 [メモリ最適化テーブルのトランザクションについて](../../2014/database-engine/understanding-transactions-on-memory-optimized-tables.md)   
 [メモリ最適化テーブルを使用したトランザクション分離レベルのガイドライン](../relational-databases/in-memory-oltp/memory-optimized-tables.md)   
 [メモリ最適化テーブルでのトランザクションの再試行ロジックのガイドライン](../../2014/database-engine/guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md)  
  
  
