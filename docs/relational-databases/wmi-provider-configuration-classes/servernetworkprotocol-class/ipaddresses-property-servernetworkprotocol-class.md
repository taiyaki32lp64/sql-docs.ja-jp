---
title: IpAddresses プロパティ (ServerNetworkProtocol)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- IpAddresses Property (ServerNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- IpAddresses property
ms.assetid: e5d66f7e-9719-436e-b723-12d56f914a05
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ad88dbca2f3e71c6a68398e0f57748b8b517414b
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73660349"
---
# <a name="ipaddresses-property-servernetworkprotocol-class"></a>IpAddresses プロパティ (ServerNetworkProtocol クラス)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  サーバー ネットワーク プロトコルに関連付けられた IP アドレスを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.IpAddresses [= value]  
```  
  
## <a name="parts"></a>要素  
 *object*  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のインスタンスによって使用されるネットワークプロトコルを表す**Servernetworkprotocol**オブジェクト。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 サーバーネットワークプロトコルによってサポートされる IP アドレスを表す[ServerNetworkProtocolIPAdress クラス](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocolipaddress-class/servernetworkprotocolipaddress-class.md)オブジェクトの配列。  
  
## <a name="remarks"></a>解説  
  
## <a name="see-also"></a>参照  
 [サーバーネットワークプロトコルと Net-library の構成](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
