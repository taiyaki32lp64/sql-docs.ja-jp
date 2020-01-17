---
title: SetNumericalValue メソッド (ServerNetworkProtocolProperty クラス) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetNumericalValue Method (ServerNetworkProtocolProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetNumericalValue method
ms.assetid: b3b4bce8-9d9e-4ccb-a223-0454281353b0
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: e2b3318b9aae0412e827875af35cbdf0477e059f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62736282"
---
# <a name="setnumericalvalue-method-servernetworkprotocolproperty-class"></a>SetNumericalValue メソッド (ServerNetworkProtocolProperty クラス)
  参照されたプロパティの数値を設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object  
.SetNumericalValue(  
NumValue  
)  
  
```  
  
## <a name="parts"></a>要素  
 *object*  
 [ServerNetworkProtocolProperty クラス] servernetworkprotocolproperty-class.md) のインスタンス上のネットワーク プロトコルの属性を表すオブジェクトを[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]します。  
  
#### <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|---------------|-----------------|  
|*%Numvalue% 個*|現在のプロパティの新しい値を指定する `uint32` 値|  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 `uint32` 値。サービスが正常に変更された場合は 0、要求がサポートされていない場合は 1 になります。それ以外の数値はエラーを示します。  
  
## <a name="remarks"></a>コメント  
  
## <a name="see-also"></a>参照  
 [サーバー ネットワーク プロトコルとネットワーク ライブラリの構成](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
