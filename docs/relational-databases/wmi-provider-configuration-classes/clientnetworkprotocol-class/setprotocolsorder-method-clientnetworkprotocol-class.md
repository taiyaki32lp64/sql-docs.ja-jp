---
title: SetProtocolsOrder メソッド (ClientNetworkProtocol)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetProtocolsOrder Method (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetProtocolsOrder method
ms.assetid: b86d98b9-aae4-4e74-b4da-1ec984d5c8b4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 88becd0d5a137d88b446e18fa0ef0798524bc0c1
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73659461"
---
# <a name="setprotocolsorder-method-clientnetworkprotocol-class"></a>SetProtocolsOrder メソッド (ClientNetworkProtocol クラス)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  プロトコル リストの順序を変更します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.SetProtocolsOrder(ProtocolOrderList)  
```  
  
## <a name="parts"></a>指定項目  
 *オブジェクト (object)*  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] クライアントによって使用されるネットワークプロトコルを表す[Clientnetworkprotocol クラス](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md)オブジェクト。  
  
#### <a name="parameters"></a>パラメーター  
  
|パラメーター|[説明]|  
|---------------|-----------------|  
|*ProtocolOrderList*|クライアント ネットワーク プロトコルを新しい順序でリストした string[] 配列|  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 **uint32** 値。サービスが正常に変更された場合は 0、要求がサポートされていない場合は 1 になります。それ以外の数値はエラーを示します。  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>参照  
 [クライアントプロトコルの構成](https://technet.microsoft.com/library/ms181035.aspx)   
 [クライアントネットワークプロトコルと Net-library の構成](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
