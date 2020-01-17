---
title: MDAC から OLE DB Driver for SQL Server へのアプリケーションの更新 | Microsoft Docs
description: MDAC から OLE DB Driver for SQL Server へのアプリケーションの更新
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- MSOLEDBSQL, vs. MDAC
- OLE DB Driver for SQL Server, vs. MDAC
- data access [OLE DB Driver for SQL Server], vs. MDAC
- OLE DB Driver for SQL Server, updating applications
author: pmasl
ms.author: pelopes
ms.openlocfilehash: ad36a17367b14a48810d83137b2887eaa75f6ef1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989263"
---
# <a name="updating-an-application-to-ole-db-driver-for-sql-server-from-mdac"></a>MDAC から OLE DB Driver for SQL Server へのアプリケーションの更新
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server と MDAC (Microsoft Data Access Components) には多くの違いがあります。Windows Vista 以降、データ アクセス コンポーネントは Windows DAC (Windows Data Access Components) と呼ばれています。 どちらを使用しても [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースへのネイティブ データ アクセスは可能ですが、OLE DB Driver for SQL Server は、旧バージョンとの互換性を維持しながら、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の新機能を公開するように設計されています。   

 また、MDAC には OLE DB、ODBC、および ActiveX データオブジェクト (ADO) を使用するためのコンポーネントが含まれていますが、OLE DB SQL Server Driver は OLE DB を実装するだけです (ただし、ADO は OLE DB Driver for SQL Server の機能にアクセスできます)。  

 SQL Server と MDAC の OLE DB ドライバーは、次の点で異なります。  

-   ADO を使用して SQL Server の OLE DB ドライバーにアクセスするユーザーは、SQL OLE DB プロバイダーにアクセスしたときよりもフィルター機能が低下する可能性があります。  

-   ADO アプリケーションで SQL Server に OLE DB ドライバーを使用し、計算列を更新しようとすると、エラーが報告されます。 MDAC では、更新が受け付けられたうえで、無視されていました。  

-   SQL Server 用の OLE DB ドライバーは、単一の自己完結型ダイナミックリンクライブラリ (DLL) ファイルです。 配布を容易にすることと、セキュリティの危険にさらされるのを防ぐことの両面から、最小限のインターフェイスしか公開されません。  

-   OLE DB インターフェイスのみがサポートされています。  

-   SQL Server 名の OLE DB ドライバーは、MDAC で使用される名前とは異なります。  

-   OLE DB Driver for SQL Server を使用すると、MDAC コンポーネントによって提供されるユーザー補助機能を利用できます。 この機能には、接続プーリング、ADO サポート、クライアント カーソルのサポートなどがあります。 これらの機能のいずれかを使用すると、OLE DB Driver for SQL Server ではデータベース接続のみが提供されます。 MDAC は、トレース、管理制御、およびパフォーマンス カウンターなどの機能を提供します。  

-   アプリケーションでは、OLE DB Driver for SQL Server と共に OLE DB Core Services を使用できます。ただし、OLE DB カーソル エンジンを使用する場合、このカーソル エンジンでは新しい [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] のデータ型が認識されないため、発生する可能性のある問題を回避するために、アプリケーションでデータ型互換性オプションを使用する必要があります。  

-   SQL Server 用の OLE DB ドライバーは、以前[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のデータベースへのアクセスをサポートします。  

-   SQL Server 用の OLE DB ドライバーには、XML 統合が含まれていません。 SQL Server 用の OLE DB ドライバーは、SELECT...FOR XML クエリでは、他の XML 機能はサポートされていません。 ただし、OLE DB Driver for SQL Server では、 で[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]導入された **xml** データ型がサポートされています。  

-   OLE DB Driver for SQL Server では、接続文字列の属性のみを使用する、クライアント側のネットワーク ライブラリの構成がサポートされます。 ネットワーク ライブラリをさらに詳細に構成する場合は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 構成マネージャーを使用する必要があります。  

-   MDAC 接続文字列では、 **Trusted_Connection**キーワードにブール値 (**true**) を使用できます。 SQL Server 接続文字列の OLE DB ドライバーでは、 **yes**または**no**を使用する必要があります。  

-   警告とエラーが一部変更されています。 サーバーから返される警告とエラーの重大度は、OLE DB Driver for SQL Server に渡されるときも保持されるようになりました。 特定の警告やエラーのトラッピングに依存しているアプリケーションは、十分にテストする必要があります。  

-   OLE DB Driver for SQL Server では、MDAC よりも厳密なエラー チェックが行われます。そのため、アプリケーションが OLE DB の仕様に厳密に準拠していないときには動作が異なることがあります。 たとえば、SQLOLEDB プロバイダーでは、結果のパラメーターの名前を '\@' で始める必要があるという規則を適用していなかったのに対して、OLE DB Driver for SQL Server では適用します。  

-   SQL Server の OLE DB ドライバーは、失敗した接続に関する MDAC とは動作が異なります。 たとえば、MDAC では接続が失敗した場合はキャッシュされたプロパティ値を返しますが、OLE DB Driver for SQL Server では呼び出し元のアプリケーションにエラーを報告します。  

-   OLE DB Driver for SQL Server では、Visual Studio Analyzer イベントは生成されませんが、代わりに Windows トレース イベントが生成されます。  

-   OLE DB Driver for SQL Server を perfmon と共に使用することはできません。 パフォーマンス モニターは、Windows に付属している MDAC SQLODBC ドライバーを使用する DSN のみと併用できる Windows ツールです。  

-   OLE DB Driver for SQL Server が以降のバージョン[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]に接続されている場合、サーバーエラー16947が SQL_ERROR として返されます。 このエラーは、位置指定更新または位置指定削除による行の更新や削除が失敗したときに発生します。 任意のバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に接続している MDAC では、サーバー エラー 16947 は警告 (SQL_SUCCESS_WITH_INFO) として返されます。  

-   OLE DB Driver for SQL Server には、以前は実装されていなかった、省略可能な OLE DB インターフェイスの **IDBDataSourceAdmin** インターフェイスが実装されています。ただし、この省略可能なインターフェイスに実装されているのは **CreateDataSource** メソッドのみです。 [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  

-   OLE DB Driver for SQL Server では、TABLE_TYPE を SYNONYM に設定すると、TABLES スキーマ行セットと TABLE_INFO スキーマ行セットのシノニムを返します。  

-   **varchar(max)** データ型、**nvarchar(max)** データ型、**varbinary(max)** データ型、**xml** データ型、**udt** データ型、またはその他のラージ オブジェクト型の戻り値を [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] より前のバージョンのクライアントに返すことはできません。 これらの型を戻り値として使用する場合は、OLE DB Driver for SQL Server を使用する必要があります。  

-   手動および暗黙のトランザクション開始時において、以下のステートメントの実行が MDAC では許可されていましたが、OLE DB Driver for SQL Server では許可されません。 これらは、自動コミット モードで実行する必要があります。  

    -   すべてのフルテキスト操作 (インデックスおよびカタログ DDL)  

    -   すべてのデータベース操作 (データベースの作成、変更、および削除)  

    -   再構成時  

    -   Shutdown  

    -   Kill  

    -   バックアップ  

-   MDAC アプリケーションから [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に接続すると、[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] で導入されたデータ型は、次の表に示すような、[!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] と互換性を持つデータ型として扱われます。  

    |SQL Server 2005 の型|SQL Server 2000 の型|  
    |--------------------------|--------------------------|  
    |**varchar(max)**|**text**|  
    |**nvarchar(max)**|**ntext**|  
    |**varbinary(max)**|**image**|  
    |**udt**|**varbinary**|  
    |**xml**|**ntext**|  

     この型マッピングは、列のメタデータに返される値に影響を与えます。 たとえば、**テキスト**列の最大サイズは2147483647ですが、OLE DB Driver for SQL Server では、プラットフォームに応じて、 **varchar (max)** 列の最大サイズが2147483647または-1 として報告されます。  

-   OLE DB Driver for SQL Server では、旧バージョンとの互換性を維持するために接続文字列のあいまい性が許可されます (たとえば、キーワードを複数回指定したり、位置や優先順位に基づいた解決方法を使用して、競合するキーワードを指定したりすることができます)。 OLE DB Driver for SQL Server の今後のリリースでは、接続文字列のあいまいさが許容されない場合があります。 OLE DB Driver for SQL Server を使用するアプリケーションでは、あいまいな接続文字列を利用しないように変更することをお勧めします。  

-   OLE DB 呼び出しを使用してトランザクションを開始する場合、SQL Server と MDAC の OLE DB ドライバーの動作に違いがあります。トランザクションは OLE DB Driver for SQL Server で直ちに開始されますが、トランザクションは MDAC を使用して最初のデータベースにアクセスした後に開始されます。 これはストアド プロシージャとバッチの動作に影響を与える可能性があります。[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、バッチまたはストアド プロシージャの実行開始時と実行終了後で @@TRANCOUNT の値が同じである必要があるためです。  

-   OLE DB Driver for SQL Server では、ITransactionLocal:: BeginTransaction によってトランザクションが直ちに開始されます。 MDAC では、暗黙のトランザクション モードでのトランザクションを必要とするステートメントがアプリケーションで実行されるまで、トランザクションの開始が遅延されました。 詳細については、「[SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../../t-sql/statements/set-implicit-transactions-transact-sql.md)」を参照してください。  


 SQL Server と MDAC 用の OLE DB ドライバーはどちらも、行のバージョン管理を使用した read committed トランザクション分離をサポートしますが、スナップショットトランザクション分離をサポートしているのは、SQL Server の OLE DB ドライバーだけです。 (プログラミング用語では、「行のバージョン管理機能を使用した Read Committed トランザクション分離」は「Read Committed トランザクション」と同義語です)。  

## <a name="see-also"></a>参照  
 [OLE DB Driver for SQL Server を使用したアプリケーションの構築](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
