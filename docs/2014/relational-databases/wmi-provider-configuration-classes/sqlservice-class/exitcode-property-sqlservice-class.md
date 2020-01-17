---
title: ExitCode プロパティ (SqlService クラス) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- ExitCode Property (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- ExitCode property
ms.assetid: e6b8bff2-946f-4abe-bd50-1f7bb11fdddf
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 7a74c48cf512f33862f41484a5fb667918e81787
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63062490"
---
# <a name="exitcode-property-sqlservice-class"></a>ExitCode プロパティ (SqlService クラス)
  サービスの開始時および停止時に検出される問題を定義した [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Win32 エラー コードを取得または設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object  
.ExitCode [= value]  
```  
  
## <a name="parts"></a>要素  
 *object*  
 サービスを表す [SqlService クラス](sqlservice-class.md) オブジェクト。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 終了コードを指定する `uint32` 値。  
  
## <a name="remarks"></a>コメント  
 このプロパティは、エラーがこのクラスによって表されているサービスに特有な場合には、ERROR_SERVICE_SPECIFIC_ERROR (1066) に設定されます。 サービスは、実行時にこの値を NO_ERROR に設定し、通常終了時にも再度設定します。  
  
## <a name="see-also"></a>参照  
 [開始とサービスの停止](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
