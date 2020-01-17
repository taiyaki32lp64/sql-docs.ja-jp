---
title: bcp_sendrow |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_sendrow
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_sendrow function
ms.assetid: ddbdb4bd-ad4e-4bf1-9a75-656aa26ce10a
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4bb5375de9769046c12f56f91d5c26e41090564b
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73782497"
---
# <a name="bcp_sendrow"></a>bcp_sendrow
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  プログラム変数から [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にデータ行を送信します。  
  
## <a name="syntax"></a>構文  
  
```  
  
RETCODE bcp_sendrow (  
    HDBC hdbc);  
```  
  
## <a name="arguments"></a>引数  
 *hdbc*  
 一括コピーが有効な ODBC 接続ハンドルです。  
  
## <a name="returns"></a>戻り値  
 SUCCEED または FAIL。  
  
## <a name="remarks"></a>解説  
 **Bcp_sendrow**関数は、プログラム変数から行を作成し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に送信します。  
  
 **Bcp_sendrow**を呼び出す前に、行データを含むプログラム変数を指定するために[bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)の呼び出しを行う必要があります。  
  
 SQLTEXT の*Edatatype*パラメーターや NULL 以外の*pData*パラメーターなど、長い可変長のデータ型を指定して**bcp_bind**を呼び出すと、他のデータの場合と同様に、 **bcp_sendrow**データ値全体が送信されます。各種. ただし、 **bcp_bind**に*PDATA*パラメーターが NULL の場合、指定されたデータを含むすべての列が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に送信された直後に、 **bcp_sendrow**によってコントロールがアプリケーションに返されます。 その後、アプリケーションは[bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)を繰り返し呼び出して、長い可変長データを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に、一度に1つのチャンクに送信できます。 詳細については、「 [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md)」を参照してください。  
  
 プログラム変数から [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルに行を一括コピーするために**bcp_sendrow**を使用すると、ユーザーが[bcp_batch](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md)または[bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md)を呼び出した場合にのみ、行がコミットされます。 ユーザーは、 *n*行ごとに**bcp_batch**を呼び出すことも、受信データの期間間になどがあるときに呼び出すこともできます。 **Bcp_batch**が呼び出されない場合、 **bcp_done**が呼び出されたときに行がコミットされます。  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]による一括コピーの重大な変更については、「[一括コピー操作&#40;の実行&#41;ODBC](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [一括コピー関数](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
