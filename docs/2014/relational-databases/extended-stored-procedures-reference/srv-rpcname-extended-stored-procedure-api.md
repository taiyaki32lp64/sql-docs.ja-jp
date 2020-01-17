---
title: srv_rpcname (拡張ストアド プロシージャ API) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_rpcname
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_rpcname
ms.assetid: 0a1424e4-3319-4836-b8d8-5e0344cc683f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f309349b2867412d552372e83ed1947b34242336
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63046650"
---
# <a name="srvrpcname-extended-stored-procedure-api"></a>srv_rpcname (拡張ストアド プロシージャ API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]代わりに CLR Integration をご使用ください。  
  
 現在のリモート ストアド プロシージャのプロシージャ名部分を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
DBCHAR * srv_rpcname (  
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
 データベース名の長さを受け取る整数変数を指すポインターです。 *len* が NULL である場合、リモート ストアド プロシージャ名の長さは返されていません。  
  
## <a name="returns"></a>戻り値  
 現在のリモート ストアド プロシージャのリモート ストアド プロシージャ名部分に対応した NULL 終端文字列を指す DBCHAR ポインターを返します。 現在のリモート ストアド プロシージャがない場合は、NULL が返され、*len* が -1 に設定されます。  
  
## <a name="remarks"></a>コメント  
 この関数は、リモート ストアド プロシージャの名前のみを返します。 所有者、データベース名、およびリモート ストアド プロシージャ番号に対応する省略可能な指定子は含まれません。  
  
 リモート ストアド プロシージャがなくても **srv_rpcname** を呼び出すことは有効であるため (情報エラーは発生しない)、この関数にはリモート ストアド プロシージャが存在するかどうかを判断する手段が用意されています。  
  
> [!IMPORTANT]  
>  拡張ストアド プロシージャのソース コードを十分に確認し、コンパイル済み DLL を、運用サーバーにインストールする前にテストする必要があります。 セキュリティの確認およびテストについて詳しくは、[Microsoft の Web サイト](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409 https://msdn.microsoft.com/security/)をご覧ください。  
  
  
