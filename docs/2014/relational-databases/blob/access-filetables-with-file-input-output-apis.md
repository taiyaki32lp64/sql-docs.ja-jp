---
title: ファイル I/O API を使用した FileTable へのアクセス | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], accessing files with file APIs
ms.assetid: fa504c5a-f131-4781-9a90-46e6c2de27bb
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: cd43f430f43f31435df6fff71687136f4bd5f9e7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66010356"
---
# <a name="access-filetables-with-file-input-output-apis"></a>ファイル I/O API を使用した FileTable へのアクセス
  FileTable でファイル システム I/O が動作するしくみについて説明します。  
  
##  <a name="accessing"></a> FileTable でのファイル I/O API の使用  
 FileTable を使用する際、多くの場合は Windows ファイル システムとファイル I/O API が利用されます。 FileTable は、さまざまなファイル I/O API を利用した非トランザクション アクセスをサポートしています。  
  
1.  一般的に、ファイル I/O API は、ファイルまたはディレクトリの論理 UNC パスを取得することによって起動されます。 アプリケーションは、[GetFileNamespacePath &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/getfilenamespacepath-transact-sql) 関数を含む [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用して、ファイルまたはディレクトリの論理パスを取得できます。 詳しくは、「 [Work with Directories and Paths in FileTables](work-with-directories-and-paths-in-filetables.md)」をご覧ください。  
  
2.  次に、この論理パスを使用して、ファイルまたはディレクトリに対するハンドルを取得し、オブジェクトを操作します。 CreateFile()、CreateDirectory() など、サポート対象のファイル システム API 関数にパスを渡して、ファイルを作成したり、開いたり、ハンドルを取得したりできます。 そのハンドルを使用することで、データのストリーミング、ディレクトリの列挙と編成、ファイル属性の取得と設定、ファイルまたはディレクトリの削除などの操作を実行できます。  
  
##  <a name="create"></a> FileTable でのファイルおよびディレクトリの作成  
 ファイル I/O API (CreateFile、CreateDirectory など) を呼び出すことで、FileTable にファイルまたはディレクトリを作成できます。  
  
-   すべての CREATION_DISPOSITION フラグ、共有モード、およびアクセス モードがサポートされています。 これには、ファイルの作成、削除、およびインプレース変更が含まれます。 さらに、ディレクトリの作成と削除、名前の変更、移動の操作など、ファイル名前空間の更新もサポートされています。  
  
-   新しいファイルまたはディレクトリの作成は、基になる FileTable 内での新しい行の作成に対応します。  
  
-   ファイルの場合、ストリーム データが **file_stream** 列に格納されます。ディレクトリの場合、この列は null になります。  
  
-   ファイルの場合、 **is_directory** 列に **false**が格納されます。 ディレクトリの場合、この列に **true**が格納されます。  
  
-   複数のファイル I/O 操作または [!INCLUDE[tsql](../../includes/tsql-md.md)] 操作が同時に行われ、その影響が階層内の同じファイルまたはディレクトリに及ぶ場合、アクセスの共有とコンカレンシーが適用されます。  
  
##  <a name="read"></a> FileTable 内のファイルおよびディレクトリの読み取り  
 ストリームおよび属性データに対するすべてのファイル I/O アクセス操作に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の Read Committed 分離セマンティクスが適用されます。  
  
##  <a name="write"></a> FileTable 内のファイルおよびディレクトリへの書き込みおよび更新  
  
-   FileTable に対するファイル I/O 書き込み操作または更新操作は、すべて非トランザクションです。 つまり、これらの操作にバインドされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] トランザクションは存在せず、ACID 保証はありません。  
  
-   FileTable に対するすべてのファイル I/O ストリーミング/インプレース更新がサポートされます。  
  
-   ファイル I/O API を介して FILESTREAM のデータまたは属性を更新すると、FileTable 内の対応する **file_stream** および対応するファイル属性列が更新されます。  
  
##  <a name="delete"></a> FileTable 内のファイルおよびディレクトリの削除  
 ファイルまたはディレクトリを削除すると、Windows ファイル I/O API のすべてのセマンティクスが適用されます。  
  
-   ディレクトリにファイルまたはサブディレクトリが含まれる場合、そのディレクトリの削除は失敗します。  
  
-   ファイルまたはディレクトリを削除すると、対応する行が FileTable から削除されます。 これは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] 操作を介して行を削除することと同じです。  
  
##  <a name="supported"></a> サポートされているファイル システム操作  
 FileTable は、以下のファイル システム操作に関連するファイル システム API をサポートしています。  
  
-   ディレクトリ管理  
  
-   ファイル管理  
  
 FileTable は、以下の操作をサポートしていません。  
  
-   ディスク管理  
  
-   ボリューム管理  
  
-   トランザクション NTFS  
  
##  <a name="considerations"></a> FileTable へのファイル I/O アクセスに関するその他の注意点  
  
###  <a name="vnn"></a> AlwaysOn 可用性グループでの仮想ネットワーク名 (VNN) の使用  
 FILESTREAM データまたは FileTable データを格納するデータベースが AlwaysOn 可用性グループに属する場合、ファイル システム API を介した FILESTREAM データまたは FileTable データへのすべてのアクセスではコンピューター名ではなく仮想ネットワーク名 (VNN) を使用する必要があります。 詳細については、「[FILESTREAM および FileTable と AlwaysOn 可用性グループ &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/filestream-and-filetable-with-always-on-availability-groups-sql-server.md)」を参照してください。  
  
###  <a name="partial"></a> 部分更新  
 FileTable 内の FILESTREAM データ用に [GetFileNamespacePath &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/getfilenamespacepath-transact-sql) 関数を使用して取得された書き込み可能なハンドルは、FILESTREAM コンテンツのインプレース部分更新を実行するために使用できます。 この操作は、トランザクション FILESTREAM アクセスとは異なります。トランザクション FILESTREAM アクセスでは、 **OpenSQLFILESTREAM()** を呼び出して明示的なトランザクション コンテキストを渡すことによって取得されたハンドルが使用されます。  
  
###  <a name="trans"></a> トランザクション セマンティクス  
 ファイル I/O API を使用して FileTable 内のファイルにアクセスする場合、このような操作はユーザー トランザクションと関連付けされず、次のような特徴を持ちます。  
  
-   FileTable 内の FILESTREAM データの非トランザクション アクセスは、いずれのトランザクションにも関連付けられていないため、特定の分離セマンティクスがありません。 ただし、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では内部トランザクションを使用して、FileTable データに対してロックまたはコンカレンシーのセマンティクスを適用することができます。 このタイプの内部トランザクションは、すべて READ COMMITTED 分離によって実行されます。  
  
-   FILESTREAM データの非トランザクション操作に対する ACID 保証はありません。 一貫性の保証は、ファイル システム内のアプリケーションで行われるファイル更新の場合と類似します。  
  
-   このような変更はロールバックできません。  
  
 ただし、FileTable 内の FILESTREAM 列は、 **OpenSqlFileStream()** の呼び出しによるトランザクション FILESTREAM アクセスによって、アクセスすることもできます。 この種のアクセスは完全にトランザクション アクセスであり、現在サポートされている全レベルのトランザクション一貫性を保持します。  
  
###  <a name="concurrency"></a> コンカレンシー制御  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、ファイル システム アプリケーション間の FileTable アクセス、およびファイル システム アプリケーションと [!INCLUDE[tsql](../../includes/tsql-md.md)] アプリケーション間の FileTable アクセスに対して、コンカレンシー制御が適用されます。 このコンカレンシー制御は、FileTable の行に適切なロックを設定することによって実現されます。  
  
###  <a name="triggers"></a> トリガー  
 ファイル システムを利用して、ファイルまたはディレクトリ、あるいはその属性の作成、変更、または削除を行うと、FileTable 内で対応する挿入操作、更新操作、または削除操作が実行されます。 そのような操作の中で、関連する [!INCLUDE[tsql](../../includes/tsql-md.md)] DML トリガーが起動されます。  
  
##  <a name="funclist"></a> FileTable でサポートされているファイル システム機能  
  
|機能|Supported|コメント|  
|----------------|---------------|--------------|  
|**oplock**|はい|レベル 2、レベル 1、バッチ、およびフィルターの各 oplock がサポートされます。|  
|**拡張属性**|いいえ||  
|**再解析ポイント**|いいえ||  
|**永続的 ACL**|いいえ||  
|**名前付きストリーム**|いいえ||  
|**スパース ファイル**|はい|スパースかどうかはファイルにのみ設定できます。この設定はデータ ストリームの記憶域に影響します。 FILESTREAM データは NTFS ボリュームに格納されるため、FileTable 機能では NTFS ファイル システムに要求を転送することによってスパース ファイルをサポートします。|  
|**圧縮**|はい||  
|**暗号化**|はい||  
|**TxF**|いいえ||  
|**ファイル ID**|いいえ||  
|**オブジェクト ID**|いいえ||  
|**シンボリック リンク**|いいえ||  
|**ハード リンク**|いいえ||  
|**短い名前**|いいえ||  
|**ディレクトリ変更の通知**|いいえ||  
|**バイト範囲ロック**|はい|バイト範囲ロックの要求は、NTFS ファイル システムに渡されます。|  
|**メモリ マップ ファイル**|いいえ||  
|**キャンセル I/O**|はい||  
|**セキュリティ**|いいえ|Windows 共有レベルのセキュリティと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のテーブルおよび列レベルのセキュリティが適用されます。|  
|**USN ジャーナル**|いいえ|FileTable 内のファイルおよびディレクトリに対するメタデータの変更は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースの DML 操作です。 したがって、これらの操作は対応するデータベース ログ ファイルに記録されます。 ただし、(サイズの変更を除き) NTFS USN ジャーナルには記録されません。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の変更の追跡機能を使用して、同様の情報をキャプチャします。|  
  
## <a name="see-also"></a>参照  
 [FileTable へのファイルの読み込み](load-files-into-filetables.md)   
 [Work with Directories and Paths in FileTables](work-with-directories-and-paths-in-filetables.md)   
 [Transact SQL を使用した FileTable へのアクセス](access-filetables-with-transact-sql.md)   
 [FileTable DDL、関数、ストアド プロシージャ、およびビュー](../views/views.md)  
  
  
