---
title: IServerVirtualDeviceSet2::Close
titlesuffix: SQL Server VDI reference
description: この記事では、IServerVirtualDeviceSet2::Close コマンドのリファレンスを提供します。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 2847ef10bd52d69375fa4f13f1d003eb4159961f
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847473"
---
# <a name="iservervirtualdeviceset2close-vdi"></a>IServerVirtualDeviceSet2::Close (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**Close** 関数は、IServerVirtualDeviceSet2::Open によって開かれた仮想デバイス セットを閉じます。 これにより、仮想デバイスに関連付けられているすべてのリソースが解放されます。 IServerVirtualDeviceSet2 ハンドルは、この関数が戻った後は役に立たず、COM に返す必要があります。

## <a name="syntax"></a>構文

```c
HRESULT IServerVirtualDeviceSet2::Close ();
```

## <a name="return-value"></a>戻り値

|戻り値 | 説明 |
|---|---|
| VD_E_PROTOCOL | デバイスがまだ開いたままでした。 |

## <a name="remarks"></a>Remarks

デバイスを閉じる前に仮想デバイス セットを閉じないでください。 このような状況が発生した場合は、VD_E_PROTOCOL が返されます。 このアクションを実行すると、Close で共有メモリのマッピングがすぐに解放されます。 サーバーで仮想デバイス インターフェイスから返されたリソースの所有権が引き続き要求される場合、サーバーがアクセス違反となる可能性があります。 インターフェイスで、SignalAbort 処理が実行されます。

完了エージェントは、実行されている場合、未処理のコマンドを完了してから呼び出し元に戻ります。 未処理のコマンドはすべて、ERROR_OPERATION_ABORTED を使用して完了されます。 つまり、このようなコマンドごとにコールバック関数が呼び出されます。

エラーが返された場合を含め、いずれの場合も、Close により仮想デバイス インターフェイスのすべてのリソースが解放されます。 VDI から返されたすべてのバッファーとその他のインターフェイス ポインターは無効になります。

COM ライブラリがアンロードされる前に、完了エージェントを確実に終了させることが重要です。 完了エージェントが呼び出し元に戻される前にライブラリがアンロードされた場合、そのプロセスで命令違反が発生する可能性があります。

## <a name="next-steps"></a>次の手順

詳細については、[SQL Server 仮想デバイス インターフェイス リファレンスの概要](reference-virtual-device-interface.md)に関するページを参照してください。