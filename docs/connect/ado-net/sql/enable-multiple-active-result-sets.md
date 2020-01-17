---
title: 複数のアクティブな結果セットの有効化
description: MARS を SQL Server で使用する方法について説明します。
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: 576079e4-debe-4ab5-9204-fcbe2ca7a5e2
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: d0c40df5ec7648b7073f9efa369428b8d88f6d11
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452219"
---
# <a name="enabling-multiple-active-result-sets"></a>複数のアクティブな結果セットの有効化

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET をダウンロードする](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

複数のアクティブな結果セット (MARS : Multiple Active Result Set) は、SQL Server で動作する機能であり、複数のバッチを単一の接続で実行することができます。 SQL Server で使用できるように MARS が有効になっているときは、使用中の各コマンド オブジェクトは接続にセッションを追加します。  
  
> [!NOTE]
>  1つの MARS セッションで、MARS が使用する1つの論理接続と、アクティブなコマンドごとに1つの論理接続を開きます。  
  
## <a name="enabling-and-disabling-mars-in-the-connection-string"></a>接続文字列で MARS を有効または無効にする  
  
> [!NOTE]
>  次の接続文字列では、SQL Server に含まれるサンプルの **AdventureWorks** データベースを使用します。 指定された接続文字列は、データベースが MSSQL1 という名前のサーバーにインストールされていることを前提としています。 必要に応じて、環境に合わせて接続文字列を変更します。  
  
MARS 機能は、既定では無効化されています。 これを有効にするには、接続文字列に "MultipleActiveResultSets = True" キーワードペアを追加します。 "True" は、MARS を有効にするための唯一の有効な値です。 次の例では、SQL Server のインスタンスに接続する方法と、MARS を有効にするように指定する方法を示します。 
  
```csharp  
string connectionString = "Data Source=MSSQL1;" +   
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" +  
    "MultipleActiveResultSets=True";  
```  
  
MARS を無効にするには、接続文字列に "MultipleActiveResultSets = False" キーワードペアを追加します。 "False" は、MARS を無効にするための唯一の有効な値です。 次の接続文字列は、MARS を無効にする方法を示しています。  
  
```csharp  
string connectionString = "Data Source=MSSQL1;" +   
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" +  
    "MultipleActiveResultSets=False";  
```  
  
## <a name="special-considerations-when-using-mars"></a>MARS を使用する場合の特別な考慮事項  
一般に、MARS が有効な接続を使用するには、既存のアプリケーションで変更を行う必要はありません。 ただし、アプリケーションで MARS 機能を使用する場合は、次の特別な考慮事項を理解しておく必要があります。  
  
### <a name="statement-interleaving"></a>ステートメントのインターリーブ  
MARS 操作は、サーバー上で同期的に実行されます。 SELECT ステートメントと BULK INSERT ステートメントのステートメントインターリーブは許可されています。 ただし、データ操作言語 (DML) ステートメントとデータ定義言語 (DDL) ステートメントはアトミックに実行されます。 アトミックバッチの実行中に実行しようとしたステートメントはブロックされます。 サーバーでの並列実行は MARS 機能ではありません。  
  
2つのバッチが MARS 接続で送信され、そのうちの1つに SELECT ステートメントが含まれている場合、もう一方が DML ステートメントを含んでいる場合、その DML は SELECT ステートメントの実行中に実行を開始できます。 ただし、SELECT ステートメントを実行する前に、DML ステートメントを完了する必要があります。 両方のステートメントが同じトランザクションで実行されている場合、SELECT ステートメントの実行を開始した後に DML ステートメントによって行われた変更は、読み取り操作では表示されません。  
  
SELECT ステートメント内の WAITFOR ステートメントでは、待機中、つまり最初の行が生成されるまで、トランザクションは生成されません。 これは、WAITFOR ステートメントが待機している間に、同じ接続内で他のバッチを実行できないことを意味します。  
  
### <a name="mars-session-cache"></a>MARS セッションキャッシュ  
MARS が有効になっている接続が開かれると、論理セッションが作成されます。これにより、オーバーヘッドが増加します。 オーバーヘッドを最小化してパフォーマンスを向上させるため、**SqlClient** は接続内の MARS セッションをキャッシュします。 キャッシュには、最大で10個の MARS セッションが含まれています。 この値はユーザーが調整できません。 セッション制限に達した場合、新しいセッションが作成されます。エラーは生成されません。 キャッシュとそれに含まれるセッションは接続ごとになります。接続間で共有されることはありません。 セッションが解放されると、プールの上限に達していない限り、プールに返されます。 キャッシュプールがいっぱいになると、セッションは閉じられます。 MARS セッションの有効期限は切れません。 これらのオブジェクトは、接続オブジェクトが破棄されたときにのみクリーンアップされます。 MARS セッションキャッシュはプリロードされていません。 アプリケーションが追加のセッションを必要とするときに読み込まれます。  
  
### <a name="thread-safety"></a>スレッド セーフ  
MARS 操作はスレッドセーフではありません。  
  
### <a name="connection-pooling"></a>接続のプール  
MARS が有効な接続は、他の接続と同じようにプールされます。 アプリケーションが2つの接続を開き、MARS が有効になっていて、MARS が無効になっている場合、2つの接続は別々のプールにあります。
  
### <a name="sql-server-batch-execution-environment"></a>SQL Server バッチ実行環境  
接続が開かれると、既定の環境が定義されます。 この環境は、論理 MARS セッションにコピーされます。  
  
バッチ実行環境には、次のコンポーネントが含まれています。  
  
- Set オプション (ANSI_NULLS、DATE_FORMAT、LANGUAGE、など)  
  
- セキュリティコンテキスト (ユーザー/アプリケーションロール)  
  
- データベースコンテキスト (現在のデータベース)  
  
- 実行状態変数 (例、@ @ERROR、@ @ROWCOUNT、@ @FETCH_STATUS @ @IDENTITY)  
  
- 最上位レベルの一時テーブル  
  
MARS では、既定の実行環境が接続に関連付けられます。 特定の接続の下で実行を開始するすべての新しいバッチは、既定の環境のコピーを受け取ります。 特定のバッチでコードを実行するたびに、環境に加えられたすべての変更のスコープは特定のバッチになります。 実行が完了すると、実行設定が既定の環境にコピーされます。 1つのバッチによって複数のコマンドが同じトランザクションで順番に実行される場合、セマンティクスは、以前のクライアントまたはサーバーに関連する接続によって公開されているものと同じになります。  
  
### <a name="parallel-execution"></a>並列実行  
MARS は、アプリケーション内の複数の接続のすべての要件を削除するようには設計されていません。 アプリケーションでサーバーに対してコマンドを実際に並列実行する必要がある場合は、複数の接続を使用する必要があります。  
  
たとえば、次のシナリオを考えてみます。 2つのコマンドオブジェクトが作成されます。1つは結果セットの処理用、もう1つはデータの更新用です。MARS を使用して共通の接続を共有します。 最初のコマンド オブジェクトの結果をすべて読み取るまで、`Transaction`.`Commit` による 更新に失敗し、次の例外が発生します。  
  
メッセージ: トランザクション コンテキストを他のセッションが使用中です。  
  
ソース: Microsoft SqlClient Data Provider  
  
が必要です: (null)  
  
受信した: SqlException  
  
このシナリオを処理するには、次の3つのオプションがあります。  
  
- トランザクションの一部ではないように、リーダーが作成された後にトランザクションを開始します。 すべての更新は、独自のトランザクションになります。  
  
- リーダーが閉じられた後、すべての作業をコミットします。 これには、大量の更新が含まれている可能性があります。  
  
- MARS は使用しないでください。代わりに、MARS より前と同じように、コマンドオブジェクトごとに個別の接続を使用します。  
  
### <a name="detecting-mars-support"></a>MARS サポートの検出  
アプリケーションでは、`SqlConnection.ServerVersion` の値を読み取ることで、MARS のサポートを確認できます。 メジャー番号は、SQL Server 2005 の場合は9、SQL Server 2008 の場合は10にする必要があります。  
  
## <a name="next-steps"></a>次の手順
- [複数のアクティブな結果セット (MARS)](multiple-active-result-sets-mars.md)
