---
title: srv_pfield (拡張ストアド プロシージャ API) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_pfield
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_pfield
ms.assetid: a61e4c1f-e65b-48ea-a7d1-3e1544af389d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ed4abfe8914c7f6b1dc3e22de7a321419b8d9cee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127112"
---
# <a name="srvpfield-extended-stored-procedure-api"></a>srv_pfield (拡張ストアド プロシージャ API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]代わりに CLR Integration をご使用ください。  
  
 データベース接続に関する情報を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
DBCHAR * srv_pfield (  
SRV_PROC *  
srvproc  
,  
int   
field  
,  
int *  
len  
);  
  
```  
  
## <a name="arguments"></a>引数  
 *srvproc*  
 データベース接続を特定するポインターです。  
  
 *field*  
 その接続について返すデータを指定します。  
  
|値|戻り値|  
|-----------|-------------|  
|SRV_APPLNAME|接続の確立時にクライアントから提供されたアプリケーション名。|  
|SRV_BCPFLAG|クライアントが一括コピー操作の準備中である場合は TRUE、それ以外の場合は FALSE を示すフラグ。|  
|SRV_CLIB|クライアントがサーバーと通信できるようにするライブラリの名前。|  
|SRV_CPID|クライアント ソース コンピューターのクライアント プロセス ID。|  
|SRV_HOST|接続の確立時にクライアントから提供されたクライアント コンピューターの名前。|  
|SRV_LIBVERS|クライアント ライブラリのバージョン。|  
|SRV_LSECURE|フラグ。 その接続で、ログインに統合セキュリティを使用した場合は TRUE を示します。|  
|SRV_NETWORK_MODULE|接続に使用された Net-Library DLL の名前。|  
|SRV_NETWORK_VERSION|接続に使用された Net-Library DLL のバージョン。|  
|SRV_NETWORK_CONNECTION|現在の *srvproc* 接続で使用した Net-Library DLL に渡された接続文字列。|  
|SRV_PIPEHANDLE|接続されたクライアントのパイプ ハンドルを格納した文字列。名前付きパイプを使用しないネットワークにクライアントが接続されている場合は NULL。 このハンドルを [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows で有効なパイプ ハンドルとして使用するには、この文字列を整数に変換します。|  
|SRV_RMTSERVER|クライアント プロセスのログイン元であるサーバー。 クライアントからのログインの場合、この値は空文字列になります。|  
|SRV_ROWSENT|現在の結果セットについて、*srvproc* で送信済みの行数。|  
|SRV_SPID|*srvproc* のサーバー スレッド ID。 拡張ストアド プロシージャでは、この値は **sys.sysprocesses** の **kpid** 列に等しく、時間の経過に伴って変化します。|  
|SRV_SPROC_CODEPAGE|マルチバイト データを解釈するためにサーバーで使用するコード ページ。|  
|SRV_STATUS|*srvproc* の現在の状態 (running または closed)。|  
|SRV_TYPE|*srvproc* の接続の種類。 server が返される場合、*srvproc* は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを拠点としています。 client が返される場合、*srvproc* は DB-Library クライアントまたは ODBC クライアントを拠点としています。|  
|SRV_USER|接続のユーザー名。|  
|||  
  
 *len*  
 返された *field* 値の長さを格納した **int** 型変数を指すポインターです。 *len* が NULL の場合、文字列の長さは返されていません。  
  
## <a name="returns"></a>戻り値  
 SRV_PROC 構造体にある指定されたフィールドの現在値を格納した NULL 終端文字列へのポインターを返します。 フィールドが空の場合は空文字列への有効なポインターが返され、*len* は 0 になります。 フィールドが指定されていない場合は NULL を返し、*len* は -1 になります。  
  
> [!IMPORTANT]  
>  拡張ストアド プロシージャのソース コードを十分に確認し、コンパイル済み DLL を、運用サーバーにインストールする前にテストする必要があります。 セキュリティの確認とテストについては、「[セキュリティ TechCenter](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)」をご覧ください。  
  
  
