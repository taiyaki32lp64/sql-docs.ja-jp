---
title: bcp_sendrow | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_sendrow
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_sendrow function
ms.assetid: ddbdb4bd-ad4e-4bf1-9a75-656aa26ce10a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3e8ef7aa7a4354f5a3fbc334504512b2ee8d131b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62688829"
---
# <a name="bcpsendrow"></a>bcp_sendrow
  プログラム変数から [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にデータ行を送信します。  
  
## <a name="syntax"></a>構文  
  
```  
  
RETCODE bcp_sendrow (  
    HDBC   
hdbc  
);  
  
```  
  
## <a name="arguments"></a>引数  
 *hdbc*  
 一括コピーが有効な ODBC 接続ハンドルです。  
  
## <a name="returns"></a>戻り値  
 SUCCEED または FAIL。  
  
## <a name="remarks"></a>コメント  
 **Bcp_sendrow**関数は、プログラム変数からの行をビルドしに送信します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
 呼び出しの前に**bcp_sendrow**への呼び出しを行う必要があります[bcp_bind](bcp-bind.md)行のデータを格納しているプログラム変数を指定します。  
  
 場合**bcp_bind**長い可変長データ型を指定すると呼ばれますが、 *eDataType* SQLTEXT と null 以外のパラメーター *pData*パラメーター、 **bcp_sendrow**は他のデータ型の場合と同様に、データ値を送信します。 場合、ただし、 **bcp_bind** null になります*pData*パラメーター、 **bcp_sendrow**に指定したデータを持つすべての列を送信した後すぐに、アプリケーションにコントロールを返します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. アプリケーションを呼び出して[bcp_moretext](bcp-moretext.md) 、長い可変長データを送信するには、繰り返し[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、一度にチャンクです。 詳細については、次を参照してください。 [bcp_moretext](bcp-moretext.md)します。  
  
 ときに**bcp_sendrow**一括にプログラム変数から行をコピーするために使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]テーブル、行はコミットされた場合にのみユーザーを呼び出して[bcp_batch](bcp-batch.md)または[bcp_done](bcp-done.md). 呼び出して、ユーザーが選択できます**bcp_batch**したらすべて*n*行または着信データの期間の間で転送がある場合。 場合**bcp_batch**は呼び出されず、行がコミットされたときに**bcp_done**が呼び出されます。  
  
 以降では一括コピーでの変更については、互換性に影響する[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]を参照してください[一括コピー操作を実行する&#40;ODBC&#41;](../native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)します。  
  
## <a name="see-also"></a>参照  
 [一括コピー関数](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
