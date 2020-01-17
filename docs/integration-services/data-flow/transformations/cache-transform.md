---
title: キャッシュ変換 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.cachetrans.f1
- sql13.dts.designer.cachetranscon.f1
- sql13.dts.designer.cachetransmap.f1
helpviewer_keywords:
- Cache transform
ms.assetid: a5683fc8-9c32-4634-819e-e9815627e4f1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1b934ea191a0dc4f9f276b4e483f5f5671bd0cc3
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297997"
---
# <a name="cache-transform"></a>キャッシュ変換

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  キャッシュ変換は、データ フロー内の接続されているデータ ソースのデータをキャッシュ接続マネージャーに書き込んで、参照変換用の参照データセットを生成します。 参照変換は、接続されているデータ ソースの入力列のデータを参照データベースの列と結合することにより参照を実行します。  
  
 参照変換をフル キャッシュ モードで実行するように構成する場合は、キャッシュ接続マネージャーを使用できます。 このモードでは、参照変換の実行前に参照データセットがキャッシュに読み込まれます。  
  
 キャッシュ接続マネージャーおよびキャッシュ変換でフル キャッシュ モードの参照変換を構成する手順については、「 [Implement a Lookup Transformation in Full Cache Mode Using the Cache Connection Manager](../../../integration-services/data-flow/transformations/lookup-transformation-full-cache-mode-cache-connection-manager.md)」(キャッシュ接続マネージャーを使用してフル キャッシュ モードの参照変換を実装する) を参照してください。  
  
 参照データセットのキャッシュの詳細については、「 [Lookup Transformation](../../../integration-services/data-flow/transformations/lookup-transformation.md)」を参照してください。  
  
> [!NOTE]  
>  キャッシュ変換では一意の行だけがキャッシュ接続マネージャーに書き込まれます。  
  
 単一のパッケージ内で同じキャッシュ接続マネージャーにデータを書き込むことができるのは 1 つのキャッシュ変換だけです。 パッケージに複数のキャッシュ変換が含まれている場合、パッケージが実行されたときに最初に呼び出されたキャッシュ変換が接続マネージャーにデータを書き込みます。 それ以降のキャッシュ変換による書き込み操作は失敗します。  
  
 詳細については、「[キャッシュ接続マネージャー](../../../integration-services/data-flow/transformations/cache-connection-manager.md)」を参照してください。  
  
## <a name="configuration-of-the-cache-transform"></a>キャッシュ変換の構成  
 データをキャッシュ ファイル (.caw) に保存するようにキャッシュ接続マネージャーを構成できます。  
  
 キャッシュ変換は、次の方法で構成できます。  
  
-   キャッシュ接続マネージャーを指定します。  
  
-   キャッシュ変換の入力列をキャッシュ接続マネージャーの変換先列にマップします。  
  
    > [!NOTE]  
    >  各入力列を変換先列にマップする必要があります。このとき、列のデータ型が一致している必要があります。 それ以外の場合、 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] デザイナーによりエラー メッセージが表示されます。  
  
     **[キャッシュ接続マネージャー エディター]** を使用して、列のデータ型、名前、およびその他の列プロパティを変更できます。  
  
 プロパティは、 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] デザイナーから設定できます。 **[詳細エディター]** ダイアログ ボックスで設定できるプロパティの詳細については、「 [Transformation Custom Properties](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)」を参照してください。  
  
 プロパティの設定方法の詳細については、「 [データ フロー コンポーネントのプロパティを設定する](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)」を参照してください。  
  
## <a name="cache-transformation-editor-connection-manager-page"></a>[キャッシュ変換エディター] ([接続マネージャー] ページ)
  **[キャッシュ変換エディター]** ダイアログ ボックスの **[接続マネージャー]** タブを使用すると、既存のキャッシュ接続マネージャーを選択したり、新しいキャッシュ接続マネージャーを作成したりできます。  
  
 キャッシュ接続マネージャーの詳細については、「 [Cache Connection Manager](../../../integration-services/data-flow/transformations/cache-connection-manager.md)」を参照してください。  
  
### <a name="options"></a>オプション  
 **Cache connection manager**  
 既存の OLE DB 接続マネージャーを一覧から選択するか、 **[新規作成]** をクリックして新しい接続を作成します。  
  
 **[新規作成]**  
 新しい接続を作成するには、[キャッシュ接続マネージャー エディター] ダイアログ ボックスを使用します。  
  
 **[編集]**  
 既存の接続を編集します。  
  
## <a name="see-also"></a>参照  
 [Integration Services の変換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [データ フロー](../../../integration-services/data-flow/data-flow.md)  
  
  
