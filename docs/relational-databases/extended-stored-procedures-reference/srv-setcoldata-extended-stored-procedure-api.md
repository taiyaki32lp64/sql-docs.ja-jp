---
title: srv_setcoldata (拡張ストアド プロシージャ API) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_setcoldata
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_setcoldata
ms.assetid: 2e19205a-25ca-4d4a-916b-d591cf2c892b
author: rothja
ms.author: jroth
ms.openlocfilehash: 36020fb9df7b98338cd64a8e476b8da0b5196c0e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68119645"
---
# <a name="srv_setcoldata-extended-stored-procedure-api"></a>srv_setcoldata (拡張ストアド プロシージャ API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]代わりに CLR Integration をご使用ください。  
  
 列のデータの現在のアドレスを指定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
int srv_setcoldata (  
SRV_PROC *  
srvproc  
,  
int   
column  
,  
void *  
data   
);  
```  
  
## <a name="arguments"></a>引数  
 *srvproc*  
 特定のクライアント接続のためのハンドルである SRV_PROC 構造体を指すポインターです。 この構造体には、アプリケーションとクライアントの間の通信やデータを管理するために、拡張ストアド プロシージャ API ライブラリで使用する情報が格納されます。  
  
 *column*  
 アドレスを指定している列の番号を示します。 列には 1 から始まる番号が割り当てられます。  
  
 *data*  
 列のデータを指すポインターです。 別に **srv_setcoldata** を呼び出して列データを置き換えるか、**srv_senddone** を呼び出すまでは、*data* に割り当てたメモリを解放しないでください。  
  
## <a name="returns"></a>戻り値  
 SUCCEED または FAIL。  
  
## <a name="remarks"></a>Remarks  
 行の各列はあらかじめ **srv_describe** で定義しておく必要があります。 列データのアドレスは、最初は **srv_describe** で設定されます。 列データのアドレスが変わった場合は、データの新しいアドレスを指定するために **srv_setcoldata** を呼び出してから、変更された各列について改めて **srv_setcoldata** を呼び出す必要があります。  
  
 NULL データを表現するには、**srv_setcollen** を使用して列の長さを 0 に設定します。 これにより、データのアドレスは無視されます。  
  
> [!IMPORTANT]  
>  拡張ストアド プロシージャのソース コードを十分に確認し、コンパイル済み DLL を、運用サーバーにインストールする前にテストする必要があります。 セキュリティの確認およびテストについて詳しくは、[Microsoft の Web サイト](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)をご覧ください。  
  
## <a name="see-also"></a>参照  
 [srv_describe &#40;拡張ストアド プロシージャ API&#41;](../../relational-databases/extended-stored-procedures-reference/srv-describe-extended-stored-procedure-api.md)  
  
  
