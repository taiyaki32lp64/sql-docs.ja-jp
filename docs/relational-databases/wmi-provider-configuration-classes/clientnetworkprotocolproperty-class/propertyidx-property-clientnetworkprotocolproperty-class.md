---
title: PropertyIdx プロパティ (ClientNetworkProtocolProperty)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- PropertyIdx Property (ClientNetworkProtocolProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- PropertyIdx property
ms.assetid: d7845962-ac68-4435-9c59-70ec450fec88
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b3330ab2be25fdeccab3c39d6d9528adedaabc0e
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73660369"
---
# <a name="propertyidx-property-clientnetworkprotocolproperty-class"></a>PropertyIdx プロパティ (ClientNetworkProtocolProperty クラス)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  [Clientnetworkprotocol クラス](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md)オブジェクトの[Properties プロパティ (clientnetworkprotocol クラス)](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/properties-property-clientnetworkprotocol-class.md)によって参照されるプロパティ配列内のプロパティのインデックス値を取得または設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.PropertyIdx [= value]  
```  
  
## <a name="parts"></a>要素  
 *object*  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] クライアントによって使用されるネットワークプロトコルの属性を表す[Clientnetworkprotocolproperty クラス](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/clientnetworkprotocolproperty-class.md)オブジェクト。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 現在のプロパティの配列インデックス値を指定する**uint32**値。  
  
## <a name="remarks"></a>解説  
  
## <a name="see-also"></a>参照  
 [クライアント プロトコルの構成](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
  
