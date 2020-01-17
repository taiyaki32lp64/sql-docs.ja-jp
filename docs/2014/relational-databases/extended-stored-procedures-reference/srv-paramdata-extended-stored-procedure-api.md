---
title: srv_paramdata (拡張ストアド プロシージャ API) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_paramdata
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_paramdata
ms.assetid: 3104514d-b404-47c9-b6d7-928106384874
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 0825b86cabf57df552063335a0870461cb8a5658
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127410"
---
# <a name="srvparamdata-extended-stored-procedure-api"></a>srv_paramdata (拡張ストアド プロシージャ API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]代わりに CLR Integration をご使用ください。  
  
 リモート ストアド プロシージャ呼び出しのパラメーターの値を返します。 この関数に代わって **srv_paraminfo** 関数が使用されるようになりました。  
  
## <a name="syntax"></a>構文  
  
```  
  
void * srv_paramdata (  
SRV_PROC *  
srvproc  
,  
int  
n   
);  
  
```  
  
## <a name="arguments"></a>引数  
 *srvproc*  
 特定のクライアント接続のためのハンドル (この場合は、リモート ストアド プロシージャ呼び出しを受け取るハンドル) である SRV_PROC 構造体を指すポインターです。 この構造体には、アプリケーションとクライアントの間の通信やデータを管理するために、拡張ストアド プロシージャ ライブラリで使用する情報が格納されます。  
  
 *n*  
 パラメーターの番号です。 最初のパラメーターは 1 です。  
  
## <a name="returns"></a>戻り値  
 パラメーター値を指すポインターを返します。 *n* 番目のパラメーターが NULL である場合、*n* 番目のパラメーターがない場合、またはリモート ストアド プロシージャがない場合には、NULL を返します。 パラメーター値が文字列である場合、NULL 終端ではないこともあります。 文字列の長さを判断するには、**srv_paramlen** を使用します。  
  
 パラメーターが [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型のいずれかである場合、この関数は次の値を返します。 ポインター データには、データ型に対する有効なポインター (VP) か、NULL か、該当なし (N/A) かを示す情報と、ポインターが指すデータの内容が含まれます。  
  
|新しいデータ型|入力データ長|  
|--------------------|-----------------------|  
|BITN|**NULL:** VP、NULL<br /><br /> **ZERO:** VP、NULL<br /><br /> **>=255:** なし<br /><br /> **<255:** なし|  
|BIGVARCHAR|**NULL:** NULL、該当なし<br /><br /> **ZERO:** VP、NULL<br /><br /> **>=255:** VP、255 文字<br /><br /> **<255:** VP、実際のデータ|  
|BIGCHAR|**NULL:** NULL、該当なし<br /><br /> **ZERO:** VP、255 個のスペース<br /><br /> **>=255:** VP、255 文字<br /><br /> **<255:** VP、実際のデータ + パディング (最大 255)|  
|BIGBINARY|**NULL:** NULL、該当なし<br /><br /> **ZERO:** VP、255 0x00<br /><br /> **>=255:** VP、255 バイト<br /><br /> **<255:** VP、実際のデータ + パディング (最大 255)|  
|BIGVARBINARY|**NULL:** NULL、該当なし<br /><br /> **ZERO:** VP、0x00<br /><br /> **>=255:** VP、255 バイト<br /><br /> **<255:** VP、実際のデータ|  
|NCHAR|**NULL:** NULL、該当なし<br /><br /> **ZERO:** VP、255 個のスペース<br /><br /> **>=255:** VP、255 文字<br /><br /> **<255:** VP、実際のデータ + パディング (最大 255)|  
|NVARCHAR|**NULL:** NULL、該当なし<br /><br /> **ZERO:** VP、NULL<br /><br /> **>=255:** VP、255 文字<br /><br /> **<255:** VP、実際のデータ|  
|NTEXT|**NULL:** なし<br /><br /> **ZERO:** なし<br /><br /> **>=255:** なし<br /><br /> **\<255:** なし|  
  
 \*   データが NULL 終端ではないため、255 文字を超えるデータが切り捨てられても警告は発生しません。  
  
## <a name="remarks"></a>コメント  
 パラメーター名がわかっている場合は、**srv_paramnumber** でパラメーター番号を取得できます。 パラメーターが NULL かどうかを判断する場合は、**srv_paramlen** を使用します。  
  
 パラメーターを指定してリモート ストアド プロシージャを呼び出す場合、パラメーターは名前で指定することも、名前を使用せずにその位置を指定して渡すこともできます。 名前によるパラメーター指定と位置によるパラメーター指定を混合してリモート ストアド プロシージャを呼び出すと、エラーが発生します。 エラーが発生しても SRV_RPC ハンドラーは呼び出されますが、パラメーターが存在しないと見なされ、**srv_rpcparams** は 0 を返します。  
  
> [!IMPORTANT]  
>  拡張ストアド プロシージャのソース コードを十分に確認し、コンパイル済み DLL を、運用サーバーにインストールする前にテストする必要があります。 セキュリティの確認およびテストについて詳しくは、[Microsoft の Web サイト](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)をご覧ください。  
  
## <a name="see-also"></a>参照  
 [srv_rpcparams &#40;拡張ストアド プロシージャ API&#41;](srv-rpcparams-extended-stored-procedure-api.md)  
  
  
