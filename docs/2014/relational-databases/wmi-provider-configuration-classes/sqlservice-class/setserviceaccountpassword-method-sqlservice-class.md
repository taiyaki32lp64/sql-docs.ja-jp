---
title: SetServiceAccountPassword メソッド (SqlService クラス) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetServiceAccountPassword Method (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetServiceAccountPassword method
ms.assetid: e577a1ac-985c-4799-bb38-9393efc3def2
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 113d84526b34f9f702cd8da68a06c055c3b559e3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63062330"
---
# <a name="setserviceaccountpassword-method-sqlservice-class"></a>SetServiceAccountPassword メソッド (SqlService クラス)
  参照されたサービスの実行環境に対応するアカウントのパスワードを変更します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object  
.SetServiceAccountPassword(  
AccountOldPassword , ServiceStartPassword  
)  
  
```  
  
## <a name="parts"></a>要素  
 *object*  
 サービスを表す [SqlService クラス](sqlservice-class.md) オブジェクト。  
  
#### <a name="parameters"></a>パラメーター  
 *AccountOldPassword*  
 アカウントの既存のパスワードを指定する文字列値。  
  
 *ServiceStartPassword*  
 アカウントの新しいパスワードを指定する文字列値。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 `uint32` 値。サービスが正常に変更された場合は 0、要求がサポートされていない場合は 1 になります。それ以外の数値はエラーを示します。  
  
## <a name="remarks"></a>コメント  
  
