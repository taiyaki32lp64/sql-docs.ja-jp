---
title: レジストリ値を設定して署名ポリシーを実装する |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- signing policies [Integration Services]
ms.assetid: 64f6966f-2292-401f-acb1-2ccb5aee484a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 21bda8729c30df9493c4f969c5af05b6dd80386f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66058214"
---
# <a name="implement-a-signing-policy-by-setting-a-registry-value"></a>レジストリ値を設定して署名ポリシーを実装する
  オプションのレジストリ値を使用して、署名付きパッケージまたは署名がないパッケージを読み込む際の組織のポリシーを管理できます。 このレジストリ キーを使用する場合、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] が実行されるコンピューターおよびポリシーを適用するコンピューターごとにこのレジストリ値を作成する必要があります。 レジストリ値が設定されると、パッケージを読み込む前に、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] によって署名が確認されます。  
  
 このトピックの手順では、オプションの `BlockedSignatureStates` DWORD 値をレジストリ キー HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS に追加する方法について説明します。 `BlockedSignatureStates` のデータ値は、署名が信頼できない場合、署名が無効な場合、または署名がない場合に、そのパッケージをブロックするかどうかを決定します。 パッケージの署名に使用される署名のステータスについて、`BlockedSignatureStates` レジストリ値では以下の定義が適用されます。  
  
-   *有効な署名* とは、正常に読み取ることができる署名のことです。  
  
-   *無効な署名* とは、暗号化解除済みのチェックサム (秘密キーによって暗号化されたパッケージ コードの一方向のハッシュ) が、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージを読み込むプロセスの一部として計算された暗号化解除済みのチェックサムと一致しない署名のことです。  
  
-   *信頼できる署名* とは、信頼されているルート証明機関により署名されたデジタル証明書を使用して作成される署名のことです。 この設定で、署名者は、ユーザーの信頼できる発行元のリストに含まれている必要はありません。  
  
-   *信頼できない署名* とは、信頼されているルート証明機関によって発行されたことを確認できない署名、または最新ではない署名のことです。  
  
 次の表に、DWORD データの有効な値、およびそれらに関連付けられたポリシーを示します。  
  
|値|Description|  
|-----------|-----------------|  
|0|管理制限はありません。|  
|1|署名が無効なパッケージをブロックします。<br /><br /> この設定では、署名がないパッケージはブロックしません。|  
|2|署名が無効または信頼できないパッケージをブロックします。<br /><br /> この設定では、署名がないパッケージをブロックしませんが、自己生成された署名をブロックします。|  
|3|署名が無効であるか署名が信頼できないパッケージ、および署名がないパッケージをブロックします。<br /><br /> この設定では、自己生成された署名もブロックします。|  
  
> [!NOTE]  
>  `BlockedSignatureStates` の推奨設定値は 3 です。 この設定では、署名されていないパッケージまたは無効な署名や信頼できない署名に対する最大の保護が提供されます。 ただし、推奨される設定がすべての状況に適しているとは限りません。 デジタル アセットの署名の詳細については、MSDN ライブラリの「[コード署名の概要](https://go.microsoft.com/fwlink/?LinkId=51414)」を参照してください。  
  
### <a name="to-implement-a-signing-policy-for-packages"></a>パッケージに対する署名ポリシーを実装するには  
  
1.  **[スタート]** メニューの **[ファイル名を指定して実行]** をクリックします。  
  
2.  実行 ダイアログ ボックスで、次のように入力します。 `Regedit`、 をクリックし、 **OK**します。  
  
3.  レジストリ キー HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS を探します。  
  
4.  **[MSDTS]** を右クリックし、 **[新規]** をポイントして、 **[DWORD 値]** をクリックします。  
  
5.  新しい値の名前を「`BlockedSignatureStates`」に更新します。  
  
6.  右クリック`BlockedSignatureStates`クリック**変更**します。  
  
7.  **[DWORD 値の編集]** ダイアログ ボックスで、「0」、「1」、「2」、または「3」のいずれかの値を入力します。  
  
8.  **[OK]** をクリックします。  
  
9. **[ファイル]** メニューの **[終了]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [セキュリティの概要 (Integration Services)](security/security-overview-integration-services.md)   
 [デジタル署名を使用してパッケージのソースを特定する](security/identify-the-source-of-packages-with-digital-signatures.md)  
  
  
