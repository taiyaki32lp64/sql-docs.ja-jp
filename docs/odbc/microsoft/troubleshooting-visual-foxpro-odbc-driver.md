---
title: トラブルシューティング (Visual FoxPro ODBC ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set ANSI [ODBC]
- troubleshooting Visual FoxPro ODBC driver [ODBC]
- remote views [ODBC]
- multitiered views [ODBC]
- parameterized views [ODBC], Visual FoxPro ODBC driver
- fetches [ODBC], Visual FoxPro ODBC driver
- positioned updates [ODBC]
- background fetching [ODBC]
ms.assetid: fd478dd8-666a-4f0a-a2d6-b94e81cbbe4b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4eeb6210b9bce124e16a1b4e666dee03c1d992be
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67912380"
---
# <a name="troubleshooting-visual-foxpro-odbc-driver"></a>トラブルシューティング (Visual FoxPro ODBC ドライバー)
次のセクションでは、パフォーマンスが向上し、Visual FoxPro ODBC ドライバーを使用しているときに発生する可能性の問題を解決する方法について説明します。  
  
## <a name="accessing-parameterized-views"></a>パラメーター化されたビューへのアクセス  
 ドライバーを使用して Visual FoxPro データベースでパラメーター化されたビューにアクセスすることはできません。 パラメーター化されたビュー、ビューの SQL の WHERE 句を作成する**選択**レコードを制限するステートメントがパラメーターに指定された値を使用して構築された WHERE 句の条件を満たすレコードにダウンロードします。 ドライバーがビューに渡すパラメーターをサポートしていないため、ドライバーを使用してパラメーター化されたビューのアクセスの試みは失敗します。  
  
 パラメーターの値は、実行時に指定またはビューに渡すプログラムでできます。  
  
## <a name="accessing-remote-views"></a>リモート ビューへのアクセス  
 ドライバーを使用して Visual FoxPro データベース内のリモートのビューにアクセスできません。 リモートのビューは、非 FoxPro データまたは FoxPro と非 FoxPro データの組み合わせのいずれかにアクセスするビューです。 リモートのビューにアクセスするには、Visual FoxPro を使用します。  
  
## <a name="deleting-records"></a>レコードを削除します。  
 削除、ドライバーを使用してレコードをマークすることができますが、データベースからレコードを完全に削除することはできません。 テーブルからレコードを完全に削除するには、Visual FoxPro を使用します。  
  
## <a name="increasing-performance-using-background-fetching"></a>バック グラウンド フェッチを使用してパフォーマンスの向上  
 ドライバーの機能をフェッチしています。 バック グラウンドを使用して大規模なフェッチでパフォーマンスを向上できます。 特定のデータ ソースから要求されたデータをフェッチするのに別のスレッドを使用するバック グラウンドでフェッチしています。  
  
 バック グラウンドで、次の方法のいずれかのデータ ソースのフェッチを使用することができます。  
  
-   チェック、**バック グラウンドでデータをフェッチ**のチェック ボックス、 [ODBC Visual FoxPro セットアップ ダイアログ ボックス](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)します。  
  
-   接続文字列で BackgroundFetch 属性のキーワードを使用します。  
  
 接続文字列キーワードの属性については、次を参照してください。[接続文字列を使用して](../../odbc/microsoft/using-connection-strings.md)します。  
  
## <a name="updating-multitiered-views"></a>多階層ビューを更新しています  
 多階層ビューは、ベース テーブルではなく、1 つまたは複数のビューに基づいてビューです。 更新プログラムが最上位のビューの基になる; ビューに移動下のレベルを 1 つだけにするには、多層ビュー内のデータを更新するときにベース テーブルは更新されません。  
  
## <a name="using-data-definition-language-ddl-in-stored-procedures"></a>ストアド プロシージャでのデータ定義言語 (DDL) の使用  
 Visual FoxPro のストアド プロシージャで CREATE TABLE または ALTER TABLE などの DDL を使用することはできません。  
  
 ストアド プロシージャで使用できる言語については、次を参照してください。[ルール、トリガー、既定値、およびストアド プロシージャのサポート](../../odbc/microsoft/support-rules-triggers-defaults-stored-procedures-visual-foxpro-odbc-driver.md)します。  
  
## <a name="using-positioned-updates"></a>位置指定更新を使用します。  
 ドライバーは、位置指定更新をサポートしていません。 SQL の WHERE 句を使用すると、更新する行を識別できます。  
  
## <a name="using-the-set-ansi-command"></a>SET ANSI コマンドの使用  
 Visual FoxPro 開発者がいる場合は、設定の ANSI の既定の設定にある、ドライバーは、Visual FoxPro の OFF の既定の設定とは対照的に注意する必要があります。 設定の ANSI の設定に既定では、通常、正確な比較を実行する他の ODBC データ ソースで一貫して動作する Visual FoxPro データ ソースをできます。 既定の設定を変更することができます。 詳細については、次を参照してください。[設定の ANSI](../../odbc/microsoft/set-ansi-command.md)します。
