---
title: SQL Server ツールの使用状況と診断データの収集を構成する (CEIP) | Microsoft Docs
ms.custom: ''
ms.date: 10/21/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: baf3a205-a6bb-4564-8b64-3a0475bb9273
author: stevestein
ms.author: sstein
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 556d60a4c7f2cc8003f6b9a29fa20dad8c5b72ef
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091812"
---
# <a name="configure-usage-and-diagnostic-data-collection-for-sql-server-tools-ceip"></a>SQL Server ツールの使用状況と診断データの収集を構成する (CEIP)

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Microsoft がカスタマー エクスペリエンス向上プログラム (CEIP) により、どのようにしてソフトウェアを改善する方法を特定しているかについて説明します。  有効または無効にするツールはいつでも構成することができます。  
  
> [!NOTE]  
> Microsoft SQL Server リリースのユーザー データの収集および使用方法については、この「[プライバシーに関する声明](https://go.microsoft.com/fwlink/?LinkID=868444)」を参照してください。  
  
## <a name="opting-in-and-out-of-ceip-for-sql-server-data-tools"></a>SQL Server Data Tools の CEIP を有効または無効にする  

 カスタマー エクスペリエンス向上プログラムは、Microsoft が時間の経過と共に製品を向上させるために記述されたプログラムです。 このプログラムは、コンピューターで実行しているユーザーのタスクを中断することなく、コンピューターのハードウェアおよびユーザーによる製品の利用状況を収集します。 収集される情報は、Microsoft がどの機能を改善するかを特定するために役立ちます。 このドキュメントでは、Visual Studio 2017、Visual Studio 2015 および Visual Studio 2013 で SQL Server Data Tools (SSDT) の CEIP を有効または無効にする方法について説明します。  SQL Server の CEIP をオプト アウトする方法については、[SQL Server のローカル監査の有効/無効の切り替え](usage-and-diagnostic-data-in-local-audit.md#turning-local-audit-on-or-off)に関する記事を参照してください。

### <a name="choice-and-control-over--ceip-and-sql-server-data-tools-for-visual-studio-2017"></a>Visual Studio 2017 の CEIP と SQL Server Data Tools の選択および制御

 Visual Studio 2017 の SSDT は、SQL Server 2017 に付属するデータ モデリング ツールです。 Visual Studio 2017 に組み込まれている CEIP オプションが使用されます。 Visual Studio 2017 の CEIP を通じてフィードバックを送信する方法の詳細は、[Visual Studio のヘルプ ドキュメント](https://www.visualstudio.com/docs/work/connect/give-feedback)で確認できます。  
  
 プレビュー版の SQL Server 2017 では、CEIP が既定で有効になっています。 次の手順で、無効にし、再度有効に戻すことができます。  
  
 **Visual Studio の場合 (全言語がインストールされた Visual Studio 2017 に適用されます)**  
  
 既に Visual Studio が含まれているコンピューターに SSDT セットアップを実行する場合は、SQL Server および Business Intelligence プロジェクト テンプレートのみが追加されます。 このシナリオでは、Visual Studio で提供されるカスタマー フィードバックのオプションを使用して CEIP を有効または無効にできます。  
  
1.  Visual Studio を起動します。  
  
2.  [ヘルプ] メニューから、 **[フィードバックの送信]**  >  **[設定]** を選択します。  
  
3.  CEIP をオフにするには、 **[いいえ、協力しません]** をクリックし、 **[OK]** をクリックします。  
  
     CEIP をオンにするには、 **[はい、協力します]** をクリックし、 **[OK]** をクリックします。  
  

  
 **レジストリ ベースのポリシーまたはグループ ポリシーを使用する**  
  
 Visual Studio 2017 がないコンピューターに SSDT セットアップを実行すると、Visual Studio Shell のみがインストールされます。 このシェルは、カスタマー フィードバックのオプションを提供していません。 この場合、CEIP を構成するための唯一のオプションがレジストリの更新です。  
  
 企業のお客様の場合、SQL Server 2017 のレジストリ ベースのポリシーを設定することにより、有効または無効にするグループ ポリシーが構成されている場合があります。  
  
 これに関連するレジストリ キーと設定は以下のとおりです。  
  
- 64 ビット OS のキー = HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\VSCommon\15.0\SQM
- 32 ビット OS のキー = HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VSCommon\15.0\SQM

グループ ポリシーが有効な場合のキー = HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\VisualStudio\SQM 

エントリ = OptIn

値 = (DWORD)
- 0 はオプトアウトされます (VSCEIP はオフ)
- 1 はオプトインされます (VSCEIP はオン)

  
> [!CAUTION]  
>  レジストリの編集を誤ると、システムに深刻な悪影響を及ぼす可能性があります。 レジストリを変更する前に、コンピューター上のすべての重要なデータをバックアップしておくことをお勧めします。 手動での変更の適用後に問題が発生した場合は、[前回正常起動時の構成] スタートアップ オプションを使うこともできます。  
  
 CEIP により収集、処理、および送信される情報の詳細については、「[プライバシーに関する声明](https://go.microsoft.com/fwlink/?LinkID=868444)」を参照してください。  
 
### <a name="choice-and-control-over-ceip-and-sql-server-data-tools-for-visual-studio-2015"></a>Visual Studio 2015 の CEIP と SQL Server Data Tools の選択および制御  
 Visual Studio 2015 の SSDT は、SQL Server 2016 に付属するデータ モデリング ツールです。 Visual Studio 2015 に組み込まれている CEIP オプションが使用されます。 Visual Studio 2015 の CEIP を通じてフィードバックを送信する方法の詳細は、[Visual Studio のヘルプ ドキュメント](https://docs.microsoft.com/visualstudio/ide/how-to-report-a-problem-with-visual-studio-2017)で確認できます。  
  
 プレビュー版の SQL Server 2016 では、CEIP が既定で有効になっています。 次の手順で、無効にし、再度有効に戻すことができます。  
  
 **Visual Studio の場合 (全言語がインストールされた Visual Studio 2015 に適用されます)**  
  
 既に Visual Studio が含まれているコンピューターに SSDT セットアップを実行する場合は、SQL Server および Business Intelligence プロジェクト テンプレートのみが追加されます。 このシナリオでは、Visual Studio で提供されるカスタマー フィードバックのオプションを使用して CEIP を有効または無効にできます。  
  
1.  Visual Studio を起動します。  
  
2.  [ヘルプ] メニューから、 **[フィードバックの送信]**  >  **[設定]** を選択します。  
  
3.  CEIP をオフにするには、 **[いいえ、協力しません]** をクリックし、 **[OK]** をクリックします。  
  
     CEIP をオンにするには、 **[はい、協力します]** をクリックし、 **[OK]** をクリックします。  
  

  
 **レジストリ ベースのポリシーまたはグループ ポリシーを使用する**  
  
 Visual Studio 2015 がないコンピューターに SSDT セットアップを実行すると、Visual Studio Shell のみがインストールされます。 このシェルは、カスタマー フィードバックのオプションを提供していません。 この場合、CEIP を構成するための唯一のオプションがレジストリの更新です。  
  
 企業のお客様の場合、SQL Server 2016 のレジストリ ベースのポリシーを設定することにより、有効または無効にするグループ ポリシーが構成されている場合があります。  
  
 これに関連するレジストリ キーと設定は以下のとおりです。  
  
 キー = HKEY_CURRENT_USER\Software\Microsoft\VSCommon\14.0\SQM  
  
 レジストリ エントリ名 = OptIn  
  
 エントリのデータ型 DWORD :  
  
-   0 は無効  
  
-   1 は有効  
  
> [!CAUTION]  
>  レジストリの編集を誤ると、システムに深刻な悪影響を及ぼす可能性があります。 レジストリを変更する前に、コンピューター上のすべての重要なデータをバックアップしておくことをお勧めします。 手動での変更の適用後に問題が発生した場合は、[前回正常起動時の構成] スタートアップ オプションを使うこともできます。  
  
 CEIP により収集、処理、および送信される情報の詳細については、「[プライバシーに関する声明](https://go.microsoft.com/fwlink/?LinkID=868444)」を参照してください。  
  
### <a name="choice-and-control-for-ceip-and-sql-server-data-tools---bi-ssdt-bi"></a>CEIP および SQL Server Data Tools - BI (SSDT BI) の選択および制御  
 SSDT-BI を使用している場合、インストール中に CEIP に協力するかどうかを選択できます。 SSDT-BI の CEIP の構成は、後でクライアント ツールまたはレジストリ設定の編集により変更することができます。  
  
 **Visual Studio 2013 の SSDT および SSDT-BI の場合**  
  
1.  ツールを起動し、Analysis Services または Integration Services の新規または既存プロジェクトを開きます。  
  
2.  [ヘルプ] メニューから **[Microsoft SQL Server カスタマー フィードバックのオプション]** を選択します。  
  
3.  CEIP を無効にするには、 **[参加しない]** をクリックします。  
  
     CEIP を有効にするには、 **[参加する (推奨)]** をクリックします。  
  
4.  **[OK]** をクリックします。  
  
 **レジストリ ベースのポリシーまたはグループ ポリシーを使用する**  
  
 企業のお客様の場合、SQL Server 2014 のレジストリ ベースのポリシーを設定することにより、有効または無効にするグループ ポリシーが構成されている場合があります。  
  
 これに関連するレジストリ キーと設定は以下のとおりです。  
  
 キー = HKEY_CURRENT_USER\Software\Microsoft\Microsoft SQL Server\120  
  
 レジストリ エントリ名 = CustomerFeedback  
  
 エントリのデータ型 DWORD :  
  
-   0 は無効  
  
-   1 は有効  
  
  
