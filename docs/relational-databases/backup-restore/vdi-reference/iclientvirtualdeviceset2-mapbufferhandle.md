---
title: IClientVirtualDeviceSet2::MapBufferHandle
titlesuffix: SQL Server VDI reference
description: この記事では、IClientVirtualDeviceSet2::MapBufferHandle コマンドについて説明します。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 5d181d1b6ddfea034716ebb048768cd7d43fbc61
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847583"
---
# <a name="iclientvirtualdeviceset2mapbufferhandle-vdi"></a>IClientVirtualDeviceSet2::MapBufferHandle (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**MapBufferHandle** 関数は、他のプロセスから取得したバッファー ハンドルから有効なバッファー アドレスを取得するために使用されます。

## <a name="syntax"></a>構文

```c
HRESULT IClientVirtualDeviceSet2::MapBufferHandle (
   DWORD      dwBuffer,
   BYTE**      ppBuffer
);
```

## <a name="parameters"></a>パラメーター

*dwBuffer* これは、IClientVirtualDeviceSet2::GetBufferHandle から返されるハンドルです。

*ppBuffer* これは、現在のプロセスで有効なバッファーのアドレスです。

## <a name="return-value"></a>戻り値

|戻り値 | 説明 |
|---|---|
| NOERROR | 関数が正常に実行されました。 |
| VD_E_PROTOCOL | 仮想デバイス セットは現在開いていません。 |
| VD_E_INVALID | ppBuffer は無効なハンドルです。 |

## <a name="remarks"></a>Remarks

ハンドルが正しく通信されるように注意する必要があります。 ハンドルは、1 つの仮想デバイス セットに対してローカルです。 ハンドルを共有するパートナーでは、バッファー ハンドルが、最初に取得された仮想デバイス セットのスコープ内でのみ使用されていることを確認する必要があります。

## <a name="next-steps"></a>次の手順

詳細については、[SQL Server 仮想デバイス インターフェイス リファレンスの概要](reference-virtual-device-interface.md)に関するページを参照してください。