---
title: デジタル署名を使用してパッケージのソースを特定する | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- signing packages [Integration Services]
- certificates [Integration Services]
- packages [Integration Services], security
- security [Integration Services], certificates
- signing policies [Integration Services]
ms.assetid: a433fbef-1853-4740-9d5e-8a32bc4ffbb2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 714ede33a89a3ab4e44dae682887ee0c21c9f363
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62766654"
---
# <a name="identify-the-source-of-packages-with-digital-signatures"></a>デジタル署名を使用してパッケージのソースを特定する
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージは、そのソースを識別するために、デジタル証明書を使用して署名できます。 パッケージがデジタル証明書を使用して署名されたら、パッケージを読み込む前に [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] でデジタル署名を確認できます。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] で署名を確認するには、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] または **dtexec** ユーティリティ (dtexec.exe) でオプションを設定するか、オプションのレジストリ値を設定します。  
  
## <a name="signing-a-package-with-a-digital-certificate"></a>デジタル証明書を使用したパッケージの署名  
 デジタル証明書を使用してパッケージに署名する前に、証明書を取得または作成する必要があります。 証明書を用意したら、この証明書を使用してパッケージに署名できます。 証明書を取得し、その証明書を使用してパッケージに署名する方法の詳細については、「 [デジタル証明書を使用してパッケージに署名する](../sign-a-package-by-using-a-digital-certificate.md)」を参照してください。  
  
## <a name="setting-an-option-to-check-the-package-signature"></a>パッケージの署名を確認するオプションの設定  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] と **dtexec** ユーティリティの両方に、署名付きパッケージのデジタル署名を確認するように [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] を構成するオプションがあります。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] と **dtexec** ユーティリティのどちらを使用するかは、すべてのパッケージを確認するか特定のパッケージだけを確認するかによって決まります。  
  
-   デザイン時にすべてのパッケージのデジタル署名を確認してからパッケージを読み込むには、 **で** [パッケージの読み込み時にデジタル署名を確認する] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]チェック ボックスをオンにします。 このオプションは、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]でのすべてのパッケージに対するグローバルな設定です。 詳細については、「 [General Page](../general-page-of-integration-services-designers-options.md)」を参照してください。  
  
-   個々 のパッケージのデジタル署名を確認するには、指定、`/VerifyS[igned]`オプションを使用する場合、 **dtexec**ユーティリティでパッケージを実行します。 詳しくは、「 [dtexec Utility](../packages/dtexec-utility.md)」をご覧ください。  
  
## <a name="setting-a-registry-value-to-check-the-package-signature"></a>パッケージの署名を確認するレジストリ値の設定  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] では、オプションのレジストリ値である **BlockedSignatureStates**もサポートされています。このレジストリ値を使用すると、署名付きパッケージと署名がないパッケージの読み込みに関する組織のポリシーを管理できます。 このレジストリ値により、パッケージが署名されていない場合、または無効な署名や信頼できない署名が含まれている場合に、パッケージが読み込まれないようにすることができます。 このレジストリ値を設定する方法の詳細については、「[レジストリ値を設定して署名ポリシーを実装する](../implement-a-signing-policy-by-setting-a-registry-value.md)」を参照してください。  
  
> [!NOTE]  
>  オプションの **BlockedSignatureStates** レジストリ値では、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] または **dtexec** コマンド ラインで設定されたデジタル署名オプションよりも制限が厳しい設定を指定できます。 この場合、制限が厳しい方のレジストリ設定が他の設定をオーバーライドします。  
  
## <a name="see-also"></a>参照  
 [Integration Services &#40;SSIS&#41; パッケージ](../integration-services-ssis-packages.md)   
 [セキュリティの概要 &#40;Integration Services&#41;](security-overview-integration-services.md)  
  
  
