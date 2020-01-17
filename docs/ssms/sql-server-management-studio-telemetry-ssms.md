---
title: SQL Server Management Studio - 使用状況および診断データ (SSMS) | Microsoft Docs
ms.custom: ''
ms.date: 04/16/2019
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: c28ffa44-7b8b-4efa-b755-c7a3b1c11ce4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 82b4af04963c5161cbea300054d19c61b61ec34a
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028817"
---
# <a name="local-audit-for-ssms-usage-and-diagnostic-data-collection"></a>SSMS の使用状況および診断データの収集のローカル監査
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

SQL Server Management Studio (SSMS) には、機能使用状況および診断データを匿名で収集して Microsoft に送信する、インターネット対応機能が含まれています。 SSMS は、標準的なコンピューター情報、および使用とパフォーマンスに関する情報を収集する場合があります。これらの情報は Microsoft に送信され、SSMS の品質、セキュリティ、および信頼性を向上させる目的で分析されます。 お客様の名前、住所などの連絡先情報は収集されません。 詳細については、「[Microsoft プライバシーに関する声明](https://privacy.microsoft.com/privacystatement)」と「[SQL Server のプライバシーの補足情報](https://go.microsoft.com/fwlink/?LinkID=868444)」を参照してください。

## <a name="audit-feature-usage-and-diagnostic-data"></a>監査機能の使用状況および診断データ

SSMS で収集される機能の使用状況データを表示するには、次の手順を実行します。

1.  SSMS を起動します。
2.  メインメニューで **[表示]** 、 **[出力]** の順にクリックし、 **[出力]** ウィンドウを表示します。 
3.  **[出力]** ウィンドウが表示されたら、 **[出力元の表示:]** メニューで **[テレメトリ]** を選択します。

SSMS を使用してデータベースと対話している間に、収集されたデータが **[出力]** ウィンドウに表示されます。

## <a name="enable-or-disable-usage-and-diagnostic-data-collection-in-ssms"></a>SSMS の使用状況および診断データの収集を有効または無効にする

SSMS の使用状況データの収集をオプトインまたはオプトアウトするには:

- SQL Server Management Studio 17 の場合:

  `Subkey = HKEY_CURRENT_USER\Software\Microsoft\SQL Server Management Studio\14.0`

  レジストリ エントリ名 = `UserFeedbackOptIn`

  エントリの種類 `DWORD`: `0` はオプトアウトです。`1` はオプトインです。

  また、SSMS 17.x は Visual Studio 2015 シェルを基盤とし、Visual Studio インストールによって、既定でカスタマー フィードバックが可能になります。  

  個々のコンピューターでカスタマー フィードバックを無効にするように Visual Studio を構成するには、次のレジストリ サブキーの値を文字列 `0`: `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\VisualStudio\SQM OptIn` に変更します。

  たとえば、次のサブキーを変更します。  
  `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\VisualStudio\SQM OptIn `=` 0`

  これらのレジストリ サブキーのレジストリに基づくグループ ポリシーは、SQL Server 2017 の使用状況および診断データ収集で受け入れられます。

- SQL Server Management Studio 18 の場合:

  `Subkey = HKEY_CURRENT_USER\Software\Microsoft\SQL Server Management Studio\18.0_IsoShell`

  レジストリ エントリ名 = `UserFeedbackOptIn`

  エントリの種類 `DWORD`: `0` はオプトアウトです。`1` はオプトインです。

## <a name="see-also"></a>参照

- [Configure usage and diagnostic data collection for SQL Server (SQL Server の使用状況および診断データの収集を構成する)](../sql-server/usage-and-diagnostic-data-configuration-for-sql-server.md)
- [SQL Server の使用状況と診断データの収集のローカル監査](https://msdn.microsoft.com/library/mt743085.aspx)