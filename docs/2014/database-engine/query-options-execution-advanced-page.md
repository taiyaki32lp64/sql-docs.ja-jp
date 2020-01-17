---
title: '[クエリオプション] の [実行] ([詳細設定] ページ)Microsoft Docs'
ms.prod: sql-server-2014
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.query.advanced.f1
ms.assetid: 661595ce-99b9-4316-ad80-ed04002d04d5
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: ''
ms.custom: ''
ms.date: 09/03/2019
ms.openlocfilehash: 39a43adeb82b154a076fc7bfc24cc56b54cc8640
ms.sourcegitcommit: 9221a693d4ab7ae0a7e2ddeb03bd0cf740628fd0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2019
ms.locfileid: "71199326"
---
# <a name="query-options-execution-advanced-page"></a>[クエリ オプション] の [実行] ([詳細設定] ページ)

  **SET** ステートメントを使用する際には、さまざまなオプションを指定できます。 このページを使用して Microsoft SQL Server クエリを実行する**SET**オプションを指定します。 各オプションの詳細については、SQL Server オンライン ブックを参照してください。
  
**SET NOCOUNT**結果セットのメッセージとして、行数のカウントを返しません。 既定では、このオプションはオフになっています。

**NOEXEC の設定**クエリを実行しません。 既定では、このオプションはオフになっています。

**SET PARSEONLY**各クエリの構文をチェックしますが、クエリは実行しません。 既定では、このオプションはオフになっています。  

**CONCAT_NULL_YIELDS_NULL の設定**このチェックボックスをオンにすると、既存の値`NULL`とを連結するクエリは、常にを`NULL`結果として返します。 このチェック ボックスがオフの場合、既存の値と `NULL` を連結するクエリは、既存の値を返します。 既定では、このオプションはオンになっています。

**ARITHABORT の設定**このチェックボックスがオンの場合、式`INSERT`の`DELETE`評価`UPDATE`中に、、またはステートメントで算術エラー (オーバーフロー、0による除算、またはドメインエラー) が発生すると、クエリまたはバッチは終了します。 このチェック ボックスがオフの場合、可能であればその値に対して  `NULL` が与えられ、クエリが続行されます。さらに、結果にメッセージが含められます。 この動作の詳細については、オンライン ブックを参照してください。 既定では、このオプションはオンになっています。
  
**SHOWPLAN_TEXT の設定**このチェックボックスをオンにすると、クエリごとにクエリプランがテキスト形式で返されます。 既定では、このオプションはオフになっています。
  
**SET STATISTICS TIME**このチェックボックスをオンにすると、各クエリに対して時間統計が返されます。 既定では、このオプションはオフになっています。
  
**SET STATISTICS IO**このチェックボックスをオンにすると、各クエリに対して入出力 (i/o) に関する統計情報が返されます。 既定では、このオプションはオフになっています。
  
**トランザクション分離レベルの設定**READ COMMITTED トランザクション分離レベルは、既定で設定されています。 詳細については、「[SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql)」を参照してください。 SNAPSHOT transaction 分離レベルは使用できません。 SNAPSHOT 分離を使用するには、次の [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントを追加します。
  
  ```sql
  SET TRANSACTION ISOLATION LEVEL SNAPSHOT;
  GO
  ```

**デッドロックの優先度の設定**既定値の**Normal**では、デッドロックが発生したときに各クエリの優先順位を同じにすることができます。 このクエリがデッドロックの競合で常に敗北し、終了されるクエリとして選択されるようにするには、ドロップダウン リストで優先度 [Low] を選択してください。

**ロックタイムアウトの設定**既定値の-1 は、トランザクションが完了するまでロックが保持されることを示します。 値が 0 の場合は、待ち時間はありません。ロックがかかるとすぐにメッセージが返されます。 トランザクションを終了するまでのロックを 0 ミリ秒よりも長く保持する必要がある場合は、0 より大きい値を指定します。

**QUERY_GOVERNOR_COST_LIMIT の設定**Query **governor cost limit**オプションを使用して、クエリを実行できる期間の上限を指定します。 クエリ コストとは、特定のハードウェア構成でクエリを完了するために必要とされる予測所要時間を秒単位で表したものです。 既定値の 0 は、クエリの実行に関して時間的制限がないことを示します。

**プロバイダーメッセージヘッダー**を表示しないこのチェックボックスがオンの場合、プロバイダーからのステータスメッセージ (OLE DB プロバイダーなど) は表示されません。 既定では、このチェック ボックスはオンになっています。 プロバイダー レベルで失敗するクエリのトラブルシューティングを行うときにプロバイダー メッセージを表示するには、このチェック ボックスをオフにします。

**クエリの実行後に切断する**このチェックボックスがオンの場合、SQL Server への接続は、クエリの完了後に終了します。 既定では、このオプションはオフになっています。

**完了時刻を表示する**クエリの実行が完了した時刻を、クエリ結果または [メッセージ] タブで印刷できます。

**Always Encrypted 用の VBS enclaves の構成証明プロトコル**セキュリティで保護された enclaves で always Encrypted によって使用される、仮想化ベースのセキュリティ (VBS) enclaves の構成証明プロトコルを設定できます。

現在サポートされている構成証明プロトコルは次のとおりです。

* ホストガーディアンサービス-Windows ホストガーディアンサービス (HGS) を使用した構成証明プロトコル。

詳細については、「 [Always Encrypted with secure enclaves](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-enclaves?view=sqlallproducts-allversions) And [Secure エンクレーブ構成証明](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-enclaves?view=sqlallproducts-allversions#secure-enclave-attestation)書」を参照してください。

**[既定値にリセット]** このページ上のすべての値を元の既定値にリセットします。
