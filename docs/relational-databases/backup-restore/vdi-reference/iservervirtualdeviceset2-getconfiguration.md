---
title: IServerVirtualDeviceSet2::GetConfiguration
titlesuffix: SQL Server VDI reference
description: この記事では、IServerVirtualDeviceSet2::GetConfiguration コマンドのリファレンスを提供します。
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 1d62a2042221bebf04e19a46a21ba81caa7c877b
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847253"
---
# <a name="iservervirtualdeviceset2getconfiguration-vdi"></a>IServerVirtualDeviceSet2::GetConfiguration (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**GetConfiguration** 関数は、クライアントによって要求された構成を取得します。

## <a name="syntax"></a>構文

```c
HRESULT IServerVirtualDeviceSet2::GetConfiguration (
   VDConfig*   pCfg
);
```

## <a name="parameters"></a>パラメーター

*pCfg*: これは、IClientVirtualDeviceSet2::Create を使用してクライアントによって指定された構成です。

## <a name="return-value"></a>戻り値

メソッド呼び出しの成功または失敗を示す *HRESULT* を返します。 値 NOERROR は、メソッド呼び出しが成功したことを示します。 0 以外の値は、エラーが発生したことを示します。

## <a name="remarks"></a>Remarks

サーバーには、クライアントによって提供される設定を検査して応答することが求められます。 詳細については、「構成」に関する記事を参照してください。 サーバーが指定された構成で正しく動作できないと判断されると、そのサーバーで SignalAbort を使用できます。

## <a name="next-steps"></a>次の手順

詳細については、[SQL Server 仮想デバイス インターフェイス リファレンスの概要](reference-virtual-device-interface.md)に関するページを参照してください。