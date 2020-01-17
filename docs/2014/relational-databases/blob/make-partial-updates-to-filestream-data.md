---
title: FILESTREAM データの部分的な更新 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT
- FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT
ms.assetid: d6f7661e-6c14-4d31-9541-4520ca0f82b2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 96d9cb3d5c5317ecc9dd069f2e99b20c30327a3d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66009885"
---
# <a name="make-partial-updates-to-filestream-data"></a>FILESTREAM データの部分的な更新
  アプリケーションでは、FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT を使用して FILESTREAM BLOB データを部分的に更新します。 [DeviceIoControl](https://go.microsoft.com/fwlink/?LinkId=105527) 関数は、この値と、 [OpenSqlFilestream](access-filestream-data-with-opensqlfilestream.md) から FILESTREAM ドライバーに返されるハンドルを渡します。 このドライバーによって、サーバー側の現在の FILESTREAM データが、ハンドルが参照するファイルにコピーされます。 ハンドルへの書き込みが行われた後にアプリケーションが FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT 値を発行すると、最後の書き込み操作は維持され、それより前のハンドルへの書き込み操作は失われます。  
  
> [!NOTE]  
>  FILESTREAM のリモート アクセスは、 [SMB プロトコル](https://go.microsoft.com/fwlink/?LinkId=112454) に依存しています。  
  
## <a name="example"></a>例  
 次の例では、 `FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT` 値を使用して、挿入された FILESTREAM BLOB を部分的に更新する方法を示します。  
  
> [!NOTE]  
>  この例では、「 [FILESTREAM が有効なデータベースを作成する方法](create-a-filestream-enabled-database.md) 」および「 [FILESTREAM データを格納するテーブルを作成する方法](create-a-table-for-storing-filestream-data.md)」で作成した、FILESTREAM が有効なデータベースとテーブルが必要です。  
  
 [!code-cpp[FILESTREAM#FS_CPP_FSCTL](../../snippets/tsql/SQL15/tsql/filestream/cpp/filestream.cpp#fs_cpp_fsctl)]  
  
## <a name="see-also"></a>関連項目  
 [OpenSqlFilestream による FILESTREAM データへのアクセス](access-filestream-data-with-opensqlfilestream.md)   
 [FILESTREAM データ用のクライアント アプリケーションの作成](create-client-applications-for-filestream-data.md)  
  
  
