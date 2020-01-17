---
title: GetNextOrderValue メソッド (ClientNetworkProtocol)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- GetNextOrderValue Method (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- GetNextOrderValue method
ms.assetid: d741dc5c-c225-43d9-a730-7ad664ac525f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1f9b9a8d69dad76d2ec1d6e38f7151238d0e91c1
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73660746"
---
# <a name="getnextordervalue-method-clientnetworkprotocol-class"></a>GetNextOrderValue メソッド (ClientNetworkProtocol クラス)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  プロトコル リスト内で次の位置にあるプロトコルを選択します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.GetNextOrderValue()  
```  
  
## <a name="parts"></a>指定項目  
 *オブジェクト (object)*  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] クライアントによって使用されるネットワークプロトコルを表す[Clientnetworkprotocol クラス](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md)オブジェクト。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 **uint32** 値。サービスが正常に変更された場合は 0、要求がサポートされていない場合は 1 になります。それ以外の数値はエラーを示します。  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>参照  
 [クライアントプロトコルの構成](https://technet.microsoft.com/library/ms181035.aspx)   
 [クライアントネットワークプロトコルと Net-library の構成](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
