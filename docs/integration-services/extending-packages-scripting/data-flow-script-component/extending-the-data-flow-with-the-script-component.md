---
title: スクリプト コンポーネントによるデータ フローの拡張 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- data flow task [Integration Services], components
- data flow [Integration Services], extending
- debugging [Integration Services], components
- code design mode [Integration Services]
- metadata [Integration Services]
- scripts [Integration Services], extending data flow
- data flow components [Integration Services], Script component
- components [Integration Services], data flow
- Script component [Integration Services], about Script component
- Script component [Integration Services]
- data flow [Integration Services], components
ms.assetid: 072bc4b8-363a-4131-87c3-240338e2fa5c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 565252bee563fc0808a5ada6b515606c35f42187
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296956"
---
# <a name="extending-the-data-flow-with-the-script-component"></a>スクリプト コンポーネントによるデータ フローの拡張

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  スクリプト コンポーネントを使用すると、カスタム コードを [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic または [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# で記述し、パッケージの実行時にコンパイル、実行することにより、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] パッケージのデータ フロー処理能力を拡張できます。 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] に含まれる変換元、変換、変換先を使用するだけでは完全に要求を満たせない場合でも、スクリプト コンポーネントを使用すれば、カスタムのデータ フロー変換元、変換、変換先を容易に開発できます。 コンポーネントに必要な入力および出力を設定すれば、必要なインフラストラクチャ コードが自動生成されるので、カスタム処理を実行するために必要なコードの記述に集中できます。  
  
 スクリプト コンポーネントは、プロジェクト アイテム **ComponentWrapper** および **BufferWrapper** に自動生成されたクラスを介して、コンポーネントに含まれるパッケージやデータ フローとやり取りします。このプロジェクト アイテムは、それぞれ、<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> クラスおよび <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> クラスのインスタンスです。 このクラスは、接続、変数、および型指定されたオブジェクトとして使用できるその他のパッケージ アイテムを作成し、入力および出力を管理します。 また、カスタム アセンブリだけでなく、[!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 名前空間および [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] クラス ライブラリを使用して、スクリプト コンポーネントに独自の機能を実装することもできます。  
  
 スクリプト コンポーネントおよびそれによって生成されるインフラストラクチャ コードを活用すれば、カスタム データ フロー コンポーネントを開発するための手順を大幅に簡略化できます。 スクリプト コンポーネントの動作のしくみを理解するため、「[カスタム データ フロー コンポーネントの開発](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)」のセクションを参照して、カスタム データ フロー コンポーネントの開発手順を理解しておくと役立つ場合があります。  
  
 作成した変換元、変換、変換先を複数のパッケージで再利用する予定がある場合、スクリプト コンポーネントを使用する代わりに、カスタム コンポーネントの開発を検討してください。 詳細については、「 [カスタム データ フロー コンポーネントの開発](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 次のトピックでは、スクリプト コンポーネントの詳細について説明します。  
  
 [スクリプト コンポーネント エディターでのスクリプト コンポーネントの構成](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)  
 **[スクリプト変換エディター]** で設定したプロパティは、スクリプト コンポーネント コードの機能やパフォーマンスに影響します。  
  
 [スクリプト コンポーネントのコーディングおよびデバッグ](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)  
 スクリプト コンポーネントに含まれるスクリプトを開発するには、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) 開発環境を使用します。  
  
 [スクリプト コンポーネントのオブジェクト モデルについて](../../../integration-services/extending-packages-scripting/data-flow-script-component/understanding-the-script-component-object-model.md)  
 新しいスクリプト コンポーネント プロジェクトには、複数のクラスと自動生成されたプロパティおよびメソッドを含む 3 つのプロジェクト アイテムが含まれています。  
  
 [スクリプト コンポーネントでの変数の使用](../../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)  
 **ComponentWrapper** プロジェクト アイテムには、パッケージ変数に対して厳密に型指定されたアクセサー プロパティが含まれています。  
  
 [スクリプト コンポーネントでのデータ ソースへの接続](../../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)  
 **ComponentWrapper** プロジェクト アイテムには、パッケージで定義された接続に対して厳密に型指定されたアクセサー プロパティも含まれています。  
  
 [スクリプト コンポーネントでのイベントの発生](../../../integration-services/extending-packages-scripting/data-flow-script-component/raising-events-in-the-script-component.md)  
 イベントを発生させて、問題とエラーを通知することができます。  
  
 [スクリプト コンポーネントでのログ記録](../../../integration-services/extending-packages-scripting/data-flow-script-component/logging-in-the-script-component.md)  
 パッケージで有効なログ プロバイダーに情報を記録できます。  
  
 [特定の種類のスクリプト コンポーネントの開発](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)  
 スクリプト コンポーネントを使用してデータ フローの変換元、変換、変換先を開発する方法を、簡単な例を使って説明します。  
  
 [その他のスクリプト コンポーネントの例](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)  
 スクリプト コンポーネントのいくつかの使用方法を、簡単な例を使って説明します。  
  
## <a name="see-also"></a>参照  
 [スクリプト コンポーネント](../../../integration-services/data-flow/transformations/script-component.md)   
 [スクリプト タスクとスクリプト コンポーネントの比較](../../../integration-services/extending-packages-scripting/comparing-the-script-task-and-the-script-component.md)  
  
  
