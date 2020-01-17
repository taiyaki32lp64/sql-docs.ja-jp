---
title: srv_alloc (拡張ストアド プロシージャ API) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_alloc
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_alloc
ms.assetid: 91505c59-a273-452f-b71d-5e8205c21863
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 61157ab8ba2b9f47caf89b6a16a3edd830437abf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63138909"
---
# <a name="srv_alloc-extended-stored-procedure-api"></a>srv_alloc (拡張ストアド プロシージャ API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]代わりに CLR Integration をご使用ください。  
  
 メモリを動的に割り当てます。  
  
## <a name="syntax"></a>構文  
  
```  
  
void * srv_alloc ( DBINT  
size  
);  
  
```  
  
## <a name="arguments"></a>引数  
 *size*  
 割り当てるバイト数を指定します。  
  
## <a name="returns"></a>戻り値  
 新しく割り当てた領域を指すポインターを返します。 *size* で指定したバイト数を割り当てられない場合は、NULL ポインターを返します。  
  
## <a name="remarks"></a>コメント  
 **srv_alloc** 関数は、[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows API の **GlobalAlloc** 関数に相当します。 拡張ストアド プロシージャ API アプリケーションでは、通常の Windows API C ランタイムのメモリ管理関数を使用できます。  
  
> [!IMPORTANT]  
>  拡張ストアド プロシージャのソース コードを十分に確認し、コンパイル済み DLL を、運用サーバーにインストールする前にテストする必要があります。 セキュリティの確認およびテストについて詳しくは、[Microsoft の Web サイト](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)をご覧ください。  
  
  
