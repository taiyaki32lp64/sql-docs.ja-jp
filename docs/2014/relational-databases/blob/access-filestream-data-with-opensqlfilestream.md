---
title: OpenSqlFilestream による FILESTREAM データへのアクセス | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
api_name:
- OpenSqlFilestream
api_location:
- sqlncli11.dll
helpviewer_keywords:
- OpenSqlFilestream
ms.assetid: d8205653-93dd-4599-8cdf-f9199074025f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 74dad8dc9795a30637a9ab08c56ce8d0940b6f0e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66010482"
---
# <a name="access-filestream-data-with-opensqlfilestream"></a>OpenSqlFilestream による FILESTREAM データへのアクセス
  OpenSqlFilestream API は、FILESTREAM バイナリ ラージ オブジェクト (BLOB)、ファイル システムに格納されているの Win32 互換ファイル ハンドルを取得します。 このハンドルは、次のいずれかの Win32 API に渡すことができます。[ReadFile](https://go.microsoft.com/fwlink/?LinkId=86422)、[WriteFile](https://go.microsoft.com/fwlink/?LinkId=86423)、[TransmitFile](https://go.microsoft.com/fwlink/?LinkId=86424)、[SetFilePointer](https://go.microsoft.com/fwlink/?LinkId=86425)、[SetEndOfFile](https://go.microsoft.com/fwlink/?LinkId=86426)、[FlushFileBuffers](https://go.microsoft.com/fwlink/?LinkId=86427)。 このハンドルをその他の Win32 API に渡すと、ERROR_ACCESS_DENIED エラーが返されます。 このハンドルは、トランザクションをコミットまたはロールバックする前に Win32 [CloseHandle](https://go.microsoft.com/fwlink/?LinkId=86428) API に渡して閉じる必要があります。 ハンドルを閉じないと、サーバー側でリソースのリークが発生します。  
  
 すべての FILESTREAM データ コンテナー アクセスは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] トランザクションで実行する必要があります。 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを同じトランザクションで実行することもできます。 これにより、SQL データと FILESTREAM BLOB データの一貫性が維持されます。  
  
 Win32 を使用して FILESTREAM BLOB にアクセスするには、 [Windows 認証](../security/choose-an-authentication-mode.md) を有効にする必要があります。  
  
> [!IMPORTANT]  
>  ファイルを書き込みアクセス用に開くと、トランザクションは FILESTREAM エージェントによって所有されます。 トランザクションが解放されるまで、Win32 ファイル I/O だけが許可されます。 トランザクションを解放するには、書き込みハンドルを閉じる必要があります。  
  
## <a name="syntax"></a>構文  
  
```  
  
  HANDLE OpenSqlFilestream (  
  LPCWSTR  
  FilestreamPath  
  ,  
  SQL_FILESTREAM_DESIRED_ACCESS  
  DesiredAccess,  
ULONGOpenOptions,LPBYTEFilestreamTransactionContext,SIZE_TFilestreamTransactionContextLength,PLARGE_INTEGERAllocationSize);  
```  
  
#### <a name="parameters"></a>パラメーター  
 *FilestreamPath*  
 [in]`nvarchar(max)`によって返されるパス、 [PathName](/sql/relational-databases/system-functions/pathname-transact-sql)関数。 PathName は、FILESTREAM のテーブルおよび列に対して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の SELECT または UPDATE の権限を持つアカウントのコンテキストから呼び出す必要があります。  
  
 *DesiredAccess*  
 [in] FILESTREAM BLOB データへのアクセスに使用するモードを設定します。 この値は [DeviceIoControl 関数](https://go.microsoft.com/fwlink/?LinkId=105527)に渡されます。  
  
|名前|値|説明|  
|----------|-----------|-------------|  
|SQL_FILESTREAM_READ|0|ファイルからデータを読み取ることができます。|  
|SQL_FILESTREAM_WRITE|1|ファイルにデータを書き込むことができます。|  
|SQL_FILESTREAM_READWRITE|2|ファイルに対してデータを読み書きできます。|  
  
> [!NOTE]  
>  これらの値は、sqlncli.h の SQL_FILESTREAM_DESIRED_ACCESS 列挙で定義されます。  
  
 *OpenOptions*  
 [in] ファイルの属性とフラグです。 このパラメーターでは、次のフラグを任意に組み合わせて指定することもできます。  
  
|フラグ|値|意味|  
|----------|-----------|-------------|  
|SQL_FILESTREAM_OPEN_NONE|0x00000000:|特にオプションを指定せずにファイルが開かれるか、または作成されます。|  
|SQL_FILESTREAM_OPEN_FLAG_ASYNC|0x00000001L|非同期 I/O 用にファイルが開かれるか、または作成されます。|  
|SQL_FILESTREAM_OPEN_FLAG_NO_BUFFERING|0x00000002L|システム キャッシュを使用せずにファイルが開かれます。|  
|SQL_FILESTREAM_OPEN_FLAG_NO_WRITE_THROUGH|0x00000004L|中間キャッシュを使用せずに 直接ディスクに書き込みます。|  
|SQL_FILESTREAM_OPEN_FLAG_SEQUENTIAL_SCAN|0x00000008L|ファイルが先頭から末尾まで順次アクセスされます。 システムはこれをヒントとしてファイルのキャッシュを最適化します。 アプリケーションがランダム アクセスのファイル ポインターを移動させると、最適なキャッシングが行われなくなる場合があります。|  
|SQL_FILESTREAM_OPEN_FLAG_RANDOM_ACCESS|0x00000010L|ファイルがランダムにアクセスされます。 システムはこれをヒントとしてファイルのキャッシュを最適化します。|  
  
 *FilestreamTransactionContext*  
 [in] [GET_FILESTREAM_TRANSACTION_CONTEXT](/sql/t-sql/functions/get-filestream-transaction-context-transact-sql) 関数から返される値です。  
  
 *FilestreamTransactionContextLength*  
 [in] GET_FILESTREAM_TRANSACTION_CONTEXT 関数から返される `varbinary(max)` データのバイト数です。 この関数は、N バイトの配列を返します。 N は関数によって決まる、返されるバイト配列のプロパティです。  
  
 *AllocationSize*  
 [in] データ ファイルの初期割り当てサイズをバイト単位で指定します。 読み取りモードでは無視されます。 このパラメーターには NULL を指定できます。その場合、ファイル システムの既定の動作が使用されます。  
  
## <a name="return-value"></a>戻り値  
 この関数の実行が成功した場合の戻り値は、指定したファイルへのオープン ハンドルです。 失敗した場合の戻り値は、INVALID_HANDLE_VALUE です。 詳細なエラー情報を取得するには、GetLastError() を呼び出します。  
  
## <a name="examples"></a>使用例  
 `OpenSqlFilestream` API を使用して Win32 ハンドルを取得する方法を次の例に示します。  
  
 [!code-csharp[FILESTREAM#FS_CS_ReadAndWriteBLOB](../../snippets/tsql/SQL15/tsql/filestream/cs/filestream.cs#fs_cs_readandwriteblob)]  
  
 [!code-vb[FILESTREAM#FS_VB_ReadAndWriteBLOB](../../snippets/tsql/SQL15/tsql/filestream/vb/filestream.vb#fs_vb_readandwriteblob)]  
  
 [!code-cpp[FILESTREAM#FS_CPP_WriteBLOB](../../snippets/tsql/SQL15/tsql/filestream/cpp/filestream.cpp#fs_cpp_writeblob)]  
  
## <a name="remarks"></a>コメント  
 この API を使用するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client をインストールする必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クライアント ツールとともにインストールされます。 詳細については、「 [SQL Server Native Client のインストール](../native-client/applications/installing-sql-server-native-client.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [バイナリ ラージ オブジェクト &#40;Blob&#41; データ &#40;SQL Server&#41;](binary-large-object-blob-data-sql-server.md)   
 [FILESTREAM データの部分的な更新](make-partial-updates-to-filestream-data.md)   
 [FILESTREAM アプリケーションでのデータベース操作との競合の回避](avoid-conflicts-with-database-operations-in-filestream-applications.md)  
  
  
