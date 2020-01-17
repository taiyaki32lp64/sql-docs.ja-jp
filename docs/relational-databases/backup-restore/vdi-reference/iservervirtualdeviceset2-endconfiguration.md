---
title: IServerVirtualDeviceSet2::EndConfiguration
titlesuffix: SQL Server VDI reference
description: この記事では、IServerVirtualDeviceSet2::EndConfiguration コマンドのリファレンスを提供します。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 5060a862f61f005c83296235bcef5a2851bcaeca
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847303"
---
# <a name="iservervirtualdeviceset2endconfiguration-vdi"></a>IServerVirtualDeviceSet2::EndConfiguration (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**EndConfiguration** 関数は、サーバーの構成が完了したことを VDI に通知します。

## <a name="syntax"></a>構文

```c
HRESULT IServerVirtualDeviceSet2::EndConfiguration ();
```

## <a name="return-value"></a>戻り値

|戻り値 | 説明 |
|---|---|
| NOERROR | 関数が正常に実行されました。 |
| VD_E_ABORT | 中止が要求されました。 |
| VD_E_PROTOCOL | セットは構成可能な状態ではありません。 |
| VD_E_MEMORY | 'RequestBuffers' 呼び出しを介して必要なメモリを取得できませんでした。 このセットは、使用可能なバッファー領域がない構成可能な状態のままになります。 サーバーでは、バッファー要件の削減、または操作の中止のいずれかを行えます。 |

## <a name="next-steps"></a>次の手順

詳細については、[SQL Server 仮想デバイス インターフェイス リファレンスの概要](reference-virtual-device-interface.md)に関するページを参照してください。