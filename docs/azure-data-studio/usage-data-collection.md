---
title: 使用状況データ コレクションとクラッシュ レポートを有効または無効にする
titleSuffix: Azure Data Studio
description: この記事では、使用状況とクラッシュ レポートのデータが収集されて Microsoft に送信されるかどうかを制御する方法について説明します。
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18; seo-lt-2019
ms.date: 09/24/2018
ms.openlocfilehash: 416c22aa04e289e7959e41924344666e4329ecf1
ms.sourcegitcommit: 39ea690996a7390e3d13d6fb8f39d8641cd5f710
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74957006"
---
# <a name="enable-or-disable-usage-data-collection-for-includename-sosincludesname-sos-shortmd"></a>[!INCLUDE[name-sos](../includes/name-sos-short.md)] のデータ コレクションを有効または無効にする

## <a name="how-to-disable-telemetry-reporting"></a>テレメトリ レポートを無効にする方法

[!INCLUDE[name-sos](../includes/name-sos-short.md)] では、使用状況データが収集されて Microsoft に送信され、製品やサービスの改善に役立てられます。 詳細については、[プライバシーに関する声明](https://go.microsoft.com/fwlink/?LinkID=528096&clcid=0x409)をお読みください。

使用状況データを Microsoft に送信したくない場合は、*telemetry.enableTelemetry* 設定を *false* に設定できます。

[!INCLUDE[name-sos](../includes/name-sos-short.md)] からのすべてのテレメトリ イベントをサイレント状態にするには、 **[ファイル]**  >  **[基本設定]**  >  **[設定]** で、次のオプションを追加します。

```json
    "telemetry.enableTelemetry": false
```

**重要な注意**: このオプションを有効にするには、[!INCLUDE[name-sos](../includes/name-sos-short.md)] の再起動が必要です。 

## <a name="how-to-disable-crash-reporting"></a>クラッシュ レポートを無効にする方法

クラッシュ レポートを無効にするには、 **[ファイル]**  >  **[基本設定]**  >  **[設定]** で、次のオプションを追加します。

```json
    "telemetry.enableCrashReporter": false
```

**重要な注意**: このオプションを有効にするには、[!INCLUDE[name-sos](../includes/name-sos-short.md)] の再起動が必要です。

## <a name="additional-resources"></a>その他のリソース
- [ワークスペースとユーザー設定](settings.md)
