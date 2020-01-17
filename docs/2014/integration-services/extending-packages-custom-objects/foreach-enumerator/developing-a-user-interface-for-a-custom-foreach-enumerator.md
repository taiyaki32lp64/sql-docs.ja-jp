---
title: カスタム ForEach 列挙子用ユーザー インターフェイスの開発 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom user interface [Integration Services], custom foreach enumerators
- custom foreach enumerators [Integration Services], developing custom user interface
ms.assetid: 8aa4aa80-c9ba-42b3-ba87-ae5ea5d3cac3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8965fcda896c67b2ae2e08cde54c679e6504b8b6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62896072"
---
# <a name="developing-a-user-interface-for-a-custom-foreach-enumerator"></a>カスタム ForEach 列挙子用ユーザー インターフェイスの開発
  基本クラスのプロパティとメソッドをオーバーライドしてカスタム機能を実装したら、Foreach 列挙子用のカスタム ユーザー インターフェイスを作成します。 カスタム ユーザー インターフェイスを作成しない場合、ユーザーは [プロパティ] ウィンドウを使用して新しいカスタム Foreach 列挙子を構成することしかできません。  
  
 カスタム ユーザー インターフェイスのプロジェクトまたはアセンブリで、<xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI> を実装するクラスを作成します。 このクラスは、通常他の Windows フォーム コントロールをホストするための複合コントロールの作成に使用される System.Windows.Forms.UserControl から派生します。 作成するコントロールは、 **[Foreach ループ エディター]** の **[コレクション]** タブの **[列挙子の構成]** 領域に表示されます。  
  
> [!IMPORTANT]  
>  「[Building, Deploying, and Debugging Custom Objects](../building-deploying-and-debugging-custom-objects.md)」(カスタム オブジェクトのビルド、配置、およびデバッグ) で説明されているようにカスタム ユーザー インターフェイスに署名してビルドし、グローバル アセンブリ キャッシュにインストールしたら、このクラスの完全修飾名を <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute> の <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute.UITypeName%2A> プロパティで忘れずに指定してください。  
  
## <a name="coding-the-user-interface-control-class"></a>ユーザー インターフェイス コントロール クラスのコーディング  
  
### <a name="initializing-the-user-interface"></a>ユーザー インターフェイスの初期化  
 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI.Initialize%2A> メソッドをオーバーライドして、ホスト オブジェクトへの参照、接続マネージャーのコレクションへの参照、およびパッケージで定義された変数をキャッシュします。  
  
### <a name="setting-properties-on-the-user-interface-control"></a>ユーザー インターフェイス コントロールでのプロパティの設定  
 ユーザー インターフェイス クラスの派生元である UserControl クラスは、他の Windows フォーム コントロールをホストするための複合コントロールとして使用することを目的としています。 このクラスが他のコントロールをホストするため、コントロールをドラッグ アンド ドロップし、それらを並べ替え、プロパティを設定し、すべての Windows フォーム アプリケーションと同じようにコントロールのイベントに実行時に応答することにより、カスタム ユーザー インターフェイスをデザインできます。  
  
### <a name="saving-settings"></a>設定の保存  
 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI.SaveSettings%2A> メソッドをオーバーライドして、ユーザーがエディターを終了したときに、ユーザーが選択した値をコントロールから列挙子のプロパティにコピーします。  
  
![Integration Services のアイコン (小)](../../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>参照  
 [カスタム Foreach 列挙子の作成](creating-a-custom-foreach-enumerator.md)   
 [カスタム Foreach 列挙子のコーディング](coding-a-custom-foreach-enumerator.md)  
  
  
