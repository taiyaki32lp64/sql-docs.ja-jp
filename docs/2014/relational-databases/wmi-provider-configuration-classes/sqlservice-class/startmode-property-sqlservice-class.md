---
title: StartMode プロパティ (SqlService クラス) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- StartMode Property (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- StartMode property
ms.assetid: c0c2c7f8-d4ae-44f2-ad8e-aecfcb7c2878
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: bf77e36824c05a0f07bc789c380cffbc1518669d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63187826"
---
# <a name="startmode-property-sqlservice-class"></a>StartMode プロパティ (SqlService クラス)
  サービスの開始モードを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object  
.StartMode [= value]  
```  
  
## <a name="parts"></a>要素  
 *object*  
 サービスを表す [SqlService クラス](sqlservice-class.md) オブジェクト。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 サービスのモードを指定する uint32 値。  
  
 値は、次のいずれかを指定できます。  
  
 Boot  
 値 = 0。 オペレーティング システム ローダーによって開始されるサービスです。 このオプションは、ドライバー サービスにのみ有効です。  
  
 システム  
 値 = 1。 `IoInitSystem` メソッドによって開始されるサービスです。 このオプションは、ドライバー サービスにのみ有効です。  
  
 Automatic  
 値 = 2。 システムの起動時にサービス コントロール マネージャーによって自動的に開始されるサービスです。  
  
 手動  
 値 = 3。 プロセスが `StartService` メソッドを呼び出すとコンピューター マネージャーによって開始されるサービスです。  
  
 Disabled  
 値 = 4。 サービスを開始できません。  
  
## <a name="remarks"></a>コメント  
  
## <a name="see-also"></a>参照  
 [開始とサービスの停止](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
