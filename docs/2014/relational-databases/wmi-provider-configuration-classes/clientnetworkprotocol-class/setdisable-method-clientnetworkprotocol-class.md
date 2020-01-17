---
title: SetDisable メソッド (ClientNetworkProtocol クラス) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetDisable Method (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetDisable method
ms.assetid: bce69ab9-ea5b-43fd-8114-08b1b5890755
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 7b37e2cd0b3342d6ecb520add0bbe4fd533e786a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63192862"
---
# <a name="setdisable-method-clientnetworkprotocol-class"></a>SetDisable メソッド (ClientNetworkProtocol クラス)
  指定されているクライアント ネットワーク プロトコルを無効になります、 [Configure Client Protocols](https://technet.microsoft.com/library/ms181035.aspx)します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object  
.SetDisable()  
  
```  
  
## <a name="parts"></a>要素  
 *object*  
 A [ClientNetworkProtocol クラス](clientnetworkprotocol-class.md)によって使用されるネットワーク プロトコルを表すオブジェクトを[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]クライアント。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 `uint32` 値。サービスが正常に変更された場合は 0、要求がサポートされていない場合は 1 になります。それ以外の数値はエラーを示します。  
  
## <a name="remarks"></a>コメント  
  
## <a name="see-also"></a>関連項目  
 [クライアント ネットワーク プロトコルとネットワーク ライブラリの構成](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
