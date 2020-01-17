---
title: 透過的なネットワーク IP 解決を使用する |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d255208f-d486-4ad3-8080-61c6e0261825
author: MightyPen
ms.author: genemi
ms.openlocfilehash: df5b0233168c52b4f79cdc6d2d03cd7b72e16046
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008477"
---
# <a name="using-transparent-network-ip-resolution"></a>透過的なネットワーク IP の解決の使用
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

TransparentNetworkIPResolution は、Microsoft ODBC Driver 13.1 for SQL Server で利用可能な既存の MultiSubnetFailover 機能のリビジョンであり、ホスト名の最初に解決された IP が使用できない場合のドライバーの接続シーケンスに影響します。応答し、ホスト名に複数の Ip が関連付けられています。 MultiSubnetFailover と対話して、次の3つの接続シーケンスを提供します。

* 0: 1 つの IP が試行され、その後にすべての ip が並列で含まれます。
* 1: すべての Ip が並列で試行されます
* 2: すべての Ip が1回試行されます

|TransparentNetworkIPResolution|MultiSubnetFailover|現象|
|:-:|:-:|:-:|
|(既定値)。|(既定値)。|0|
|(既定値)。|有効|1|
|(既定値)。|Disabled|0|
|有効|(既定値)。|0|
|有効|有効|1|
|有効|Disabled|0|
|Disabled|(既定値)。|2|
|Disabled|有効|1|
|Disabled|Disabled|2|

接続`TransparentNetworkIPResolution`文字列と DSN キーワードは、この設定を接続文字列レベルで制御します。 既定値は有効です。

Keyword|値|既定
-|-|-
`TransparentNetworkIPResolution`|`Yes`, `No`|`Yes`

事前`SQL_COPT_SS_TNIR`接続属性を使用すると、アプリケーションでこの設定をプログラムによって制御できます。

接続属性|   サイズ/型|  既定| [値]| [説明]
-|-|-|-|-
`SQL_COPT_SS_TNIR` (1249)| `SQL_IS_INTEGER` または `SQL_IS_UINTEGER`| `SQL_IS_ON`(1)、`SQL_IS_OFF`(0)|`SQL_IS_ON`|TNIR を有効または無効にします。

<a name="for-more-information-about-multisubnetfailover-see-odbc-driver-on-linux-and-macos---high-availability-and-disaster-recoveryconnectodbclinux-macodbc-driver-on-linux-support-for-high-availability-disaster-recoverymd"></a>MultiSubnetFailover の詳細については、「 [Linux および macOS の ODBC ドライバー-高可用性とディザスターリカバリー](../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md) 」を参照してください。
--------------------------------------------------
## <a name="see-also"></a>参照  
* [Microsoft ODBC Driver for SQL Server on Windows](../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
* [SQL Server マルチサブネット クラスタリング (SQL Server)](https://msdn.microsoft.com/library/ff878716.aspx#RelatedContent)
