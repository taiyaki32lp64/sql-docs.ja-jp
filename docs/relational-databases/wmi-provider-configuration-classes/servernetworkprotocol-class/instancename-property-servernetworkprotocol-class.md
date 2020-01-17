---
title: InstanceName プロパティ (ServerNetworkProtocol)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- InstanceName Property (ServerNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- InstanceName property
ms.assetid: 456911c1-9881-4574-8576-0070eff78c27
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 89ef707d9dbca569f8b303356e10b4dc097f3b5c
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73660405"
---
# <a name="instancename-property-servernetworkprotocol-class"></a>InstanceName プロパティ (ServerNetworkProtocol クラス)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  サーバーネットワークプロトコルによって参照される [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスの名前を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.InstanceName [= value]  
```  
  
## <a name="parts"></a>要素  
 *object*  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のインスタンスによって使用されるネットワークプロトコルを表す[Servernetworkprotocol クラス](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocol-class/servernetworkprotocol-class.md)オブジェクト。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 サーバー ネットワーク プロトコルによって参照された [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスの名前を指定する文字列値。  
  
## <a name="remarks"></a>解説  
  
## <a name="see-also"></a>参照  
 [サーバーネットワークプロトコルと Net-library の構成](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
