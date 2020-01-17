---
title: Native Client、MDAC からアプリの SQL を更新する
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- SQLNCLI, vs. MDAC
- SQL Server Native Client, vs. MDAC
- data access [SQL Server Native Client], vs. MDAC
- SQL Server Native Client, updating applications
ms.assetid: 2860efdd-c59a-4deb-8a0e-5124a8f4e6dd
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f8f6b7efd8d97f63e93061cbef1a54e1df3146d2
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75243785"
---
# <a name="updating-an-application-to-sql-server-native-client-from-mdac"></a>MDAC から SQL Server Native Client へのアプリケーションの更新
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client と MDAC (Microsoft Data Access Components) には多くの違いがあります (Windows Vista 以降、このデータ アクセス コンポーネントは Windows DAC (Windows Data Access Components) と呼ばれています)。 どちらを使用しても [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースへのネイティブ データ アクセスは可能ですが、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client は、旧バージョンとの互換性を維持しながら、[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] の新機能を公開することを主眼において作成されています。  
  
 このトピックの情報は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に付属するバージョンの [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client に対応するように MDAC (Windows DAC) アプリケーションを更新する場合に役立ちます。 に[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]付属している native client のバージョンでこのアプリケーションを最新の状態にする方法については、「 [SQL Server 2005 Native client からアプリケーションを更新](../../../relational-databases/native-client/applications/updating-an-application-from-sql-server-2005-native-client.md)する」を参照してください。  
  
 また、MDAC には OLE DB、ODBC、および ADO (ActiveX Data Objects) を使用するためのコンポーネントが含まれていますが、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client には、OLE DB と ODBC しか実装されていません (ただし、ADO から [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client の機能にアクセスすることはできます)。  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client と MDAC のその他の違いを次に示します。  
  
-   ADO を使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client プロバイダーにアクセスした場合に使用できるフィルター機能は、同じユーザーが SQL OLE DB プロバイダーにアクセスした場合よりも少ないことがあります。  
  
-   ADO アプリケーションで [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client を使用している場合に計算列の更新を試みると、エラーが報告されます。 MDAC では、更新が受け付けられたうえで、無視されていました。  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client は、1 つの自己完結型 DLL (ダイナミック リンク ライブラリ) ファイルです。 配布を容易にすることと、セキュリティの危険にさらされるのを防ぐことの両面から、最小限のインターフェイスしか公開されません。  
  
-   OLE DB インターフェイスと ODBC インターフェイスのみがサポートされます。  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client の OLE DB プロバイダー名と ODBC ドライバー名は、MDAC で使用されるものと異なります。  
  
-   MDAC コンポーネントによって提供される、ユーザーがアクセスできる機能は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client の使用時に使用できます。 この機能には、接続プーリング、ADO サポート、クライアント カーソルのサポートなどがあります。 このような機能を使用するとき、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ではデータベース接続のみが提供されます。 MDAC は、トレース、管理制御、およびパフォーマンス カウンターなどの機能を提供します。  
  
-   アプリケーションでは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client と共に OLE DB Core Services を使用できます。ただし、OLE DB カーソル エンジンを使用している場合、このカーソル エンジンでは新しい [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] のデータ型が認識されないので、アプリケーションでデータ型互換性オプションを使用して、問題が発生しないようにする必要があります。  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client は、以前の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースへのアクセスをサポートしています。  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client には、XML の統合は含まれていません。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client は SELECT...FOR XML クエリでは、他の XML 機能はサポートされていません。 ただし、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client では、 **** で[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]導入された xml データ型がサポートされています。  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client では、接続文字列の属性のみを使用する、クライアント側のネットワーク ライブラリの構成がサポートされます。 ネットワーク ライブラリをさらに詳細に構成する場合は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 構成マネージャーを使用する必要があります。  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client には、odbcbcp.dll との互換性がありません。 ODBC api と**bcp** api の両方を使用するアプリケーションは、Native Client を使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]するために sqlncli11 とリンクするように再構築する必要があります。  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client は、MSDASQL (Microsoft OLE DB Provider for ODBC) からはサポートされません。 MDAC SQLODBC ドライバーを MSDASQL と共に使用しているか、MDAC SQLODBC ドライバーを ADO と共に使用している場合は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client の OLE DB を使用してください。  
  
-   MDAC 接続文字列を使用すると、ブール値 (**true**) を**Trusted_Connection**キーワードに設定できます。 Native [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Client 接続文字列では、 **yes**または**no**を使用する必要があります。  
  
-   警告とエラーが一部変更されています。 サーバーから返される警告とエラーの重大度は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client に渡されるときも保持されるようになりました。 特定の警告やエラーのトラッピングに依存しているアプリケーションは、十分にテストする必要があります。  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client では、MDAC よりも厳密なエラー チェックが行われます。そのため、アプリケーションが ODBC と OLE DB の仕様に厳密に準拠していないときには動作が異なることがあります。 たとえば、SQLOLEDB プロバイダーは、結果パラメーターとしてパラメーター名を '\@' で始める必要がありますが、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーはこの規則を適用しませんでした。  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client では、接続が失敗したときの動作が MDAC と異なります。 たとえば、MDAC では接続が失敗した場合はキャッシュされたプロパティ値を返しますが、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client では呼び出し元のアプリケーションにエラーを報告します。  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client では、Visual Studio Analyzer イベントは生成されませんが、代わりに Windows トレース イベントが生成されます。  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client をパフォーマンス モニターと併用することはできません。 パフォーマンス モニターは、Windows に付属している MDAC SQLODBC ドライバーを使用する DSN のみと併用できる Windows ツールです。  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client を [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降のバージョンに接続すると、サーバー エラー 16947 が SQL_ERROR として返されます。 このエラーは、位置指定更新または位置指定削除による行の更新や削除が失敗したときに発生します。 任意のバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に接続している MDAC では、サーバー エラー 16947 は警告 (SQL_SUCCESS_WITH_INFO) として返されます。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client では、 **IDBDataSourceAdmin**インターフェイスが実装されています。これは、以前に実装されていないオプションの OLE DB インターフェイスですが、この省略可能なインターフェイスの**createdatasource**メソッドのみが実装されています。 [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーでは、TABLE_TYPE を SYNONYM に設定すると、TABLES スキーマ行セットと TABLE_INFO スキーマ行セットのシノニムを返します。  
  
-   データ型**varchar (max)**、 **nvarchar (max)**、 **varbinary (max)**、 **xml**、 **udt**、またはその他のラージオブジェクト型の戻り値は、よりも[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]前のバージョンのクライアントには返すことができません。 これらの型を戻り値として使用する場合は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client を使用する必要があります。  
  
-   手動および暗黙のトランザクション開始時において、以下のステートメントの実行が MDAC では許可されていましたが、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client では許可されません。 これらは、自動コミット モードで実行する必要があります。  
  
    -   すべてのフルテキスト操作 (インデックスおよびカタログ DDL)  
  
    -   すべてのデータベース操作 (データベースの作成、変更、および削除)  
  
    -   再構成  
  
    -   Shutdown  
  
    -   強制終了  
  
    -   バックアップ  
  
-   MDAC アプリケーションから [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に接続すると、[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] で導入されたデータ型は、次の表に示すような、[!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] と互換性を持つデータ型として扱われます。  
  
    |SQL Server 2005 の型|SQL Server 2000 の型|  
    |--------------------------|--------------------------|  
    |**varchar (max)**|**本文**|  
    |**nvarchar (max)**|**ntext**|  
    |**varbinary (max)**|**絵**|  
    |**udt**|**可変長**|  
    |**xml**|**ntext**|  
  
     この型マッピングは、列のメタデータに返される値に影響を与えます。 たとえば、**テキスト**列の最大サイズは2147483647ですが[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 、native client ODBC では最大サイズの**varchar (max)** 列が SQL_SS_LENGTH_UNLIMITED として報告[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]されます。また、native client OLE DB では、プラットフォームに応じて、 **varchar (max)** 列の最大サイズが2147483647または-1 として報告されます。  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client では、旧バージョンとの互換性を維持するために接続文字列のあいまい性が許可されます。たとえば、キーワードを複数回指定したり、位置と優先順位に基づいた解決方法を使用して、競合するキーワードを指定することができます。 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client の今後のリリースでは、あいまいな接続文字列を使用できなくなる可能性があります。 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client を使用するアプリケーションでは、あいまいな接続文字列を利用しないように変更することをお勧めします。  
  
-   ODBC または OLE DB 呼び出しを使用してトランザクションを開始した場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client と MDAC とでは動作が異なります。[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ではトランザクションがすぐに開始されますが、MDAC では最初のデータベース アクセスの後にトランザクションが開始されます。 これは、バッチまたはストアドプロシージャが開始さ[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]れ\@ \@たときと同じように、バッチまたはストアドプロシージャの実行が完了した後に、TRANCOUNT を同じにする必要があるので、ストアドプロシージャとバッチの動作に影響を与える可能性があります。  
  
-   Native [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Client では、ITransactionLocal:: BeginTransaction によってトランザクションがすぐに開始されます。 MDAC では、暗黙のトランザクション モードを必要とするステートメントをアプリケーションが実行するまで、トランザクションの開始が遅延されました。 詳細については、「[SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../../t-sql/statements/set-implicit-transactions-transact-sql.md)」を参照してください。  
  
-   Native Client driver を system.string と[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]共に使用して、新しい、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]固有のデータ型または機能を公開するサーバーコンピューターにアクセスすると、エラーが発生する場合があります。 System.string では、汎用の ODBC 実装が提供されます。その後、ベンダー固有の機能や拡張機能は公開されません。 (Native [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Client ドライバーは、最新[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の機能をネイティブにサポートするように更新されています)。この問題を回避するには、MDAC に戻すか、または system.string に移行します。  
  
 行のバージョン管理機能を使用した Read Committed トランザクション分離は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client と MDAC の両方でサポートされていますが、スナップショット トランザクション分離は [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client のみでサポートされています  (プログラミング用語では、「行のバージョン管理機能を使用した Read Committed トランザクション分離」は「Read Committed トランザクション」と同義語です)。  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client を使用したアプリケーションの構築](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
