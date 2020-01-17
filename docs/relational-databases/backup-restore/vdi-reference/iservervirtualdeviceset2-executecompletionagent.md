---
title: IServerVirtualDeviceSet2::ExecuteCompletionAgent
titlesuffix: SQL Server VDI reference
description: この記事では、IServerVirtualDeviceSet2::ExecuteCompletionAgent コマンドのリファレンスを提供します。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 2ad094794b5115aa4593f918de442798445e2b79
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847293"
---
# <a name="iservervirtualdeviceset2executecompletionagent-vdi"></a>IServerVirtualDeviceSet2::ExecuteCompletionAgent (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**ExecuteCompletionAgent** 関数は、完了エージェントのメイン ループを実装するために使用されます。

## <a name="syntax"></a>構文

```c
HRESULT IServerVirtualDeviceSet2::ExecuteCompletionAgent ();
```

## <a name="return-value"></a>戻り値

メソッド呼び出しの成功または失敗を示す *HRESULT* を返します。 値 NOERROR は、メソッド呼び出しが成功したことを示します。 0 以外の値は、エラーが発生したことを示します。

## <a name="remarks"></a>Remarks

完了エージェントによって、SQL Server が自身を仮想デバイスのコマンド完了と同期できるメカニズムが提供されます。 これは任意のコマンドを発行する前にアクティブにしておく必要があり、すべてのデバイスが閉じられるまでアクティブなままにしておく必要があります。

場合によっては SQL Server で特殊なスレッドの初期化を実行する必要があるため、このインターフェイスによって新しい制御スレッドが開始されることはありません。 代わりに、SQL Server でスレッドが設定されてから、このルーチンにコントロールが渡されます。 スレッドは、Windows NT プロセス間通信 (IPC) メカニズムでブロックでき、IServerVirtualDevice::SendCommand を介して送信されたコマンドで提供される任意のコールバック関数を呼び出せる必要があります。

この関数は、IServerVirtualDeviceSet2::Close または SignalAbort が呼び出されるまで戻りません。

## <a name="next-steps"></a>次の手順

詳細については、[SQL Server 仮想デバイス インターフェイス リファレンスの概要](reference-virtual-device-interface.md)に関するページを参照してください。