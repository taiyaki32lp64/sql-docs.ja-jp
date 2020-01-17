---
title: SSMS XEvent Profiler の使用
ms.date: 10/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: genemi
ms.technology: xevents
ms.topic: tutorial
helpviewer_keywords:
- extended events [SQL Server], system health session
- extended events [SQL Server], system_health session
- system_health session [SQL Server extended events]
- system health session [SQL Server extended events]
ms.assetid: 1e1fad43-d747-4775-ac0d-c50648e56d78
author: yualan
ms.author: alayu
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6b500713053e8ea65722a10e2bf93ec566d9fbdd
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75251407"
---
# <a name="use-the-ssms-xevent-profiler"></a>SSMS XEvent Profiler の使用

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
XEvent Profiler は、拡張イベントのライブ ビューアー ウィンドウを表示する SQL Server Management Studio (SSMS) 機能です。 この概要では、このプロファイラーを使用する理由、主な機能、拡張イベントを初めて表示する場合の手順について説明します。

## <a name="why-would-i-use-the-xevent-profiler"></a>XEvent Profiler を使用する理由
SQL Profiler とは異なり、XEvent Profiler は SSMS に直接統合され、SQL エンジンのスケーラブルな拡張イベント テクノロジ上に構築されています。 この機能を使用すると、SQL Server の診断イベントのライブ ストリーミング ビューにすばやくアクセスできます。 このビューはカスタマイズできます。また、.viewsettings ファイルとして他の SSMS ユーザーと共有することができます。 XE プロファイラーで作成されたセッションは、SQL Profiler を使用した場合の同様の SQL トレースよりも、実行中の SQL Server に対する影響が少なくなります。 このセッションはユーザーがカスタマイズできますが、既存の XE セッションのプロパティの UI または TSQL を使用してカスタマイズすることもできます。

## <a name="prerequisites"></a>前提条件
この機能は、SQL Server Management Studio (SSMS) v17.3 以降でのみ使用できます。 最新バージョンを使用していることを確認してください。 最新バージョンは[こちら](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)で入手できます。

## <a id="getting-started"></a>はじめに
XEvent Profiler にアクセスするには、次の手順を実行します。

1. **SQL Server Management Studio** を開きます。

2. SQL Server Database Engine または localhost のインスタンスに接続します。

3. オブジェクト エクスプローラーで、XE プロファイラー メニュー項目を見つけて、[+] 記号をクリックして展開します。

   ![XEProfiler メニュー](media/xevents-xe-profiler-menu.png)

4. このセッションのすべての拡張イベントを表示する場合は、 **[標準]** をダブルクリックします。 ログに記録されている SQL ステートメントを表示する場合は、 **[T-SQL]** をクリックします。 セッションがまだ作成されていない場合は、セッションが自動的に作成されます。

   ![XEProfiler セッション](media/xevents-xe-profiler-start-session.png)

5. これで拡張イベントが表示されるようになります。

   ![XEProfiler ビューアー](media/xevents-xe-profiler-start-viewer.png)

## <a name="see-also"></a>参照
[拡張イベント](../../relational-databases/extended-events/extended-events.md)  
[拡張イベントのツール](../../relational-databases/extended-events/extended-events-tools.md)  
  
  
