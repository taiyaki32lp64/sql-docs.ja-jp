---
title: IServerVirtualDeviceSet2::IsSharedBuffer
titlesuffix: SQL Server VDI reference
description: この記事では、IServerVirtualDeviceSet2::IsSharedBuffer コマンドのリファレンスを提供します。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: cd3e7abfd1d250a170e0de4ebc1b392bc5857468
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847363"
---
# <a name="iservervirtualdeviceset2issharedbuffer-vdi"></a>IServerVirtualDeviceSet2::IsSharedBuffer (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**IsSharedBuffer** 関数は、指定されたバッファー アドレスが、AllocateBuffer メソッドで使用可能な共有バッファーのいずれかを参照しているかどうかを判断します。

## <a name="syntax"></a>構文

```c
HRESULT IServerVirtualDeviceSet2::IsSharedBuffer (
   LPVOID   lpBuffer
);
```

## <a name="parameters"></a>パラメーター

*lpBuffer*: これはバッファーのアドレスです。

## <a name="return-value"></a>戻り値

|戻り値 | 説明 |
|---|---|
| TRUE | バッファーは共有バッファーです。 |
| FALSE | バッファーは仮想デバイス セットの一部ではありません。 |

## <a name="next-steps"></a>次の手順

詳細については、[SQL Server 仮想デバイス インターフェイス リファレンスの概要](reference-virtual-device-interface.md)に関するページを参照してください。