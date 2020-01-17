---
title: MultiIpConfigurationSupport プロパティ (ServerNetworkProtocol)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- MultiIpConfigurationSupport Property (ServerNetworkProtocol
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- MultiIpConfigurationSupport property
ms.assetid: 442c6133-4038-42db-a67d-2631285ac76b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6ed53a60bd0ef285468d71c4018ba7a4ed9cd8c6
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73660383"
---
# <a name="multiipconfigurationsupport-property-servernetworkprotocol-class"></a>MultiIpConfigurationSupport プロパティ (ServerNetworkProtocol クラス)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  複数の IP アドレスがサーバー ネットワーク プロトコルによってサポートされるかどうかを指定するブール型のプロパティを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.MultiIpConfigurationSupport [= value]  
```  
  
## <a name="parts"></a>要素  
 *object*  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のインスタンスによって使用されるネットワークプロトコルを表す[Protocolname プロパティ (ServerNetworkProtocol クラス)](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocol-class/protocolname-property-servernetworkprotocol-class.md)オブジェクト。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 複数の IP アドレスがサーバーネットワークプロトコルによってサポートされているかどうかを指定するブール値。サーバーネットワークプロトコルによって複数の ip アドレスがサポートされている場合は**true** 、複数の ip アドレスがによってサポートされていない場合は**false**を指定します。サーバーネットワークプロトコル。  
  
## <a name="remarks"></a>解説  
  
## <a name="see-also"></a>参照  
 [サーバーネットワークプロトコルと Net-library の構成](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
