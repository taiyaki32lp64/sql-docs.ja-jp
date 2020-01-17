---
title: bcp_columns |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_columns
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_columns function
ms.assetid: 5376f6fe-9508-439a-8c66-778d77f19ac3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fcfbbdb1881662401e791ea197115120444cf855
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63225525"
---
# <a name="bcpcolumns"></a>bcp_columns
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] との一括コピー入出力に使用する、ユーザー ファイル内の合計列数を設定します。 [bcp_setbulkmode](bcp-setbulkmode.md) bcp_columns 代わりに使用でき、 [bcp_colfmt](bcp-colfmt.md)します。  
  
## <a name="syntax"></a>構文  
  
```  
  
RETCODE bcp_columns (  
HDBC   
hdbc  
,  
INT   
nColumns  
);  
  
```  
  
## <a name="arguments"></a>引数  
 *hdbc*  
 一括コピーが有効な ODBC 接続ハンドルです。  
  
 *nColumns*  
 ユーザー ファイル内の合計列数です。 一括をユーザー ファイルからデータをコピーする準備を行う場合でも、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]テーブルで、ユーザー ファイル内のすべての列をコピーする予定がないと、設定する必要があります*nColumns*ユーザー ファイルの列の合計数にします。  
  
## <a name="returns"></a>戻り値  
 SUCCEED または FAIL。  
  
## <a name="remarks"></a>コメント  
 この関数は、後でのみ呼び出すことができます[bcp_init](bcp-init.md)は有効なファイル名で呼び出されました。  
  
 この関数を呼び出す必要があるのは、既定とは異なる形式のユーザー ファイルを使用する場合のみです。 既定のユーザー ファイル形式の説明の詳細については、次を参照してください。 **bcp_init**します。  
  
 呼び出した後`bcp_columns`、呼び出す必要があります[bcp_colfmt](bcp-colfmt.md)カスタム ファイル形式を完全に定義するユーザー ファイル内の各列にします。  
  
## <a name="see-also"></a>参照  
 [一括コピー関数](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
