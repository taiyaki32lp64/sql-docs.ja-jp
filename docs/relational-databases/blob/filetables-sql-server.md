---
title: FileTables (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], overview
- FileTables [SQL Server]
- FileTable [SQL Server], see FileTables [SQL Server]
- FileTable [SQL Server]
ms.assetid: a57b629c-e9ed-48fd-9a48-ed3787d80c8f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8993c5e9ea1334b5bb8a002f1991041886a9f282
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125168"
---
# <a name="filetables-sql-server"></a>FileTables (SQL Server)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  FileTable 機能は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に格納されているファイル データに対して Windows ファイル名前空間のサポートと Windows アプリケーションとの互換性を提供します。 FileTable により、アプリケーションは、ストレージとデータ管理コンポーネントを統合し、非構造化データおよびメタデータに対する統合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス (フルテキスト検索、セマンティック検索など) を提供できます。  
  
 つまり、ファイルおよびドキュメントを FileTable と呼ばれる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の特殊なテーブルに保存しておき、ファイル システムに格納されているかのように、Windows アプリケーションからこれらのファイルおよびドキュメントにアクセスできるということです。このとき、クライアント アプリケーションに変更を加える必要はありません。  
  
 FileTable の機能は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の FILESTREAM テクノロジをベースとして構築されています。 FILESTREAM の詳細については、「[FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)」を参照してください。  
  
##  <a name="Goals"></a> FileTable 機能の利点  
 FileTable 機能の目的は、次のとおりです。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース内に格納されたファイル データに対する Windows API の互換性。 Windows API の互換性は、次のとおりです。  
  
    -   非トランザクション ストリーム アクセスと FILESTREAM データのインプレース更新。  
  
    -   ディレクトリおよびファイルの階層構造の名前空間。  
  
    -   作成日や更新日などのファイル属性の保管。  
  
    -   Windows ファイルおよびディレクトリ管理 API のサポート。  
  
-   FILESTREAM およびファイル属性データに対する管理ツール、サービス、リレーショナル クエリなど、他の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 機能との互換性。  
  
 このようにして、FileTable は、現在ファイル サーバーにファイルとして格納されている非構造化データを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で保管および管理するうえでの大きな障壁を取り除きます。 企業は、このデータをファイル サーバーから FileTable に移動して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]が提供する統合管理およびサービスを活用できます。 それと同時に、ファイル システムでこのデータをファイルとして認識する既存の Windows アプリケーションとの互換性を維持することもできます。  
 
  
##  <a name="Description"></a> FileTable とは  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、データベース内のファイルとディレクトリのストレージを必要とするアプリケーションに対して、Windows API の互換性および非トランザクション アクセスによって、特殊な **ファイルのテーブル**( **FileTable**と呼ばれます) を提供します。 FileTable は、FILESTREAM データ、ファイルとディレクトリの階層の情報、およびファイル属性を保存するための定義済みのスキーマを持つ、特殊なユーザー テーブルです。  
  
 FileTable には、次の機能が含まれています。  
  
-   FileTable は、ディレクトリおよびファイルの階層を表します。 含まれるディレクトリおよびファイルの両方について、その階層のすべてのノードに関連するデータを格納します。 この階層は、FileTable を作成するときに指定するルート ディレクトリから始まります。  
  
-   FileTable のどの行も、ファイルまたはディレクトリを表します。  
  
-   各行には次のアイテムが含まれます。 FileTable のスキーマの詳細については、「 [FileTable スキーマ](../../relational-databases/blob/filetable-schema.md)」を参照してください。  
  
    -   ストリーム データ用の **file_stream** 列、および **stream_id** (GUID) 識別子 ( **file_stream** 列はディレクトリでは NULL です)。  
  
    -   現在のアイテム (ファイルまたはディレクトリ) 、およびディレクトリ階層を表して保持するための、**path_locator** 列と **parent_path_locator** 列の両方。  
  
    -   ファイル I/O API で便利な、作成日や更新日などの 10 のファイル属性。  
  
    -   ファイルやドキュメント全体に対するフルテキスト検索およびセマンティック検索をサポートする型列。  
  
-   FileTable は、ファイル名前空間のセマンティクスを維持するため、特定のシステム定義の制約とトリガーを適用します。  
  
-   非トランザクション アクセスでデータベースが構成されている場合、FileTable で表されるファイルおよびディレクトリの階層は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに構成された FILESTREAM 共有の下で公開されます。 これにより、Windows アプリケーションはファイル システムにアクセスできるようになります。  
  
 FileTable の他の特性は、次のとおりです。  
  
-   FileTable に格納されているファイルおよびディレクトリ データは、Windows API ベースのアプリケーションが非トランザクション ファイル アクセスを行うための Windows 共有によって公開されます。 Windows アプリケーションでは、これは通常のファイルおよびディレクトリの共有のように見えます。 アプリケーションは、豊富な Windows API のセットを使用して、この共有のファイルおよびディレクトリを管理できます。  
  
-   共有によって公開されるディレクトリ階層は、FileTable 内で保持されている、純粋に論理的なディレクトリ構造です。  
  
-   Windows 共有によるファイルまたはディレクトリの作成または変更の呼び出しは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントによってインターセプトされ、FileTable の対応するリレーショナル データに影響します。  
  
-   Windows API の操作は、本質的には非トランザクションであり、ユーザー トランザクションに関連しません。 ただし、通常のテーブルの FILESTREAM 列の場合のように、FileTable に格納されている FILESTREAM データへのトランザクション アクセスは、完全にサポートされます。  
  
-   FileTable に対して、通常の [!INCLUDE[tsql](../../includes/tsql-md.md)] アクセスによってクエリおよび更新を実行することもできます。 また、FileTable は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理ツールや、バックアップなどの機能と統合されています。  

-   dbmail を介して電子メールの要求を送信し、filestream ディレクトリ内のファイルを添付することができません (そのため filetable 内のファイルも添付できません)。 ファイル システム フィルター ドライバーの RsFx0420 は、ファイルストリーム フォルダーに出入りする着信 I/O 要求を検査します。 SQLServer 実行可能ファイルと Filestream コードのいずれの要求でもない場合、その要求は明示的に許可されません。
  
##  <a name="additional"></a> FileTable の使用に関するその他の考慮事項  
  
###  <a name="DBA"></a> 管理上の注意点  
 **FILESTREAM と FileTable について**  
  
-   FileTable は FILESTREAM とは別に構成します。 したがって、非トランザクション アクセスの有効化や FileTable の作成を行うことなく、FILESTREAM 機能を使用し続けることができます。  
  
-   FileTable を介した場合を除き、FILESTREAM データへの非トランザクション アクセスは存在しません。 そのため、非トランザクション アクセスを有効にしても、既存の FILESTREAM 列およびアプリケーションの動作は影響を受けません。  
  
 **FileTable と非トランザクション アクセスについて**  
  
-   非トランザクション アクセスは、データベース レベルで有効または無効にできます。  
  
-   非トランザクション アクセスをオフにしたり、読み取り専用または完全な読み取り/書き込みアクセスを有効にしたりすることによって、データベース レベルで非トランザクション アクセスを構成または調整することができます。  
   
###  <a name="memory"></a> FileTable ではメモリ マップ ファイルはサポートされていません  
 FileTable ではメモリ マップ ファイルはサポートされていません。 メモ帳とペイントの 2 つは、メモリ マップ ファイルを使用するアプリケーションの一般的な例です。 これらのアプリケーションを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と同じコンピューターで使用して、FileTable に保存されているファイルを開くことはできません。 ただし、これらのアプリケーションをリモート コンピューターで使用すると、メモリ マッピング機能が使用されないため、FileTable に保存されているファイルを開くことができます。  
   
##  <a name="reltasks"></a> 関連タスク  
 [FileTable の前提条件の有効化](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)  
 FileTable を作成および使用するための前提条件を有効にする方法について説明します。  
  
 [FileTable の作成、変更、および削除](../../relational-databases/blob/create-alter-and-drop-filetables.md)  
 新しい FileTable の作成や、既存の FileTable の変更または削除を行う方法について説明します。  
  
 [FileTable へのファイルの読み込み](../../relational-databases/blob/load-files-into-filetables.md)  
 FileTable にファイルを読み込むまたは移行する方法について説明します。  
  
 [FileTable 内のディレクトリとパスの操作](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
 FileTable 内でファイルが格納されるディレクトリ構造について説明します。  
  
 [Transact SQL を使用した FileTable へのアクセス](../../relational-databases/blob/access-filetables-with-transact-sql.md)  
 Transact SQL データ操作言語 (DML) コマンドでどのように FileTable が操作されるかについて説明します。  
  
 [ファイル I/O API を使用した FileTable へのアクセス](../../relational-databases/blob/access-filetables-with-file-input-output-apis.md)  
 FileTable でファイル システム I/O が動作するしくみについて説明します。  
  
 [FileTable の管理](../../relational-databases/blob/manage-filetables.md)  
 FileTable を管理するための一般的な管理タスクについて説明します。  
  
##  <a name="relcontent"></a> 関連コンテンツ  
 [FileTable スキーマ](../../relational-databases/blob/filetable-schema.md)  
 FileTable の定義済みスキーマおよび固定スキーマについて説明します。  
  
 [FileTable と他の SQL Server 機能の互換性](../../relational-databases/blob/filetable-compatibility-with-other-sql-server-features.md)  
 FileTable と他の SQL Server 機能との連携について説明します。  
  
 [FileTable DDL、関数、ストアド プロシージャ、およびビュー](../../relational-databases/blob/filetable-ddl-functions-stored-procedures-and-views.md)  
 FileTable 機能をサポートするために追加または変更された [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントおよび [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース オブジェクトの一覧を示します。  

## <a name="see-also"></a>参照
[Filestream および FileTable の動的管理ビュー (Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[Filestream および FileTable のカタログ ビュー (Transact-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
<br>[Filestream および FileTable システム ストアド プロシージャ (Transact-SQL)](../system-stored-procedures/filestream-and-filetable-system-stored-procedures.md)


  
  
