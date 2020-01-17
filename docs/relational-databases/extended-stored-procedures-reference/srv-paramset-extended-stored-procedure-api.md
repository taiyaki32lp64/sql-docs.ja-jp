---
title: srv_paramset (拡張ストアド プロシージャ API) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_paramset
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_paramset
ms.assetid: 2a509206-a1b8-4b20-b0a2-ef680cef7bd8
author: rothja
ms.author: jroth
ms.openlocfilehash: c3ec0de44aacbcfb2d4e6b96d7525da900017e01
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75253550"
---
# <a name="srv_paramset-extended-stored-procedure-api"></a>srv_paramset (拡張ストアド プロシージャ API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  
  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]代わりに CLR Integration をご使用ください。  
  
 リモート ストアド プロシージャ呼び出しの戻りパラメーターの値を設定します。 この関数に代わって **srv_paramsetoutput** 関数が使用されるようになりました。  
  
## <a name="syntax"></a>構文  
  
```  
  
int srv_paramset (  
SRV_PROC *  
srvproc  
,  
int  
n  
,   
void *  
data  
,  
int  
len   
);  
```  
  
## <a name="arguments"></a>引数  
 *srvproc*  
 特定のクライアント接続のためのハンドル (この場合は、リモート ストアド プロシージャ呼び出しを受け取るハンドル) である SRV_PROC 構造体を指すポインターです。 この構造体には、アプリケーションとクライアントの間の通信やデータを管理するために、拡張ストアド プロシージャ API ライブラリで使用する情報が格納されます。  
  
 *非該当*  
 設定するパラメーターの番号を示します。 最初のパラメーターは 1 です。  
  
 *データ*  
 リモート ストアド プロシージャの戻りパラメーターとしてクライアントに返されるデータ値を指すポインターです。  
  
 *len*  
 返されるデータの実際の長さを指定します。 パラメーターのデータ型が固定長であり、NULL 値を許容しない型 (*srvbit* や *srvint1* など) である場合、*len* は無視されます。  
  
## <a name="returns"></a>戻り値  
 パラメーター値が正しく設定された場合は SUCCEED を返し、それ以外の場合は FAIL を返します。 FAIL を返すのは、現在のリモート ストアド プロシージャがない場合、*n* 番目のリモート ストアド プロシージャ パラメーターがない場合、パラメーターが戻りパラメーターでない場合、*len* 引数が無効である場合です。  
  
 
  *len* が 0 である場合は、NULL を返します。 
  *len* を 0 に設定する以外に、クライアントに NULL を返す方法はありません。  
  
 パラメーターがデータ型の[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 1 つである場合、この関数は次の値を返します。  
  
|新しいデータ型|戻り値のデータ長|  
|--------------------|------------------------|  
|**BITN**|**NULL:** _len_ = 0、DATA = IG、RET = 0<br /><br /> **0:** 該当なし<br /><br /> **>= 255:** 該当なし<br /><br /> **<255:** 該当なし|  
|**BIGVARCHAR**|**NULL:** _len_ = 0、DATA = IG、RET = 1<br /><br /> **0:** _len_ = IG、DATA = ig、RET = 0<br /><br /> **>= 255:** _len_ = valid、DATA = valid、RET = 0<br /><br /> **<255:** _len_ = <8k、DATA = valid、RET = 1|  
|**BIGCHAR**|**NULL:** _len_ = 0、DATA = IG、RET = 1<br /><br /> **0:** _len_ = IG、DATA = ig、RET = 0<br /><br /> **>= 255:** _len_ = valid、DATA = valid、RET = 0<br /><br /> **<255:** _len_ = <8k、DATA = valid、RET = 1|  
|**BIGBINARY**|**NULL:** _len_ = 0、DATA = IG、RET = 1<br /><br /> **0:** _len_ = IG、DATA = ig、RET = 0<br /><br /> **>= 255:** _len_ = valid、DATA = valid、RET = 0<br /><br /> **<255:** _len_ = <8k、DATA = valid、RET = 1|  
|**BIGVARBINARY**|**NULL:** _len_ = 0、DATA = IG、RET = 1<br /><br /> **0:** _len_ = IG、DATA = ig、RET = 0<br /><br /> **>= 255:** _len_ = valid、DATA = valid、RET = 0<br /><br /> **<255:** _len_ = <8k、DATA = valid、RET = 1|  
|NCHAR|**NULL:** _len_ = 0、DATA = IG、RET = 1<br /><br /> **0:** _len_ = IG、DATA = ig、RET = 0<br /><br /> **>= 255:** _len_ = valid、DATA = valid、RET = 0<br /><br /> **<255:** _len_ = <8k、DATA = valid、RET = 1|  
|NVARCHAR|**NULL:** _len_ = 0、DATA = IG、RET = 1<br /><br /> **0:** _len_ = IG、DATA = ig、RET = 0<br /><br /> **>= 255:** _len_ = valid、DATA = valid、RET = 0<br /><br /> **<255:** _len_ = <8k、DATA = valid、RET = 1|  
|**NTEXT**|**NULL:** _len_ = IG、DATA = ig、RET = 0<br /><br /> **0:** _len_ = IG、DATA = ig、RET = 0<br /><br /> **>= 255:** _len_ = IG、DATA = ig、RET = 0<br /><br /> 255: _len_ = ig、data = ig、RET = 0 ** \<**|  
|RET は srv_paramset の戻り値です。||  
|IG は値が無視されることを示します。||  
|valid はデータを指す任意の有効なポインターを示します。||  
  
## <a name="remarks"></a>コメント  
 パラメーターには、リモート ストアド プロシージャを使用してクライアントとアプリケーションとの間で受け渡しされるデータが格納されます。 クライアントは戻りパラメーターとして特定のパラメーターを指定できます。 この戻りパラメーターには、Open Data Services サーバー アプリケーションがクライアントに返す値を格納することができます。 戻りパラメーターの使用は、パラメーターの参照渡しに類似しています。  
  
 戻りパラメーターとして呼び出されていないパラメーターには、戻り値を設定できません。 パラメーターがどのように呼び出されたかを判別するには **srv_paramstatus** を使用します。  
  
 この関数は、パラメーターの戻り値を設定するものであり、戻り値を実際にクライアントに返す役割はありません。 
  **srv_paramset** に設定されているかどうかにかかわらず、すべての戻りパラメーターは、ステータス フラグ SRV_DONE_FINAL が設定された状態で **srv_senddone** が呼び出されると、自動的にクライアントに送信されます。  
  
 パラメーターを指定してリモート ストアド プロシージャを呼び出す場合、パラメーターは名前で指定することも、名前を使用せずにその位置を指定して渡すこともできます。 名前によるパラメーター指定と位置によるパラメーター指定を混合してリモート ストアド プロシージャを呼び出すと、エラーが発生します。 エラーが発生しても SRV_RPC ハンドラーは呼び出されますが、パラメーターが存在しないと見なされ、**srv_rpcparams** は 0 を返します。  
  
> [!IMPORTANT]  
>  拡張ストアド プロシージャのソース コードを十分に確認し、コンパイル済み DLL を、運用サーバーにインストールする前にテストする必要があります。 セキュリティの確認およびテストについて詳しくは、[Microsoft の Web サイト](https://www.microsoft.com/msrc?rtc=1)をご覧ください。  
  
## <a name="see-also"></a>参照  
 [srv_paramsetoutput &#40;拡張ストアドプロシージャ API&#41;](../../relational-databases/extended-stored-procedures-reference/srv-paramsetoutput-extended-stored-procedure-api.md)  
  
  
