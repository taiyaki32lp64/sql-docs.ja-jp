---
title: srv_setcollen (拡張ストアド プロシージャ API) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_setcollen
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_setcollen
ms.assetid: 3c60f1c3-4562-463a-a259-12df172788bd
author: rothja
ms.author: jroth
ms.openlocfilehash: 15bd83b902ad64213fcde3ef15a185d69fde8cd4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68119637"
---
# <a name="srv_setcollen-extended-stored-procedure-api"></a>srv_setcollen (拡張ストアド プロシージャ API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]代わりに CLR Integration をご使用ください。  
  
 可変長列または NULL 値を許容する列の、現在のデータ長をバイト数で指定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
int srv_setcollen (  
SRV_PROC *  
srvproc  
,  
int   
column  
,  
int  
len   
);  
```  
  
## <a name="arguments"></a>引数  
 *srvproc*  
 特定のクライアント接続のためのハンドルである SRV_PROC 構造体を指すポインターです。 この構造体には、アプリケーションとクライアントの間の通信やデータを管理するために、拡張ストアド プロシージャ API ライブラリで使用する情報が格納されます。  
  
 *column*  
 データ長を指定している列の番号を示します。 列には 1 から始まる番号が割り当てられます。  
  
 *len*  
 列データの長さをバイト数で指定します。 長さが 0 である場合、列データの値が NULL であることを示します。  
  
## <a name="returns"></a>戻り値  
 SUCCEED または FAIL。  
  
## <a name="remarks"></a>Remarks  
 行の各列は最初に **srv_describe** で定義する必要があります。 列のデータ長は **srv_describe** または **srv_setcollen** の前回呼び出し時に設定されます。 ある行について可変長のデータ (NULL 終端データ) が変化する場合、**srv_sendrow** を呼び出す前に、**srv_setcollen** を使用してデータを新しい長さに変更する必要があります。 NULL 値を許容する列では、NULL を許容する SRVINTN などのデータ型に *desttype* を設定して **srv_describe** を呼び出してから、*len* を 0 に設定して **srv_setcollen** を呼び出すことにより NULL データを指定します。 拡張ストアド プロシージャ API を使用して長さがゼロのデータを指定することはできません。  
  
 列データ型が可変長の場合、*len* の値は確認されません。 固定長の列について呼び出された場合、この関数は FAIL を返します。  
  
> [!IMPORTANT]  
>  拡張ストアド プロシージャのソース コードを十分に確認し、コンパイル済み DLL を、運用サーバーにインストールする前にテストする必要があります。 セキュリティの確認およびテストについて詳しくは、[Microsoft の Web サイト](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)をご覧ください。  
  
## <a name="see-also"></a>参照  
 [srv_describe &#40;拡張ストアド プロシージャ API&#41;](../../relational-databases/extended-stored-procedures-reference/srv-describe-extended-stored-procedure-api.md)  
  
  
