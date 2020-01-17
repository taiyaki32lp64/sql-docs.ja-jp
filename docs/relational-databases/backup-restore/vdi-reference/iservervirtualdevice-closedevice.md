---
title: IServerVirtualDevice::CloseDevice
titlesuffix: SQL Server VDI reference
description: この記事では、IServerVirtualDevice::CloseDevice コマンドのリファレンスを提供します。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: c73649e2a4301e94f8e68504222cc0122061f25f
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847433"
---
# <a name="iservervirtualdeviceclosedevice-vdi"></a>IServerVirtualDevice::CloseDevice (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**CloseDevice** 関数は、IServerVirtualDeviceSet2::OpenDevice で開かれた仮想デバイスを閉じます。

## <a name="syntax"></a>構文

```c
HRESULT IServerVirtualDevice::CloseDevice ();
```

## <a name="return-value"></a>戻り値

|戻り値 | 説明 |
|---|---|
| VD_E_CLOSE | デバイスは既に閉じられています。 |
| VD_E_ABORT | インターフェイスは中止状態です。 |

## <a name="remarks"></a>Remarks

異常終了を強制するために SignalAbort を使用すると、CloseDevice は不要になります。 SignalAbort が使用された後に CloseDevice が呼び出された場合、何のアクションも実行されません。

## <a name="next-steps"></a>次の手順

詳細については、[SQL Server 仮想デバイス インターフェイス リファレンスの概要](reference-virtual-device-interface.md)に関するページを参照してください。