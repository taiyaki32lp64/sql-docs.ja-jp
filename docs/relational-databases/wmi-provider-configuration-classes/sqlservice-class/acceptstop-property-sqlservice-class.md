---
title: AcceptStop プロパティ (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- AcceptStop Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
helpviewer_keywords:
- AcceptStop property
ms.assetid: bf8ffe79-4f4c-4a2d-82e5-2ae8f5d466c5
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 956151208b93a848219cdac2d897f132511e411d
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73659810"
---
# <a name="acceptstop-property-sqlservice-class"></a>AcceptStop プロパティ (SqlService クラス)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  サービスを停止できるかどうかを指定するブール型のプロパティの値を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.AcceptStop [= value]  
```  
  
## <a name="parts"></a>要素  
 *object*  
 サービスを表す[Sqlservice クラス](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md)オブジェクト  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 サービスを停止できるかどうかを指定するブール値。サービスを停止できる場合は**true** 、サービスを停止できない場合は**false**を指定します。  
  
## <a name="remarks"></a>解説  
  
## <a name="see-also"></a>参照  
 [サービスの開始と停止](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
