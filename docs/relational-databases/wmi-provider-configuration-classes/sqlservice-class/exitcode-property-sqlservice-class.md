---
title: ExitCode プロパティ (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ExitCode Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ExitCode property
ms.assetid: e6b8bff2-946f-4abe-bd50-1f7bb11fdddf
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 392fc529b10e79d96a83ccd896733d14d0b8b4dc
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73659682"
---
# <a name="exitcode-property-sqlservice-class"></a>ExitCode プロパティ (SqlService クラス)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  サービスの開始時および停止時に検出される問題を定義した [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Win32 エラー コードを取得または設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.ExitCode [= value]  
```  
  
## <a name="parts"></a>要素  
 *object*  
 サービスを表す [SqlService クラス](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) オブジェクト。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 終了コードを指定する**uint32**値。  
  
## <a name="remarks"></a>解説  
 このプロパティは、エラーがこのクラスによって表されているサービスに特有な場合には、ERROR_SERVICE_SPECIFIC_ERROR (1066) に設定されます。 サービスは、実行時にこの値を NO_ERROR に設定し、通常終了時にも再度設定します。  
  
## <a name="see-also"></a>参照  
 [サービスの開始と停止](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
