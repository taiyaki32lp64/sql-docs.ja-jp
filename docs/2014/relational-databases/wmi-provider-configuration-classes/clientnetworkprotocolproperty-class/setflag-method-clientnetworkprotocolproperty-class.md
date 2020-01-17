---
title: SetFlag メソッド (ClientNetworkProtocolProperty クラス) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetFlag Method (ClientNetworkProtocolProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetFlag method
ms.assetid: 0407520f-2f84-4f68-b2b7-429697286c1b
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 6c33eca0bf3281243aeee42ed89001cf9108d5d4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63245088"
---
# <a name="setflag-method-clientnetworkprotocolproperty-class"></a>SetFlag メソッド (ClientNetworkProtocolProperty クラス)
  によって参照される現在のプロパティのフラグを設定、 [PropertyIdx プロパティ (ClientNetworkProtocolProperty クラス)](clientnetworkprotocolproperty-class.md)値。  
  
## <a name="syntax"></a>構文  
  
```  
  
object  
.SetFlag(  
BoolValue  
) [=]  
```  
  
## <a name="parts"></a>要素  
 *object*  
 A [ClientNetworkProtocolProperty クラス](clientnetworkprotocolproperty-class.md)によって使用されるネットワーク プロトコルの属性を表すオブジェクトを[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]クライアント。  
  
#### <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|---------------|-----------------|  
|*BoolValue*|フラグの新しい値を指定するブール値|  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 `uint32` 値。サービスが正常に変更された場合は 0、要求がサポートされていない場合は 1 になります。それ以外の数値はエラーを示します。  
  
## <a name="remarks"></a>コメント  
  
## <a name="see-also"></a>参照  
 [クライアント プロトコルの構成](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
  
