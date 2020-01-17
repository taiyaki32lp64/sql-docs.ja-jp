---
title: srv_rpcowner (拡張ストアド プロシージャ API) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_rpcowner
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_rpcowner
ms.assetid: e81a60e6-14ea-47bc-a11c-3d7635344447
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 68e5d0214a2bd14a466b7a0c40f792031d3fac5d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62745503"
---
# <a name="srvrpcowner-extended-stored-procedure-api"></a>srv_rpcowner (拡張ストアド プロシージャ API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]代わりに CLR Integration をご使用ください。  
  
 現在のリモート ストアド プロシージャの所有者部分を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
DBCHAR * srv_rpcowner (  
SRV_PROC *  
srvproc  
,  
int *  
len   
);  
  
```  
  
## <a name="arguments"></a>引数  
 *srvproc*  
 特定のクライアント接続のためのハンドル (この場合は、リモート ストアド プロシージャを受け取るハンドル) である SRV_PROC 構造体を指すポインターです。 この構造体には、アプリケーションとクライアントの間の通信やデータを管理するために、拡張ストアド プロシージャ API ライブラリで使用する情報が格納されます。  
  
 *len*  
 所有者名の長さを受け取る整数変数を指すポインターです。 パラメーター *len* は NULL になる場合があります。NULL 値の場合、所有者部分の長さは返されていません。  
  
## <a name="returns"></a>戻り値  
 現在のリモート ストアド プロシージャの所有者部分を表した  NULL 終端文字列を指す DBCHAR ポインターです。 現在のリモート ストアド プロシージャがない場合は、NULL が返され、*len* が - 1 に設定されます。  
  
## <a name="remarks"></a>コメント  
 この関数は、リモート ストアド プロシージャの所有者部分だけを返します。 名前、リモート ストアド プロシージャ名、およびリモート ストアド プロシージャ番号の省略可能な各指定子は含まれません。  
  
> [!IMPORTANT]  
>  拡張ストアド プロシージャのソース コードを十分に確認し、コンパイル済み DLL を、運用サーバーにインストールする前にテストする必要があります。 セキュリティの確認およびテストについて詳しくは、[Microsoft の Web サイト](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)をご覧ください。  
  
  
