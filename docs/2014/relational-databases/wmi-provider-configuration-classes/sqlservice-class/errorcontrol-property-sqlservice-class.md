---
title: ErrorControl プロパティ (SqlService クラス) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- ErrorControl Property (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- ErrorControl property
ms.assetid: cbb1e0fa-5bfc-4b1b-a6ed-f7d5cfad4d73
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 89cdfa63bff88c4f4bb5954402034b31ad7f77ce
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63060987"
---
# <a name="errorcontrol-property-sqlservice-class"></a>ErrorControl プロパティ (SqlService クラス)
  起動時にサービスを開始できなかった場合のエラーの重大度を取得または設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object  
.ErrorControl [= value]  
```  
  
## <a name="parts"></a>要素  
 *object*  
 サービスを表す [SqlService クラス](sqlservice-class.md) オブジェクト。  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 起動時にサービスが失敗した場合にレポートされるエラーの重大度を指定する文字列値。 次の表では、使用可能な値を示します。  
  
 Ignore  
 ユーザーへの通知が行われません。  
  
 標準  
 ユーザーへの通知が行われます。  
  
 重大  
 システムは最後の正しい構成で再起動されます。  
  
 重大  
 正しい構成でシステムの再起動が試行されます。  
  
 Unknown  
 重大度が不明です。  
  
## <a name="remarks"></a>コメント  
 値は、失敗が発生した場合に、起動プログラムによって行われるアクションを示しています。 すべてのエラーは、コンピューター システムによって記録されます。  
  
## <a name="see-also"></a>参照  
 [開始とサービスの停止](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
