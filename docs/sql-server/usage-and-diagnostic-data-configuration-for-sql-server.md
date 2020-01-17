---
title: SQL Server の使用状況および診断データの収集を構成する (CEIP) | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
ms.date: 03/27/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: ''
ms.technology: configuration
ms.openlocfilehash: d5248f97b044cb688174171fdb6ef79943851a92
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028935"
---
# <a name="configure-usage-and-diagnostic-data-collection-for-sql-server-ceip"></a>SQL Server の使用状況および診断データの収集を構成する (CEIP)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

## <a name="summary"></a>概要

Microsoft SQL Server は既定で、お客様のアプリケーションの使用状態に関する情報を収集します。 具体的には、SQL Server はインストール エクスペリエンス、利用状況、およびパフォーマンスに関する情報を収集します。 この情報は、Microsoft が製品の向上を図り、お客様のニーズをさらに満たすのに役立ちます。 たとえば Microsoft では、お客様が受け取るエラー コードの種類に関する情報を収集して、関連するバグの修正、SQL Server の使用方法に関するドキュメントの改善、より良いサービスのために製品に機能を追加すべきかどうかの判断を行います。

具体的には、Microsoft はこのメカニズムでは次の種類の情報は送信しません。
- ユーザー テーブル内からのすべての値
- すべてのログオン資格情報またはその他の認証情報
- 個人を特定できる情報 (PII)

次のサンプル シナリオには、製品の向上に役立つ、機能の利用状況の情報が含まれます。

SQL Server 2017 は列ストア インデックスをサポートし、高速な分析シナリオを可能にします。 列ストア インデックスでは、新しく挿入されるデータに対して、従来の「B ツリー」インデックス構造と特殊な列指向の圧縮構造とを結合し、データを圧縮してクエリ実行の速度を上げます。 製品には、バックグラウンドで B ツリー構造から圧縮構造にデータを移行するヒューリスティックが含まれており、それによってその後のクエリ結果の速度を上げます。

バック グラウンド操作がデータ挿入の速度に追いつかない場合、クエリのパフォーマンスが想定よりも遅くなることがあります。 製品向上のため、Microsoft では、SQL Server がデータの自動圧縮プロセスにどれくらい追いついているかの情報を収集します。 製品チームはこの情報を活用して、圧縮を実行するコードの頻度と並列処理を微調整します。 このクエリはこの情報を収集するために不定期に実行されるため、Microsoft はデータの移動速度を評価できます。 これによって、製品のヒューリスティックを最適化することができます。  

```sql
SELECT object_id, type_desc, data_space_id, db_id() AS database_id FROM sys.indexes WITH(nolock) WHERE type = 5 or type = 6 
```

```sql
SELECT cntr_value as merge_policy_evaluation
FROM sys.dm_os_performance_counters WITH(nolock)
WHERE object_name LIKE '%columnstore%' 
AND counter_name ='Total Merge Policy Evaluations' 
AND instance_name = '_Total'
```

このプロセスは、お客様に価値あるものをお届けするために必要なメカニズムに重点を置いたものです。 製品チームはインデックス内のデータを見ることはなく、そうしたデータを Microsoft に送信することもありません。 SQL Server 2017 は、インストール エクスペリエンスに関する情報をセットアップ時点から常に収集および送信して、お客様側で発生しているインストールの問題をすばやく発見し修正できるようにします。 SQL Server 2017 は、次のメカニズムによって、Microsoft に (サーバー インスタンスごとに) 情報を送信しないように構成できます。
- エラーと使用状況レポートのアプリケーションの使用
- サーバー上でのレジストリ サブキーの設定

Linux 上の SQL Server については、「[Customer Feedback for SQL Server on Linux (Linux 上の SQL Server のカスタマー フィードバック)](https://docs.microsoft.com/sql/linux/sql-server-linux-customer-feedback)」をご覧ください。

> [!NOTE]
> Microsoft への情報送信を無効にできるのは、有料版の SQL Server のみです。

## <a name="remarks"></a>備考
 - SQL CEIP サービスの削除または無効化はサポートされていません。 
 - クラスター グループからの SQL CEIP リソースの削除はサポートされていません。 

データ収集をオプト アウトするには、「[ローカル監査の有効/無効を切り替える](usage-and-diagnostic-data-in-local-audit.md#turning-local-audit-on-or-off)」を参照してください。

## <a name="error-and-usage-reporting-application"></a>エラーと使用状況レポートのアプリケーション 

セットアップ後は、SQL Server コンポーネントおよびインスタンスの使用状況と診断データの収集の設定は、エラーと使用状況レポートのアプリケーションを通じて変更できます。 このアプリケーションは、SQL Server のインストールの一部として提供されます。 このツールを使うと、それぞれの SQL Server インスタンスで、それ自体の使用状況レポート設定を構成できます。

> [!NOTE]
> エラーと使用状況レポートのアプリケーションは、SQL Server の構成ツールに表示されます。 このツールを使用して、SQL Server 2017 と同様の方法で、エラー報告および使用状況と診断データの収集の設定を管理できます。 エラー報告は、使用状況と診断データの収集とは異なるため、使用状況と診断データの収集に関係なくオンまたはオフにすることができます。 エラー報告では、Microsoft に送信するクラッシュ ダンプを収集しますが、それには「[プライバシーに関する声明](https://go.microsoft.com/fwlink/?LinkID=868444)」で説明されているような機密情報が含まれている可能性があります。

SQL Server エラーと使用状況レポートを開始するには、 **[開始]** をクリックまたはタップし、検索ボックスで「エラー」を検索します。 SQL Server エラーと使用状況レポートの項目が表示されます。 このツールを開始した後は、使用状況と診断データに加えて、インスタンスとそのコンピューターにインストールされているコンポーネントについて収集された重大なエラーを管理できます。

有料版では、[使用状況レポート] チェック ボックスを使用して、使用状況と診断データの Microsoft への送信を管理します。

有料版または無料版では、[エラー レポート] チェック ボックスを使用して、重大なエラーについてのフィードバックとクラッシュ ダンプの Microsoft への送信を管理します。

## <a name="set-registry-subkeys-on-the-server"></a>サーバー上でのレジストリ サブキーの設定

企業のお客様は、グループ ポリシーの設定を構成して、使用状況と診断データの収集のオプトイン、オプトアウトを設定できます。 これを行うには、レジストリに基づいたポリシーを構成します。 関連するレジストリ サブキーと設定は以下の通りです。

- SQL Server インスタンスの機能
    
    Subkey = HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\{InstanceID}\CPE
    
    レジストリ エントリ名 = CustomerFeedback
    
    エントリのデータ型 DWORD :0 はオプトアウト、1 はオプトインです
    
    {InstanceID} は、次の例のように、インスタンスの型とインスタンスを表します。

    - SQL Server 2017 データベース エンジンの MSSQL14.CANBERRA、インスタンス名は "CANBERRA"
    - SQL Server 2017 Analysis Services の MSAS14.CANBERRA、インスタンス名は "CANBERRA"
    - SQL Server 2017 Reporting Services の MSRS14.CANBERRA、インスタンス名は "CANBERRA"

- すべての共有機能
    
    Subkey = HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\{Major Version}
    
    レジストリ エントリ名 = CustomerFeedback
    
    エントリのデータ型 DWORD :0 はオプトアウト、1 はオプトインです

> [!NOTE]
> {Major Version} は SQL Server のバージョンを表します。たとえば、SQL Server 2017 は 140 です。

- SQL Server Management Studio 17 と SQL Server Management Studio 18 については、「[SQL Server Management Studio のユーザー サポート](../ssms/sql-server-management-studio-telemetry-ssms.md)」をご覧ください

## <a name="set-registry-subkeys-for-crash-dump-collection"></a>クラッシュ ダンプ収集のレジストリ サブキーの設定

SQL Server の以前のバージョンでの動作と同様に、SQL Server 2017 Enterprise のお客様は、サーバーでグループ ポリシー設定を構成してクラッシュ ダンプの収集のオプトイン、オプトアウトを設定できます。 これを行うには、レジストリに基づいたポリシーを構成します。 関連するレジストリ サブキーと設定は以下の通りです。 

- SQL Server インスタンスの機能

    Subkey = HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\{InstanceID}\CPE

    レジストリ エントリ名 = EnableErrorReporting

    エントリのデータ型 DWORD :0 はオプトアウト、1 はオプトインです
 
    {InstanceID} は、次の例のように、インスタンスの型とインスタンスを表します。 

    - SQL Server 2017 データベース エンジンの MSSQL14.CANBERRA、インスタンス名は "CANBERRA"
    - SQL Server 2017 Analysis Services の MSAS14.CANBERRA、インスタンス名は "CANBERRA"
    - SQL Server 2017 Reporting Services の MSRS14.CANBERRA、インスタンス名は "CANBERRA"
 

- すべての共有機能
    
    Subkey = HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\{Major Version}

    レジストリ エントリ名 = EnableErrorReporting

    エントリのデータ型 DWORD :0 はオプトアウト、1 はオプトインです

> [!NOTE]
> {Major Version} は SQL Server のバージョンを表します。 たとえば、"140" は、SQL Server 2017 を指します。

これらのレジストリ サブキー上のレジストリに基づいたグループ ポリシーは、SQL Server 2017 クラッシュ ダンプ収集で受け入れられます。 

## <a name="crash-dump-collection-for-ssms"></a>SSMS のクラッシュ ダンプの収集
SSMS では、それ自体のクラッシュ ダンプを収集しません。 SSMS に関連するクラッシュ ダンプはすべて、Windows エラー報告の一部として収集されます。

この機能をオンまたはオフにする手順は、対象の OS バージョンによって異なります。 機能をオンまたはオフにするには、お使いの Windows バージョンの該当資料にある手順を実行してください。
 
- Windows Server 2016 および Windows 10

    [組織内の Windows 診断データの構成](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)
- Windows Server 2008 R2 および Windows 7

    [WER 設定](/windows/desktop/wer/wer-settings)
 
## <a name="feedback-for-analysis-services"></a>Analysis Services に関するフィードバック

インストール中に、SQL Server 2016 Analysis Services は Analysis Services インスタンスに特別なアカウントを追加します。 このアカウントは、Analysis Services Server 管理者ロールのメンバーです。 このアカウントを使用して、Analysis Services インスタンスからフィードバック情報を収集します。  

「サーバー上でのレジストリ サブキーの設定」セクションで説明したように、お使いのサービスで使用状況と診断データを送信しないように構成できます。 ただし、これを実行しても、サービス アカウントは削除されません。 
 
[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
