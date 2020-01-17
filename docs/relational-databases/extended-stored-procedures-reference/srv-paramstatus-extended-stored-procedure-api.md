---
title: srv_paramstatus (拡張ストアド プロシージャ API) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_paramstatus
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_paramstatus
ms.assetid: 86cecd45-0b09-42e9-8152-32a12a1c2b7a
author: rothja
ms.author: jroth
ms.openlocfilehash: 9898dbde804b0c4615a5dc4ad6b8fefa79000ccb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68005573"
---
# <a name="srv_paramstatus-extended-stored-procedure-api"></a>srv_paramstatus (拡張ストアド プロシージャ API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]代わりに CLR Integration をご使用ください。  
  
 特定のリモート ストアド プロシージャ呼び出しのパラメーターの状態を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
int srv_paramstatus (  
SRV_PROC *  
srvproc  
,  
int  
n   
);  
```  
  
## <a name="arguments"></a>引数  
 *srvproc*  
 特定のクライアント接続のためのハンドル (この場合は、リモート ストアド プロシージャ呼び出しを受け取るハンドル) である SRV_PROC 構造体を指すポインターです。 この構造体には、アプリケーションとクライアントの間の通信やデータを管理するために、拡張ストアド プロシージャ API ライブラリで使用する情報が格納されます。  
  
 *n*  
 パラメーターの番号を示します。 最初のパラメーターは 1 です。  
  
## <a name="returns"></a>戻り値  
 このパラメーターの状態フラグを示す **int** 値を返します。 現時点では、フラグは 1 つのみです。ビット 0 が 1 に設定されていた場合、そのパラメーターは戻りパラメーターです。 *n* 番目のパラメーターがない場合、またはリモート ストアド プロシージャがない場合は、-1 を返します。  
  
## <a name="remarks"></a>Remarks  
 このルーチンは、リモート ストアド プロシージャ呼び出しのパラメーターに関する状態フラグを返します。  
  
 パラメーターには、リモート ストアド プロシージャを使用してクライアントとアプリケーションとの間で受け渡しされるデータが格納されます。 クライアントは戻りパラメーターとして特定のパラメーターを指定できます。 この戻りパラメーターには、アプリケーションからクライアントに返す値を格納できます。  
  
 現在使用されている唯一の状態フラグは、パラメーターが戻りパラメーターかどうかを示すものです。  
  
 パラメーターを指定してリモート ストアド プロシージャを呼び出す場合、パラメーターは名前で指定することも、名前を使用せずにその位置を指定して渡すこともできます。 名前によるパラメーター指定と位置によるパラメーター指定を混合してリモート ストアド プロシージャを呼び出すと、エラーが発生します。 エラーが発生しても SRV_RPC ハンドラーは呼び出されますが、パラメーターが存在しないと見なされ、**srv_rpcparams** は 0 を返します。  
  
> [!IMPORTANT]  
>  拡張ストアド プロシージャのソース コードを十分に確認し、コンパイル済み DLL を、運用サーバーにインストールする前にテストする必要があります。 セキュリティの確認およびテストについて詳しくは、[Microsoft の Web サイト](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)をご覧ください。  
  
## <a name="see-also"></a>参照  
 [srv_rpcparams &#40;拡張ストアド プロシージャ API&#41;](../../relational-databases/extended-stored-procedures-reference/srv-rpcparams-extended-stored-procedure-api.md)  
  
  
