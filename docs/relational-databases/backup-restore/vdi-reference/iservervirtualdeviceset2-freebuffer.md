---
title: IServerVirtualDeviceSet2::FreeBuffer
titlesuffix: SQL Server VDI reference
description: この記事では、IServerVirtualDeviceSet2::FreeBuffer コマンドのリファレンスを提供します。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 2829f849ce8cd220fdabc75a0d2059c5da0c80fd
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847263"
---
# <a name="iservervirtualdeviceset2freebuffer-vdi"></a>IServerVirtualDeviceSet2::FreeBuffer (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**FreeBuffer** 関数は、仮想デバイス セットから共有メモリ バッファーを取得します。

## <a name="syntax"></a>構文

```c
HRESULT IServerVirtualDeviceSet2::FreeBuffer (
   LPVOID   pBuffer,
   UINT32   dwSize
);
```

## <a name="parameters"></a>パラメーター

*pBuffer*: これは、IServerVirtualDeviceSet2::AllocateBuffer によって返されるバッファーを返します。

*dwSize*: これは、バッファーのサイズを取得します (バイト単位)。 これには、クライアントによって要求されたプレフィックス ゾーンは含まれません。 このようなゾーンはサーバーに表示されず、バッファー アドレスが返される前に使用可能な領域があります。

## <a name="return-value"></a>戻り値

|戻り値 | 説明 |
|---|---|
| NOERROR | バッファーが返されます。 |
| VD_E_INVALID | パラメーターが無効でした。 |

## <a name="next-steps"></a>次の手順

詳細については、[SQL Server 仮想デバイス インターフェイス リファレンスの概要](reference-virtual-device-interface.md)に関するページを参照してください。