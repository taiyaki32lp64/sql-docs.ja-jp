---
title: FILESTREAM データ用のクライアント アプリケーションの作成 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], Win32
ms.assetid: 8a02aff6-e54c-40c6-a066-2083e9b090aa
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 385deb9dd689c6716ab8addaa64d8bf8bd62ed97
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085394"
---
# <a name="create-client-applications-for-filestream-data"></a>FILESTREAM データ用のクライアント アプリケーションの作成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Win32 API を使って、FILESTREAM BLOB のデータの読み書きができます。 次の手順を実行する必要があります。  
  
-   FILESTREAM ファイルのパスを読み取ります。  
  
-   現在のトランザクション コンテキストを読み取ります。  
  
-   Win32 ハンドルを取得し、そのハンドルを使用して FILESTREAM BLOB に対してデータの読み書きを行います。  
  
> [!NOTE]  
>  このトピックの例を実行するには、「 [FILESTREAM が有効なデータベースを作成する方法](../../relational-databases/blob/create-a-filestream-enabled-database.md) 」および「 [FILESTREAM データを格納するテーブルを作成する方法](../../relational-databases/blob/create-a-table-for-storing-filestream-data.md)」に基づいて、FILESTREAM が有効なデータベースとテーブルを作成する必要があります。  
  
##  <a name="func"></a> FILESTREAM データを操作するための関数  
 FILESTREAM を使用してバイナリ ラージ オブジェクト (BLOB) データを格納すると、Win32 API を使用してそのファイルを操作できます。 Win32 アプリケーションで FILESTREAM BLOB データを操作できるようにするために、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には次の関数と API が用意されています。  
  
-   [PathName](../../relational-databases/system-functions/pathname-transact-sql.md) 。BLOB へのパスをトークンとして返します。 アプリケーションでは、このトークンを使用して Win32 ハンドルを取得し、BLOB データを操作します。  
  
     FILESTREAM データを含むデータベースが Always On 可用性グループに属する場合、PathName 関数はコンピューター名ではなく仮想ネットワーク名 (VNN) を返します。  
  
-   [GET_FILESTREAM_TRANSACTION_CONTEXT()](../../t-sql/functions/get-filestream-transaction-context-transact-sql.md) は、セッションの現在のトランザクションを表すトークンを返します。 アプリケーションでは、このトークンを使用して、FILESTREAM のファイル システム ストリーミング操作をトランザクションにバインドします。  
  
-   [OpenSqlFilestream API](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) 。Win32 ファイル ハンドルを取得します。 アプリケーションでは、このハンドルを使って FILESTREAM データをストリーミングして、次の Win32 API にハンドルを渡すことができます。[ReadFile](https://go.microsoft.com/fwlink/?LinkId=86422)、[WriteFile](https://go.microsoft.com/fwlink/?LinkId=86423)、[TransmitFile](https://go.microsoft.com/fwlink/?LinkId=86424)、[SetFilePointer](https://go.microsoft.com/fwlink/?LinkId=86425)、[SetEndOfFile](https://go.microsoft.com/fwlink/?LinkId=86426)、[FlushFileBuffers](https://go.microsoft.com/fwlink/?LinkId=86427)。 このハンドルを使用してその他の API を呼び出すと、ERROR_ACCESS_DENIED エラーが返されます。 ハンドルは、 [CloseHandle](https://go.microsoft.com/fwlink/?LinkId=86428)を使用して閉じる必要があります。  
  
 すべての FILESTREAM データ コンテナー アクセスは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] トランザクションで実行されます。 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行すると、SQL データと FILESTREAM データの一貫性を維持できます。  
  
##  <a name="steps"></a> FILESTREAM データにアクセスするための手順  
  
###  <a name="path"></a> FILESTREAM ファイルのパスの読み取り  
 FILESTREAM テーブルの各セルには、ファイル パスが関連付けられています。 パスを読み取るには、 **ステートメントで** varbinary(max) **列の** PathName [!INCLUDE[tsql](../../includes/tsql-md.md)] プロパティを使用します。 **varbinary(max)** 列のファイル パスを読み取る方法を次の例に示します。  
  
 [!code-sql[FILESTREAM#FS_PathName](../../relational-databases/blob/codesnippet/tsql/create-client-applicatio_1.sql)]  
  
###  <a name="trx"></a> トランザクション コンテキストの読み取り  
 現在のトランザクション コンテキストを取得するには、 [!INCLUDE[tsql](../../includes/tsql-md.md)] [GET_FILESTREAM_TRANSACTION_CONTEXT()](../../t-sql/functions/get-filestream-transaction-context-transact-sql.md) 関数を使用します。 トランザクションを開始して現在のトランザクション コンテキストを読み取る方法を次の例に示します。  
  
 [!code-sql[FILESTREAM#FS_GET_TRANSACTION_CONTEXT](../../relational-databases/blob/codesnippet/tsql/create-client-applicatio_2.sql)]  
  
###  <a name="handle"></a> Win32 ファイル ハンドルの取得  
 Win32 ファイル ハンドルを取得するには、OpenSqlFilestream API を呼び出します。 この API は、sqlncli.dll ファイルからエクスポートされます。 返されるハンドルは、次のいずれかの Win32 API に渡すことができます。[ReadFile](https://go.microsoft.com/fwlink/?LinkId=86422)、[WriteFile](https://go.microsoft.com/fwlink/?LinkId=86423)、[TransmitFile](https://go.microsoft.com/fwlink/?LinkId=86424)、[SetFilePointer](https://go.microsoft.com/fwlink/?LinkId=86425)、[SetEndOfFile](https://go.microsoft.com/fwlink/?LinkId=86426)、[FlushFileBuffers](https://go.microsoft.com/fwlink/?LinkId=86427)。 Win32 ファイル ハンドルを取得し、これを使用して FILESTREAM BLOB に対してデータを読み書きする方法を次の例に示します。  
  
 [!code-cs[FILESTREAM#FS_CS_ReadAndWriteBLOB](../../relational-databases/blob/codesnippet/csharp/create-client-applicatio_3.cs)]  
  
 [!code-vb[FILESTREAM#FS_VB_ReadAndWriteBLOB](../../relational-databases/blob/codesnippet/visualbasic/create-client-applicatio_4.vb)]  
  
 [!code-cpp[FILESTREAM#FS_CPP_WriteBLOB](../../relational-databases/blob/codesnippet/cpp/create-client-applicatio_5.cpp)]  
  
##  <a name="best"></a> アプリケーションの設計と実装のベスト プラクティス  
  
-   FILESTREAM を使用するアプリケーションの設計と実装を行う場合は、次のガイドラインを考慮してください。  
  
-   初期化されていない FILESTREAM 列を表すには、0x の代わりに NULL を使用します。 0x 値を使用するとファイルが作成されますが、NULL の場合はファイルが作成されません。  
  
-   null でない FILESTREAM 列を含むテーブルでは、挿入操作と削除操作を行わないでください。 挿入操作および削除操作を行うと、ガベージ コレクション用の FILESTREAM テーブルが変更される場合があります。 その結果、アプリケーション パフォーマンスが時間と共に低下する可能性があります。  
  
-   レプリケーションを使用するアプリケーションでは、NEWID() の代わりに NEWSEQUENTIALID() を使用します。 このようなアプリケーションでは、GUID の生成に関して NEWID() よりも NEWSEQUENTIALID() の方が高いパフォーマンスを発揮します。  
  
-   FILESTREAM API は、データへの Win32 ストリーミング アクセス向けに設計されています。 [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用して 2 MB を超える FILESTREAM バイナリ ラージ オブジェクト (BLOB) の読み取り/書き込みを行わないでください。 [!INCLUDE[tsql](../../includes/tsql-md.md)]から BLOB データの読み取り/書き込みを行う必要がある場合は、Win32 から FILESTREAM BLOB を開く前にすべての BLOB データを必ず使用してください。 すべての [!INCLUDE[tsql](../../includes/tsql-md.md)] データが使用されていない場合、後続の FILESTREAM を開く操作または閉じる操作が失敗することがあります。  
  
-   FILESTREAM BLOB の更新や FILESTREAM BLOB の後または前にデータを追加する [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントは使用しないようにします。 そのような操作を行うと、BLOB データが tempdb データベースにスプールされ、新しい物理的ファイルに戻される可能性があります。  
  
-   小さな BLOB 更新を FILESTREAM BLOB に追加しないようにします。 追加操作ごとに、基になる FILESTREAM ファイルがコピーされます。 アプリケーションで小さな BLOB を書き込む必要がある場合は、BLOB を **varbinary(max)** 列に書き込んでおき、BLOB の数があらかじめ設定された制限に達したときに FILESTREAM BLOB に対して 1 回の書き込み操作を行います。  
  
-   アプリケーションで大量の BLOB ファイルのデータ長を取得しないようにします。 サイズは [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]に格納されないため、この操作を実行するには多くの時間が必要になります。 BLOB ファイルの長さを調べる必要がある場合は、 [!INCLUDE[tsql](../../includes/tsql-md.md)] DATALENGTH() 関数を使用して BLOB のサイズを調べます (BLOB が閉じている場合)。 DATALENGTH() でサイズを取得する際には、BLOB ファイルは開かれません。  
  
-   アプリケーションで Message Block1 (SMB1) プロトコルを使用する場合、60 KB 単位で FILESTREAM BLOB データを読み取ると、パフォーマンスが最適化されます。  
  
## <a name="see-also"></a>参照  
 [FILESTREAM アプリケーションでのデータベース操作との競合の回避](../../relational-databases/blob/avoid-conflicts-with-database-operations-in-filestream-applications.md)   
 [OpenSqlFilestream による FILESTREAM データへのアクセス](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)   
 [バイナリ ラージ オブジェクト &#40;Blob&#41; データ &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)   
 [FILESTREAM データの部分的な更新](../../relational-databases/blob/make-partial-updates-to-filestream-data.md)  
  
  
