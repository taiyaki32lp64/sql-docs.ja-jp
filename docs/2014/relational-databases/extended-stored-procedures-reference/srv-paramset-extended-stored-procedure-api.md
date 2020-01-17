---
title: srv_paramset (拡張ストアド プロシージャ API) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_paramset
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_paramset
ms.assetid: 2a509206-a1b8-4b20-b0a2-ef680cef7bd8
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 00645f619a89010bb4e2b112d50e00cbc6f40dce
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127155"
---
# <a name="srvparamset-extended-stored-procedure-api"></a>srv_paramset (拡張ストアド プロシージャ API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]代わりに CLR Integration をご使用ください。  
  
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
  
 *n*  
 設定するパラメーターの番号を示します。 最初のパラメーターは 1 です。  
  
 *data*  
 リモート ストアド プロシージャの戻りパラメーターとしてクライアントに返されるデータ値を指すポインターです。  
  
 *len*  
 返されるデータの実際の長さを指定します。 パラメーターのデータ型が固定長であり、NULL 値を許容しない型 (*srvbit* や *srvint1* など) である場合、*len* は無視されます。  
  
## <a name="returns"></a>戻り値  
 パラメーター値が正しく設定された場合は SUCCEED を返し、それ以外の場合は FAIL を返します。 FAIL を返すのは、現在のリモート ストアド プロシージャがない場合、*n* 番目のリモート ストアド プロシージャ パラメーターがない場合、パラメーターが戻りパラメーターでない場合、*len* 引数が無効である場合です。  
  
 *len* が 0 である場合は、NULL を返します。 *len* を 0 に設定する以外に、クライアントに NULL を返す方法はありません。  
  
 パラメーターが [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] データ型のいずれかである場合、この関数は次の値を返します。  
  
|新しいデータ型|戻り値のデータ長|  
|--------------------|------------------------|  
|`BITN`|**NULL:** *len* = 0、data = IG、RET = 0<br /><br /> **ZERO:** なし<br /><br /> **>=255:** なし<br /><br /> **<255:** なし|  
|`BIGVARCHAR`|**NULL:** *len* = 0、data = IG、RET = 1<br /><br /> **ZERO:** *len* = IG、data = IG、RET = 0<br /><br /> **>=255:** *len* = max8k、data = valid、RET = 0<br /><br /> **<255:** *len* = <8k、data = valid、RET = 1|  
|`BIGCHAR`|**NULL:** *len* = 0、data = IG、RET = 1<br /><br /> **ZERO:** *len* = IG、data = IG、RET = 0<br /><br /> **>=255:** *len* = max8k、data = valid、RET = 0<br /><br /> **<255:** *len* = <8k、data = valid、RET = 1|  
|`BIGBINARY`|**NULL:** *len* = 0、data = IG、RET = 1<br /><br /> **ZERO:** *len* = IG、data = IG、RET = 0<br /><br /> **>=255:** *len* = max8k、data = valid、RET = 0<br /><br /> **<255:** *len* = <8k、data = valid、RET = 1|  
|`BIGVARBINARY`|**NULL:** *len* = 0、data = IG、RET = 1<br /><br /> **ZERO:** *len* = IG、data = IG、RET = 0<br /><br /> **>=255:** *len* = max8k、data = valid、RET = 0<br /><br /> **<255:** *len* = <8k、data = valid、RET = 1|  
|NCHAR|**NULL:** *len* = 0、data = IG、RET = 1<br /><br /> **ZERO:** *len* = IG、data = IG、RET = 0<br /><br /> **>=255:** *len* = max8k、data = valid、RET = 0<br /><br /> **<255:** *len* = <8k、data = valid、RET = 1|  
|NVARCHAR|**NULL:** *len* = 0、data = IG、RET = 1<br /><br /> **ZERO:** *len* = IG、data = IG、RET = 0<br /><br /> **>=255:** *len* = max8k、data = valid、RET = 0<br /><br /> **<255:** *len* = <8k、data = valid、RET = 1|  
|`NTEXT`|**NULL:** *len* = IG、data = IG、RET = 0<br /><br /> **ZERO:** *len* = IG、data = IG、RET = 0<br /><br /> **>=255:** *len* = IG、data = IG、RET = 0<br /><br /> **\<255:** *len* = IG、data = IG、RET = 0|  
|RET は srv_paramset の戻り値です。||  
|IG は値が無視されることを示します。||  
|valid はデータを指す任意の有効なポインターを示します。||  
  
## <a name="remarks"></a>コメント  
 パラメーターには、リモート ストアド プロシージャを使用してクライアントとアプリケーションとの間で受け渡しされるデータが格納されます。 クライアントは戻りパラメーターとして特定のパラメーターを指定できます。 この戻りパラメーターには、Open Data Services サーバー アプリケーションがクライアントに返す値を格納することができます。 戻りパラメーターの使用は、パラメーターの参照渡しに類似しています。  
  
 戻りパラメーターとして呼び出されていないパラメーターには、戻り値を設定できません。 パラメーターがどのように呼び出されたかを判別するには **srv_paramstatus** を使用します。  
  
 この関数は、パラメーターの戻り値を設定するものであり、戻り値を実際にクライアントに返す役割はありません。 **srv_paramset** に設定されているかどうかにかかわらず、すべての戻りパラメーターは、ステータス フラグ SRV_DONE_FINAL が設定された状態で **srv_senddone** が呼び出されると、自動的にクライアントに送信されます。  
  
 パラメーターを指定してリモート ストアド プロシージャを呼び出す場合、パラメーターは名前で指定することも、名前を使用せずにその位置を指定して渡すこともできます。 名前によるパラメーター指定と位置によるパラメーター指定を混合してリモート ストアド プロシージャを呼び出すと、エラーが発生します。 エラーが発生しても SRV_RPC ハンドラーは呼び出されますが、パラメーターが存在しないと見なされ、**srv_rpcparams** は 0 を返します。  
  
> [!IMPORTANT]  
>  拡張ストアド プロシージャのソース コードを十分に確認し、コンパイル済み DLL を、運用サーバーにインストールする前にテストする必要があります。 セキュリティの確認およびテストについて詳しくは、[Microsoft の Web サイト](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409 https://msdn.microsoft.com/security/)をご覧ください。  
  
## <a name="see-also"></a>関連項目  
 [srv_paramsetoutput &#40;拡張ストアド プロシージャ API&#41;](srv-paramsetoutput-extended-stored-procedure-api.md)  
  
  
