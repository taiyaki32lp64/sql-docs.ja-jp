---
title: SetStringValue メソッド (ClientNetworkProtocolProperty クラス) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetStringValue Method (ClientNetworkProtocolProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetStringValue method
ms.assetid: 88d67b22-0eea-48c9-ab73-e0b4907953df
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 82b89246d6289d0b19ee97e68e94f77d7cb30a77
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63244991"
---
# <a name="setstringvalue-method-clientnetworkprotocolproperty-class"></a>SetStringValue メソッド (ClientNetworkProtocolProperty クラス)
  [PropertyIdx プロパティ (ClientNetworkProtocolProperty クラス)](clientnetworkprotocolproperty-class.md) の値によって参照される現在のプロパティの文字列値を設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object  
.SetStringValue(  
StrValue  
)  
  
```  
  
## <a name="parts"></a>要素  
 *object*  
 A [ClientNetworkProtocolProperty クラス](clientnetworkprotocolproperty-class.md)によって使用されるネットワーク プロトコルの属性を表すオブジェクトを[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]クライアント。  
  
#### <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|---------------|-----------------|  
|*strValue*|現在のプロパティの新しい値を指定する文字列値|  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 `uint32` 値。サービスが正常に変更された場合は 0、要求がサポートされていない場合は 1 になります。それ以外の数値はエラーを示します。  
  
## <a name="remarks"></a>コメント  
  
## <a name="see-also"></a>参照  
 [クライアント プロトコルの構成](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
  
