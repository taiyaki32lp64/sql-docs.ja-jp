---
title: トレース オプションの設定 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio Analyzer tracing [ODBC]
- ODBC data source administrator [ODBC], tracing options
- tracing options [ODBC], ODBC data source administrator
ms.assetid: 44404a79-b716-4bc1-9ffb-70cd8239d237
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 13e8caf9f3a9643f8063d6227258245a603f1665
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901629"
---
# <a name="setting-tracing-options"></a>トレース オプションの設定
**トレース**のタブ、 **ODBC データ ソース アドミニストレーター**  ダイアログ ボックスでは、ODBC 関数呼び出しをトレースする方法を構成することができます。  
  
## <a name="how-tracing-works"></a>トレースのしくみ  
 トレースを開始すると、**トレース** タブ、ドライバー マネージャーは、アプリケーションの実行後のすべてのすべての ODBC 関数呼び出しに記録されます。 トレースが開始される前に実行されているアプリケーションから ODBC 関数呼び出しは記録されません。 ODBC 関数呼び出しは、指定したログ ファイルに記録されます。  
  
 クリックした後、トレースが停止**今すぐトレースを停止**します。 トレースを向上させる、ログ ファイルが継続し、すべての ODBC アプリケーションのパフォーマンスに影響する注意してください。  
  
 トレースの詳細については、次を参照してください。[トレース](../../odbc/reference/develop-app/tracing.md)します。  
  
### <a name="changes-in-odbc-tracing"></a>ODBC トレースの変更  
 MDAC 2.7 SP2 では、前にトレースが任意の id で実行されているすべての ODBC アプリケーションの公開の詳細をキャプチャする、コンピューター全体の単位で ODBC トレースがのみ使用できます。 これには、プロセスの作成またはその他のローカル ユーザー アカウントおよびローカル サービスおよびネットワーク サービスなどのビルトイン セキュリティ プリンシパルの代わりに実行で発生する可能性のある ODBC に関連するアクティビティ トレースが含まれています。  
  
 既定で ODBC トレースは、ユーザー モードようになりました。 ローカル管理者の場合は、ただし、有効にできますもコンピューター全体のトレース、ODBC データ ソース アドミニストレーターを使用しています。  
  
 ODBC トレース モードを構成するには。  
  
1.  必要がある場合は、ローカルの Administrators グループのメンバーシップを持つアカウントを使用してログオンします。  
  
2.  管理ツールには、ODBC データ ソース アドミニストレーターを開きます。  
  
3.  をクリックして、**トレース**タブ。  
  
4.  トレース モードを使用して、構成、**コンピューター全体のトレースをすべてのユーザー id を** チェック ボックス。  
  
5.  コンピューター全体のトレースを有効にするには、チェック ボックスを選択します。  
  
6.  ユーザーごとのトレースを返すには、チェック ボックスをオフにします。  
  
7.  **[適用]** をクリックします。  
  
> [!NOTE]  
>  1 つのモードで既にトレースを開始する場合は、トレースを停止し、モードが正常に変更するその他のモードに切り替えるにする必要があります。  
  
> [!IMPORTANT]  
>  必要な場合、コンピューター全体のトレースを有効にする必要がありますのみ左のそれ以外の場合、オフにします。  
  
## <a name="visual-studio-analyzer-tracing"></a>Visual Studio Analyzer のトレース  
  
> [!IMPORTANT]  
>  Visual Studio Analyzer のサポートは、以降 (Visual Studio Analyzer のみ含まれていた以前のバージョンの Visual Studio でします。) Windows 8 では削除されました。 トラブルシューティング メカニズムの代わりに、BID のトレースを使用します。  
  
 Visual Studio® アナライザーのトレース、パフォーマンスと、ODBC 層に関するデバッグ情報を提供します。 ODBC コンポーネントに費やされた時間の関連をできるだけ正確なとして画像を表示する最上位レベルのインターフェイスにすべての送信イベントを発生します。 Visual Studio Analyzer のトレースには、任意のイベント ソース、ソースのセットアップ時に登録する必要があります。 この種のトレースの詳細については、Visual Studio のドキュメントを参照してください。
