---
title: 共通言語ランタイム (CLR) 統合の使用状況のシナリオと例 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- scenarios [CLR integration]
- common language runtime [SQL Server], samples
- examples [CLR integration]
- sample applications [CLR integration]
- database objects [CLR integration], samples
- managed code [SQL Server], samples
ms.assetid: 33aac25f-abb4-4f29-af88-4a0dacd80ae7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3718a084211e7c3b2b7a14973e195a4b1c3b6b1a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62780725"
---
# <a name="usage-scenarios-and-examples-for-common-language-runtime-clr-integration"></a>CLR (共通言語ランタイム) 統合の使用シナリオと例
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、サンプル アプリケーション、パッケージ サンプル、およびさまざまなコーディング サンプルが含まれています。これらのサンプルを使用することで、CLR (共通言語ランタイム) 統合のプログラミング機能について理解することができます。  
  
 完全な Visual Studio プロジェクトがこれらのサンプルと追加資料を実装する、次を参照してください。 [codeplex のサンプル (&)、Microsoft SQL Server コミュニティのプロジェクト](https://go.microsoft.com/fwlink/?LinkID=193935)します。  
  
|名前|説明|  
|----------|-----------------|  
|[CLR UDF からのネイティブ コードへのアクセス](../../../2014/database-engine/dev-guide/accessing-native-code-from-a-clr-udf.md)|アセンブリ内のユーザー定義関数に含まれるネイティブ (アンマネージ) C++ コードの関数をデータベースから呼び出す方法を紹介します。|  
|[Array パラメーター サンプル](../../../2014/database-engine/dev-guide/array-parameter-sample.md)|クライアントからサーバー上の CLR 統合ストアド プロシージャに情報の配列を渡すことで、データベース内の一連の行を作成、更新、または削除する方法を例示します。 この処理は、UDT を使って行っています。|  
|[カレンダー対応の日付と時刻 UDT サンプル](../../../2014/database-engine/dev-guide/calendar-aware-date-and-time-udt-sample.md)|日付と時刻のカレンダー対応処理を提供する 2 つの UDT を定義します。|  
|[CLR Transactions サンプル](../../../2014/database-engine/dev-guide/clr-transactions-sample.md)|System.Transactions 名前空間にあるマネージド API を使用してトランザクションを制御する例を示します。|  
|[CLR と XML を使用した連絡先の作成](../../../2014/database-engine/dev-guide/contact-creation-using-clr-and-xml.md)|SQL Server の Contact サンプルは、基礎となる AdventureWorks2012 サンプル データベースに新しい機能の層を追加する便利なユーティリティをいくつか提供します。 1 つ目のユーティリティは、AdventureWorks2012 データベースに関係した、さまざまな人々の連絡先のレコードを作成します。 連絡先の情報は XML を使用して指定され、XML を作成してデータベースの適切なテーブルに配置するための C# ベースのストアド プロシージャまたは VB ストアド プロシージャに渡されます。|  
|[通貨型と変換関数](../../../2014/database-engine/dev-guide/currency-type-and-conversion-function.md)|C# を使用して Currency ユーザー定義データ型を定義します。|  
|[CLR を使用したラージ オブジェクトの処理](../../../2014/database-engine/dev-guide/handling-large-objects-using-clr.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と、サーバーからアクセスできるファイル システムとの間で、CLR ストアド プロシージャを使用して LOB (ラージ バイナリ オブジェクト) を転送する例を示します。|  
|[Hello World Ready サンプル](../../../2014/database-engine/dev-guide/hello-world-ready-sample.md)|CLR 統合に基づく簡単な国際化対応のストアド プロシージャを作成、配置、およびテストする基本的な操作を例示します。|  
|[Hello World サンプル](../../../2014/database-engine/dev-guide/hello-world-sample.md)|CLR 統合に基づく簡単なストアド プロシージャを作成、配置、およびテストする基本的な操作を例示します。|  
|[インプロセス データ アクセス サンプル](../../../2014/database-engine/dev-guide/in-process-data-access-sample.md)|CLR インプロセス データ アクセス プロバイダーのさまざまな機能を例示する簡単な関数が数多く含まれています。|  
|[結果セットのサンプル](../../../2014/database-engine/dev-guide/result-set-sample.md)|クエリの結果全体を読み取るときに、新しい接続を開かず、すべての結果をメモリに読み込まずにコマンドを実行する方法を例示します。|  
|[Send DataSet サンプル](../../../2014/database-engine/dev-guide/send-dataset-sample.md)|サーバー側の CLR ベースのストアド プロシージャ内で、クライアントへの結果セットとして ADO.NET ベースのデータセットを返す方法を示します。|  
|[文字列ユーティリティ関数サンプル](../../../2014/database-engine/dev-guide/string-utility-functions-sample.md)|Visual C# と Visual Basic で記述されたストリーミング TVF (テーブル値関数) が含まれています。この関数は、コンマ区切りの文字列を 1 列のテーブルに分割します。|  
|[補助文字対応文字列操作サンプル](../../../2014/database-engine/dev-guide/supplementary-aware-string-manipulation-sample.md)|Unicode 文字列とサロゲート文字列の両方を処理できる、補助文字対応の 5 つの [!INCLUDE[tsql](../../includes/tsql-md.md)] 文字列関数の実装を示します。|  
|[UDT ユーティリティ](../../../2014/database-engine/dev-guide/udt-utilities.md)|多くの UDT (ユーザー定義データ型) ユーティリティ関数が含まれています。|  
|[未使用のアセンブリのクリーンアップ](../../../2014/database-engine/dev-guide/unused-assembly-cleanup.md)|メタデータ カタログに対してクエリを実行して、現在のデータベース内で使用されていないアセンブリを削除する .NET ストアド プロシージャが含まれています。|  
|[ユーザー定義型](../../../2014/database-engine/dev-guide/user-defined-type.md)|[!INCLUDE[tsql](../../includes/tsql-md.md)] と、System.Data.SqlClient を使用するクライアント アプリケーションの両方から、簡単な UDT を作成および使用する方法を示します。|  
|[UTF8 文字列ユーザー定義データ型&#40;UDT&#41;](../../../2014/database-engine/dev-guide/utf8-string-user-defined-data-type-udt.md)|UTF8 エンコードされた値を格納するために、データベースの型システムを拡張する UDT の実装を例示します。|  
  
  
