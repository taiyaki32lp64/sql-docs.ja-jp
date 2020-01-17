---
title: srv_paramname (拡張ストアド プロシージャ API) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_paramname
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_paramname
ms.assetid: 1a53d707-7b06-49cc-a0df-ac727cfe953f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8a5eca5aef966d205ef550b05eff2d7055e4cb28
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127173"
---
# <a name="srvparamname-extended-stored-procedure-api"></a>srv_paramname (拡張ストアド プロシージャ API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]代わりに CLR Integration をご使用ください。  
  
 リモート ストアド プロシージャ呼び出しのパラメーターの名前を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
DBCHAR * srv_paramname (  
SRV_PROC * srvproc,intn, int *len );  
```  
  
## <a name="arguments"></a>引数  
 *srvproc*  
 特定のクライアント接続のためのハンドル (この場合は、リモート ストアド プロシージャ呼び出しを受け取るハンドル) である SRV_PROC 構造体を指すポインターです。 この構造体には、アプリケーションとクライアントの間の通信やデータを管理するために、拡張ストアド プロシージャ API ライブラリで使用する情報が格納されます。  
  
 *n*  
 パラメーターの番号を示します。 最初のパラメーターは 1 です。  
  
 *len*  
 パラメーター名の長さ (バイト数) を格納した `int` 変数へのポインターです。 *len* が NULL である場合、リモート ストアド プロシージャのパラメーター名の長さは返されていません。  
  
## <a name="returns"></a>戻り値  
 パラメーター名を格納した NULL 終端文字列を指すポインターを返します。 パラメーター名の長さは、*len* に格納されます。 *n* 番目のパラメーターがない場合、またはリモート ストアド プロシージャがない場合は NULL を返し、*len* が -1 に設定され、情報エラー メッセージが送信されます。 パラメーター名が NULL である場合、*len* は 0 に設定され、NULL 終端の空文字列が返されます。  
  
## <a name="remarks"></a>コメント  
 この関数は、リモート ストアド プロシージャ呼び出しのパラメーターの名前を取得します。 パラメーターを指定してリモート ストアド プロシージャを呼び出す場合、パラメーターは名前で指定することも、名前を使用せずにその位置を指定して渡すこともできます。 名前によるパラメーター指定と位置によるパラメーター指定を混合してリモート ストアド プロシージャを呼び出すと、エラーが発生します。 エラーが発生しても SRV_RPC ハンドラーは呼び出されますが、パラメーターが存在しないと見なされ、**srv_rpcparams** は 0 を返します。  
  
> [!IMPORTANT]  
>  拡張ストアド プロシージャのソース コードを十分に確認し、コンパイル済み DLL を、運用サーバーにインストールする前にテストする必要があります。 セキュリティの確認およびテストについて詳しくは、[Microsoft の Web サイト](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409 https://msdn.microsoft.com/security/)をご覧ください。  
  
## <a name="see-also"></a>参照  
 [srv_rpcparams &#40;拡張ストアド プロシージャ API&#41;](srv-rpcparams-extended-stored-procedure-api.md)  
  
  
