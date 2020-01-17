---
title: SQL Server 中央管理サーバーの拡張機能
titleSuffix: Azure Data Studio
description: Azure Data Studio 用の SQL Server 中央管理サーバーの拡張機能 (プレビュー) をインストールして使用する
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.custom: seodec18
ms.date: 06/06/2019
ms.openlocfilehash: 6c323c2580e86e560aa1b0df5d131b260d0c1bb5
ms.sourcegitcommit: 39ea690996a7390e3d13d6fb8f39d8641cd5f710
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74957026"
---
# <a name="sql-server-central-management-servers-extension-preview"></a>SQL Server 中央管理サーバーの拡張機能 (プレビュー)

中央管理サーバーの拡張機能を使用すると、ユーザーは 1 つまたは複数のグループに編成された SQL Server のインスタンスの一覧を格納できます。 CMS グループを使用して実行されるアクションは、サーバー グループ内のすべてのサーバーで動作します。

このエクスペリエンスは、現在、初期のプレビュー段階にあります。 問題の報告や機能の要求を行うには、[ここ](https://github.com/microsoft/azuredatastudio/issues)にアクセスしてください。

![CMS の拡張機能](media/sql-server-cms-extension/cms-list.png)

## <a name="install-the-sql-server-central-management-servers-extension"></a>SQL Server 中央管理サーバーの拡張機能をインストールする

1. 拡張機能マネージャーを開いて、使用可能な拡張機能にアクセスするには、拡張機能アイコンを選択するか、 **[表示]** メニューの **[拡張機能]** を選択します。
2. 使用可能な拡張機能を選択すると、その詳細が表示されます。
1. 必要な拡張機能 (SQL Server 中央管理サーバー) を選択して**インストール**します。

### <a name="how-do-i-start-central-management-servers"></a>中央管理サーバーを起動する方法
 中央管理サーバーを表示するには、[接続] アイコン (Ctrl/Cmd + G) をクリックします。 拡張機能を初めてダウンロードすると、CMS ビューは最小化されます。これを開くには、 **[中央管理サーバー]** をクリックします

## <a name="next-steps"></a>次のステップ
中央管理サーバーの概念の詳細については、[こちら](https://docs.microsoft.com/sql/ssms/register-servers/create-a-central-management-server-and-server-group)を参照してください。


