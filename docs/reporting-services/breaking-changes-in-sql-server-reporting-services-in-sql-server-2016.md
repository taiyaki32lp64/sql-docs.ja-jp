---
title: SQL Server 2016 における SQL Server Reporting Services の重大な変更 | Microsoft Docs
ms.date: 07/02/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- Me.Value references
- Reporting Services, backward compatibility
- breaking changes [Reporting Services]
ms.assetid: 39c7aafd-dcb9-4317-b8f7-d15828eb4f9a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 41aad02f9f5b65dd1cf1474abd0c152f3face8c0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65503955"
---
# <a name="breaking-changes-in-sql-server-reporting-services-in-sql-server-2016"></a>SQL Server 2016 における SQL Server Reporting Services の重大な変更

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016](../includes/ssrs-appliesto-2016.md)] [!INCLUDE [ssrs-appliesto-not-2017](../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../includes/ssrs-previous-versions.md)]

このトピックでは、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]における重大な変更について説明します。 これらの変更によって、以前のバージョンの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]に基づくアプリケーション、スクリプト、または機能が使用できなくなる場合があります。 この問題は、アップグレードするとき、またはカスタムのスクリプトやレポートで発生することがあります。

## <a name="security-extensions"></a>セキュリティ拡張機能

カスタム セキュリティ拡張機能が新しい [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]で動作するには、いくつかの変更が必要です。 セキュリティ拡張機能は、IAuthenticationExtension2 インターフェイスを使用する必要があります。

## <a name="wmi-provider"></a>WMI プロバイダー

[!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] アプリケーション名は "ReportManager" から "ReportServerWebApp" へと変更されます。

## <a name="next-steps"></a>次の手順

[SQL Server 2016 における SQL Server Reporting Services の動作変更](../reporting-services/behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)  
[Reporting Services (SSRS) の新機能](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)   
[SQL Server 2016 における SQL Server Reporting Services の非推奨の機能](../reporting-services/deprecated-features-in-sql-server-reporting-services-ssrs.md)    
[SQL Server Reporting Services SQL Server 2016 で廃止された機能](../reporting-services/discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)  

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
