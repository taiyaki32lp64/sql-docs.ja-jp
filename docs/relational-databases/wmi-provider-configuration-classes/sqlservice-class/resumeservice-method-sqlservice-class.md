---
title: ResumeService メソッド (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ResumeService Method (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ResumeService method
ms.assetid: 0b0a5f08-b95e-4626-bf81-309da7a0aacd
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 40c0822bc8b881153909f77ec50b0c9de9883dec
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73660935"
---
# <a name="resumeservice-method-sqlservice-class"></a>ResumeService メソッド (SqlService クラス)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  サービスを再開状態にする動作を試行します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.ResumeService()  
```  
  
## <a name="parts"></a>要素  
 *object*  
 サービスを表す [SqlService クラス](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) オブジェクト。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 Uint32 値。 **ResumeService**要求が受け入れられた場合は0、要求がサポートされていない場合は1、エラーを示すその他の数値。  
  
## <a name="remarks"></a>解説  
  
## <a name="see-also"></a>参照  
 [サービスの開始と停止](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
