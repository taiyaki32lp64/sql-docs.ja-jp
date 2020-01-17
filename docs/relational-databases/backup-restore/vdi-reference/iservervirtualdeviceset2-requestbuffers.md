---
title: IServerVirtualDeviceSet2::RequestBuffers
titlesuffix: SQL Server VDI reference
description: この記事では、IServerVirtualDeviceSet2::RequestBuffers コマンドのリファレンスを提供します。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 1b941f251c9093f10abbced8c3522f1719a1580e
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847183"
---
# <a name="iservervirtualdeviceset2requestbuffers-vdi"></a>IServerVirtualDeviceSet2::RequestBuffers (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**RequestBuffers** 関数は、指定されたサイズと配置要件を持つ特定の数のバッファーがサーバーに必要であることを VDI に通知します。

## <a name="syntax"></a>構文

```c
HRESULT IServerVirtualDeviceSet2::RequestBuffers (
   DWORD   dwSize,
   DWORD   dwAlignment,
   DWORD   dwCount
);
```

## <a name="parameters"></a>パラメーター

*dwSize*: 各バッファーのサイズを識別します。 このサイズには、データに必要なリージョンだけを含める必要があります。 VDI によって、すべての配置とプレフィックスの要件が処理されます。

*dwAlignment*: これらのバッファーに必要な配置です。 'BeginConfiguration' で指定された基本の配置の値よりも制限の厳しい値が使用されている可能性があります。 値が 0 の場合、既定値の基本の配置の値になります。

*dwCount*: 指定されたサイズと配置で 'AllocateBuffer' によって要求されるバッファーの数です。

## <a name="return-value"></a>戻り値

|戻り値 | 説明 |
|---|---|
| NOERROR | 関数が正常に実行されました。 |
| VD_E_ABORT | 中止が要求されました。 |
| VD_E_PROTOCOL | このセットは、バッファー割り当てを宣言できる状態ではありません (状態遷移マトリックスを参照)。 |
| VD_E_MEMORY | 要求されたメモリを取得できませんでした。 |

## <a name="remarks"></a>Remarks

このメソッドは、AllocateBuffer でバッファーが割り当てられる前に使用する必要があります。 RequestBuffers で、指定されたサイズとアラインメントを持つバッファーのセットが要求された後、AllocateBuffer で個々のバッファーが割り当てられます。

構成フェーズでは、EndConfiguration 呼び出し時に (その時点で割り当てられる) 1 つのバッファー領域を使用できるように、RequestBuffers の呼び出しが "合計" されます。 構成が完了すると、任意の RequestBuffers の呼び出しで、より多くのバッファー領域が即座に割り当てられるようになります。

## <a name="next-steps"></a>次の手順

詳細については、[SQL Server 仮想デバイス インターフェイス リファレンスの概要](reference-virtual-device-interface.md)に関するページを参照してください。