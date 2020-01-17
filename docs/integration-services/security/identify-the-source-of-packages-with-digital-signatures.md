---
title: デジタル署名を使用してパッケージのソースを特定する | Microsoft Docs
ms.custom: security
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.digitalsigning.f1
helpviewer_keywords:
- signing packages [Integration Services]
- certificates [Integration Services]
- packages [Integration Services], security
- security [Integration Services], certificates
- signing policies [Integration Services]
ms.assetid: a433fbef-1853-4740-9d5e-8a32bc4ffbb2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fd8b17acb904ae0d33b06e85531e531792f1d60e
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295695"
---
# <a name="identify-the-source-of-packages-with-digital-signatures"></a>デジタル署名を使用してパッケージのソースを特定する

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージは、そのソースを識別するために、デジタル証明書を使用して署名できます。 パッケージがデジタル証明書を使用して署名されたら、パッケージを読み込む前に [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] でデジタル署名を確認できます。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] で署名を確認するには、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] または **dtexec** ユーティリティ (dtexec.exe) でオプションを設定するか、オプションのレジストリ値を設定します。  
  
## <a name="sign-a-package-with-a-digital-certificate"></a>デジタル証明書を使用してパッケージに署名する  
 デジタル証明書を使用してパッケージに署名する前に、証明書を取得または作成する必要があります。 証明書を用意したら、この証明書を使用してパッケージに署名できます。 証明書を取得し、その証明書を使用してパッケージに署名する方法の詳細については、「 [デジタル証明書を使用してパッケージに署名する](#cert)」を参照してください。  
  
## <a name="set-an-option-to-check-the-package-signature"></a>パッケージの署名を確認するオプションを設定する  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] と **dtexec** ユーティリティの両方に、署名付きパッケージのデジタル署名を確認するように [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] を構成するオプションがあります。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] と **dtexec** ユーティリティのどちらを使用するかは、すべてのパッケージを確認するか特定のパッケージだけを確認するかによって決まります。  
  
-   デザイン時にすべてのパッケージのデジタル署名を確認してからパッケージを読み込むには、 **で** [パッケージの読み込み時にデジタル署名を確認する] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]チェック ボックスをオンにします。 このオプションは、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]でのすべてのパッケージに対するグローバルな設定です。
  
-   個別のパッケージのデジタル署名を確認するには、 **dtexec** ユーティリティを使用してパッケージを実行するときに **/VerifyS[igned]** オプションを指定します。 詳細については、「 [dtexec Utility](../../integration-services/packages/dtexec-utility.md)」を参照してください。  
  
## <a name="set-a-registry-value-to-check-package-signature"></a>パッケージの署名を確認するレジストリ値を設定する  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] では、オプションのレジストリ値である **BlockedSignatureStates**もサポートされています。このレジストリ値を使用すると、署名付きパッケージと署名がないパッケージの読み込みに関する組織のポリシーを管理できます。 このレジストリ値により、パッケージが署名されていない場合、または無効な署名や信頼できない署名が含まれている場合に、パッケージが読み込まれないようにすることができます。 このレジストリ値を設定する方法の詳細については、「 [レジストリ値を設定して署名ポリシーを実装する](#registry)」を参照してください。  
  
> **注:** オプションの **BlockedSignatureStates** レジストリ値では、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] または **dtexec** コマンド ラインで設定されたデジタル署名オプションよりも制限が厳しい設定を指定できます。 この場合、制限が厳しい方のレジストリ設定が他の設定をオーバーライドします。  

## <a name="registry"></a> レジストリ値を設定して署名ポリシーを実装する
  オプションのレジストリ値を使用して、署名付きパッケージまたは署名がないパッケージを読み込む際の組織のポリシーを管理できます。 このレジストリ キーを使用する場合、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] が実行されるコンピューターおよびポリシーを適用するコンピューターごとにこのレジストリ値を作成する必要があります。 レジストリ値が設定されると、パッケージを読み込む前に、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] によって署名が確認されます。  
  
 このトピックの手順では、オプションの **BlockedSignatureStates** DWORD 値をレジストリ キー HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS に追加する方法について説明します。 **BlockedSignatureStates** のデータ値は、署名が信頼できない場合、署名が無効な場合、または署名がない場合に、そのパッケージをブロックするかどうかを決定します。 パッケージの署名に使用される署名のステータスについて、 **BlockedSignatureStates** レジストリ値では以下の定義が適用されます。  
  
-   *有効な署名* とは、正常に読み取ることができる署名のことです。  
  
-   *無効な署名* とは、暗号化解除済みのチェックサム (秘密キーによって暗号化されたパッケージ コードの一方向のハッシュ) が、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを読み込むプロセスの一部として計算された暗号化解除済みのチェックサムと一致しない署名のことです。  
  
-   *信頼できる署名* とは、信頼されているルート証明機関により署名されたデジタル証明書を使用して作成される署名のことです。 この設定で、署名者は、ユーザーの信頼できる発行元のリストに含まれている必要はありません。  
  
-   *信頼できない署名* とは、信頼されているルート証明機関によって発行されたことを確認できない署名、または最新ではない署名のことです。  
  
 次の表に、DWORD データの有効な値、およびそれらに関連付けられたポリシーを示します。  
  
|[値]|Description|  
|-----------|-----------------|  
|0|管理制限はありません。|  
|1|署名が無効なパッケージをブロックします。<br /><br /> この設定では、署名がないパッケージはブロックしません。|  
|2|署名が無効または信頼できないパッケージをブロックします。<br /><br /> この設定では、署名がないパッケージをブロックしませんが、自己生成された署名をブロックします。|  
|3|署名が無効であるか署名が信頼できないパッケージ、および署名がないパッケージをブロックします。<br /><br /> この設定では、自己生成された署名もブロックします。|  
  
> [!NOTE]  
>  **BlockedSignatureStates** の推奨設定は 3 です。 この設定では、署名されていないパッケージまたは無効な署名や信頼できない署名に対する最大の保護が提供されます。 ただし、推奨される設定がすべての状況に適しているとは限りません。 デジタル アセットの署名の詳細については、MSDN ライブラリの「[コード署名の概要](https://go.microsoft.com/fwlink/?LinkId=51414)」を参照してください。  
  
### <a name="to-implement-a-signing-policy-for-packages"></a>パッケージに対する署名ポリシーを実装するには  
  
1.  **[スタート]** メニューの **[ファイル名を指定して実行]** をクリックします。  
  
2.  [ファイル名を指定して実行] ダイアログ ボックスで、「 **Regedit**」と入力し、 **[OK]** をクリックします。  
  
3.  レジストリ キー HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS を探します。  
  
4.  **[MSDTS]** を右クリックし、 **[新規]** をポイントして、 **[DWORD 値]** をクリックします。  
  
5.  新しい値の名前を「 **BlockedSignatureStates**」に更新します。  
  
6.  **[BlockedSignatureStates]** を右クリックし、 **[変更]** をクリックします。  
  
7.  **[DWORD 値の編集]** ダイアログ ボックスで、「0」、「1」、「2」、または「3」のいずれかの値を入力します。  
  
8.  **[OK]** をクリックします。  
  
9. **[ファイル]** メニューの **[終了]** をクリックします。    

## <a name="cert"></a> デジタル証明書を使用してパッケージに署名する
  このトピックでは、デジタル証明書を使用して [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージに署名する方法について説明します。 デジタル署名を他の設定と共に使用して、有効でないパッケージの読み込みや実行を防ぐことができます。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージに署名する前に、次のタスクを実行する必要があります。  
  
-   証明書と関連付ける秘密キーを作成または取得して、この秘密キーをローカル コンピューターに格納します。  
  
-   信頼できる証明機関からコード署名用の証明書を入手します。 証明書を取得または作成するには、次のいずれかの方法を使用できます。  
  
    -   証明書を発行する公的な商用証明機関から証明書を入手します。  
  
    -   組織が証明書を内部的に発行できるようにする証明書サーバーから証明書を入手します。 証明書の署名に使用されるルート証明書を、 **[信頼されたルート証明機関]** ストアに追加する必要があります。 ルート証明書を追加するには、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理コンソール (MMC) の証明書スナップインを使用します。 詳細については、MSDN ライブラリの「[証明書サービス](https://go.microsoft.com/fwlink/?LinkId=100755)」を参照してください。  
  
    -   テスト目的でのみ独自の証明書を作成します。 証明書作成ツール (Makecert.exe) は、テスト目的で X.509 証明書を生成します。 詳細については、MSDN ライブラリの「[証明書作成ツール (Makecert.exe)](https://go.microsoft.com/fwlink/?LinkId=100756)」を参照してください。  
  
     証明書の詳細については、証明書スナップインのオンライン ヘルプを参照してください。 デジタル アセットの署名方法の詳細については、MSDN ライブラリの「[Authenticode を使用したコードの署名と検証](https://go.microsoft.com/fwlink/?LinkId=78100)」を参照してください。  
  
-   証明書がコードの署名用に有効になっていることを確認します。 証明書がコードの署名用に有効になっているかどうかを判断するには、証明書スナップインで証明書のプロパティを確認します。  
  
-   個人ストアに証明書を格納します。  
  
 上記のタスクが完了したら、次の手順に従ってパッケージに署名できます。  
  
### <a name="to-sign-a-package"></a>パッケージに署名するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、署名するパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで **[SSIS]** メニューの **[デジタル署名]** をクリックします。  
  
4.  **[デジタル署名]** ダイアログ ボックスで、 **[署名]** をクリックします。  
  
5.  **[証明書の選択]** ダイアログ ボックスで、証明書を選択します。  
  
6.  必要に応じて、 **[証明書の表示]** をクリックして証明書の情報を表示します。  
  
7.  **[OK]** をクリックして、 **[証明書の選択]** ダイアログ ボックスを閉じます。  
  
8.  **[OK]** をクリックして、 **[デジタル署名]** ダイアログ ボックスを閉じます。  
  
9. 更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
     パッケージは署名されましたが、パッケージを読み込む前にデジタル署名を確認するように、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] を構成する必要があります。  

## <a name="signing_dialog"></a> [デジタル署名] ダイアログ ボックスの UI リファレンス
  **[デジタル署名]** ダイアログ ボックスを使用すると、デジタル署名を使用してパッケージに署名したり、署名を削除したりできます。 **[デジタル署名]** ダイアログ ボックスは、 **の** [SSIS] **メニューの** [デジタル署名] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]から使用できます。  
  
 詳細については、「 [デジタル証明書を使用してパッケージに署名する](#cert)」を参照してください。  
  
### <a name="options"></a>オプション  
 **[署名]**  
 **[証明書の選択]** ダイアログ ボックスを開き、使用する証明書を選択します。  
  
 **[削除]**  
 デジタル署名を削除します。  

## <a name="see-also"></a>参照  
 [Integration Services &#40;SSIS&#41; パッケージ](../../integration-services/integration-services-ssis-packages.md)   
 [セキュリティの概要 &#40;Integration Services&#41;](../../integration-services/security/security-overview-integration-services.md)  
  
  
