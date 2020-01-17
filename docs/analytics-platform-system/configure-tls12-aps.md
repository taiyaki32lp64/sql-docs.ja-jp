---
title: TLS 1.2 の構成
description: APS で TLS 1.2 を構成するための推奨事項
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 10/29/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 988cac765a596b541d128b0b6190f6f228d95ee7
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401253"
---
# <a name="configure-tls-12-in-aps"></a>APS で TLS 1.2 を構成する

TLS 1.2 のみを使用するように AP をセキュリティで保護するには、すべての物理ホストと仮想ホストで他のプロトコルを明示的に無効にする必要があります。 プロトコルを無効にするには、レジストリ設定の変更が必要です。 レジストリを変更するには、仮想ホストと物理ホストを再起動する必要があります。

> [!WARNING]
> ここでは、レジストリの変更方法を示す手順について説明します。 ただし、データの損失を引き起こす可能性があり、オペレーティングシステムの再インストールが必要になる可能性があるレジストリを誤って変更すると、深刻な問題が発生する可能性があります。 レジストリを変更する前に、バックアップしておくことを強くお勧めします。 バックアップがあれば、問題が発生してもレジストリを復元できます。 レジストリをバックアップおよび復元する方法の詳細については、次の記事番号をクリックして、Microsoft サポート技術情報の記事を参照してください。<br>
[322756](https://support.microsoft.com/help/322756) Windows でレジストリをバックアップおよび復元する方法

**切り替える**
```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0]
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client]
"Enabled"=dword:00000000
"DisabledByDefault"=dword:00000001
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server]
"Enabled"=dword:00000000
"DisabledByDefault"=dword:00000001
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1]
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client]
"Enabled"=dword:00000000
"DisabledByDefault"=dword:00000001
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server]
"Enabled"=dword:00000000
"DisabledByDefault"=dword:00000001
```

また、APS SSIS 変換先アダプターなどのツールがインストールされているクライアントコンピューターに、次のキーを設定します。
```
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]
"SystemDefaultTlsVersions"=dword:00000001
"SchUseStrongCrypto"=dword:00000001

[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319]
"SystemDefaultTlsVersions"=dword:00000001
"SchUseStrongCrypto"=dword:00000001 
```



