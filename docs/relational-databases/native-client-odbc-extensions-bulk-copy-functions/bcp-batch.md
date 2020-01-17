---
title: bcp_batch |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_batch
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_batch function
ms.assetid: 0bda489e-86bc-4a7e-80f6-96047e03f281
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f435b0ba0d7474867af20aea1d59bd6118035623
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73783234"
---
# <a name="bcp_batch"></a>bcp_batch
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  プログラム変数から一括コピーされ、 [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)によって [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に送信されたすべての行をコミットします。  
  
## <a name="syntax"></a>構文  
  
```  
  
DBINT bcp_batch (HDBC  
        hdbc);  
```  
  
## <a name="arguments"></a>引数  
 *hdbc*  
 一括コピーが有効な ODBC 接続ハンドルです。  
  
## <a name="returns"></a>戻り値  
 **Bcp_batch**を最後に呼び出した後に保存された行の数。エラーが発生した場合は-1。  
  
## <a name="remarks"></a>解説  
 一括コピーのバッチではトランザクションを定義します。 アプリケーションで[bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)を使用し、プログラム変数から SQL Server テーブルに行を一括コピーする**bcp_sendrow** 、プログラムが**bcp_batch**または[bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md)を呼び出した場合にのみ、行がコミットされます。  
  
 **Bcp_batch**は、 *n*行ごとに、または (テレメトリアプリケーションと同様に) 受信データになどがあるときに1回呼び出すことができます。 アプリケーションがを呼び出さない場合**bcp_batch** **bcp_done**が呼び出されたときにのみ、一括コピーされた行がコミットされます。  
  
## <a name="see-also"></a>参照  
 [一括コピー関数](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
