---
title: Properties プロパティ (ClientNetworkProtocol)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- Properties Property (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- Properties property
ms.assetid: 7e0a4e38-4555-4750-8fd3-4425b29e6aa1
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8fcca87157b2f6f7fe881c35b72ea54d965e095c
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73659247"
---
# <a name="properties-property-clientnetworkprotocol-class"></a>Properties プロパティ (ClientNetworkProtocol クラス)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  [Configure Client Protocols (クライアント プロトコルの構成)](https://technet.microsoft.com/library/ms181035.aspx)によって指定された現在のクライアント ネットワーク プロトコルに関連付けられたプロパティを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.Properties [= value]  
```  
  
## <a name="parts"></a>要素  
 *object*  
 [クライアントによって使用されるネットワーク プロトコルを表す](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) ClientNetworkProtocol クラス [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] オブジェクト。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 [OrderValue](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/clientnetworkprotocolproperty-class.md) プロパティによって参照される現在のクライアント ネットワーク プロトコルによってサポートされているプロパティを表す **ClientNetworkProtocolProperty クラス** オブジェクトの配列。  
  
## <a name="remarks"></a>解説  
  
## <a name="see-also"></a>参照  
 [クライアントネットワークプロトコルと Net-library の構成](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
