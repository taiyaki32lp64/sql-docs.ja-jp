---
title: srv_getbindtoken (拡張ストアド プロシージャ API) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_getbindtoken
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_getbindtoken
ms.assetid: c947d011-08ac-4fb8-b925-3da6e0999277
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: dec2e73de3c4c3525b29b44b7c4563a7fd6887ba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127300"
---
# <a name="srvgetbindtoken-extended-stored-procedure-api"></a>srv_getbindtoken (拡張ストアド プロシージャ API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]代わりに CLR Integration をご使用ください。  
  
 拡張ストアド プロシージャを起動する現在のクライアント セッションに含まれるトランザクションのバインド トークンを取得します。  
  
 すると拡張ストアド プロシージャは **sp_bindsession** を使用して、同じサーバーに対して作成した新しいセッションを既存のトランザクションにバインドします。これにより新しいセッションは、この拡張ストアド プロシージャを起動したクライアント セッションと、同じトランザクション ロック領域を共有できるようになります。  
  
## <a name="syntax"></a>構文  
  
```  
  
int srv_getbindtoken (  
SRV_PROC*  
srvproc  
,  
char*  
bindtoken  
);  
  
```  
  
## <a name="arguments"></a>引数  
 *srvproc*  
 特定のクライアント接続のためのハンドルである SRV_PROC 構造体を指すポインターです。 この構造体には、アプリケーションとクライアントの間の通信やデータを管理するために、拡張ストアド プロシージャ API ライブラリで使用するすべての情報が格納されます。  
  
 *bindtoken*  
 バインド トークンのコピー先バッファーを指すポインターです。 バインド トークンは NULL 終端文字列として表されます。 指定するバッファーは、255 バイト以上の長さにする必要があります。  
  
## <a name="returns"></a>戻り値  
 SUCCEED または FAIL。  
  
## <a name="remarks"></a>コメント  
  
### <a name="to-bind-an-extended-stored-procedure-session-to-the-client-session-that-called-it-so-they-share-the-same-transaction-lock-space"></a>同じトランザクション ロック領域を共有するために、拡張ストアド プロシージャのセッションを呼び出し元のクライアント セッションにバインドするには  
  
1.  拡張ストアド プロシージャが **svr_getbindtoken** を呼び出し、そのセッションの現在のトランザクションのバインド トークンを取得します。 トークンは、指定された *bindtoken* パラメーターで返されます。  
  
2.  拡張ストアド プロシージャが同じサーバーに対して新しいセッションを開きます。 そのセッション内で、拡張ストアド プロシージャが **sp_bindsession** を含むバインド トークンを使用し、新しいセッションを同じトランザクションにバインドします。 この拡張ストアド プロシージャは、複数のセッションを作成し、すべてのセッションを同じトランザクションにバインドすることができます。  
  
3.  外部ストアド プロシージャが返されたり、**sp_bindsession** が空文字列で呼び出されたりすると、セッションのバインドが解除されます。  
  
    > [!NOTE]  
    >  共有の接続にアクセスできるバインドされたセッションは、一度に 1 つだけです。 あるセッションが現在サーバーでステートメントを実行しているかサーバーからの結果を待っている場合、バインドされた同じ接続を共有している他のセッションは、現在のセッションで現在のステートメントの実行が完了するまでサーバーにアクセスできません。 あるセッションが、サーバーがビジー状態のときに接続にアクセスを試みると、そのセッションは競合状態になりにエラーが返されます。その際、接続が使用中なので後でセッションを再試行する必要があることが示されます。  
  
> [!IMPORTANT]  
>  拡張ストアド プロシージャのソース コードを十分に確認し、コンパイル済み DLL を、運用サーバーにインストールする前にテストする必要があります。 セキュリティの確認およびテストについて詳しくは、[Microsoft の Web サイト](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)をご覧ください。  
  
## <a name="see-also"></a>参照  
 [sp_bindsession &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-bindsession-transact-sql)   
 [sp_getbindtoken &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-getbindtoken-transact-sql)  
  
  
