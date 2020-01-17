---
title: SetDefaults メソッド (ClientSettings)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetDefaults Method (ClientSettings Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetDefaults method
ms.assetid: 056508f3-a5c8-467c-a196-dc1ef1f5178f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ac698d7fa655e47459b9de3af0f5896e038c0c0c
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73657637"
---
# <a name="clientsettings-class---setdefaults-method"></a>ClientSettings クラス - SetDefaults メソッド
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  既存のデータを上書きするオプションを使用して、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クライアントのインスタンスのすべての既定値を設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
object.SetDefaults(OverwriteAll)  
```  
  
## <a name="parts"></a>要素  
 *object*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クライアントインスタンスを表す**Clientsettings**オブジェクト。  
  
#### <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|---------------|-----------------|  
|*OverwriteAll*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クライアントのインスタンス上の既存の値を上書きするかどうかを指定するブール値。 既存のデータを上書きする**場合は true** 。既存のデータを上書きしない場合は**false** 。|  
  
## <a name="property-valuereturn-value"></a>プロパティ値/戻り値  
 **uint32** 値。サービスが正常に変更された場合は 0、要求がサポートされていない場合は 1 になります。それ以外の数値はエラーを示します。  
  
## <a name="remarks"></a>解説  
  
