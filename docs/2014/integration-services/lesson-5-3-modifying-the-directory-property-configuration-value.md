---
title: 手順 3:Directory プロパティの構成値の変更 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ba2a091f-361c-4331-afe2-53b465164c36
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: cb83ac5bb1b811c23b782b01167c437e9b989518
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62767364"
---
# <a name="step-3-modifying-the-directory-property-configuration-value"></a>手順 3:Directory プロパティの構成値の変更
  ここでは、SSISTutorial.dtsConfig ファイルに保存されている構成設定のうち、パッケージ レベル変数 `User::varFolderName`の Value プロパティを変更します。 この変数は、ForEach ループ コンテナーの Directory プロパティを更新します。 変更後の値がポイントして、`New Sample Data`前のタスクで作成したフォルダーにします。 構成設定を変更し、パッケージを実行すると、パッケージ レベル変数によって Directory プロパティが更新されます。この更新では、パッケージにもともと構成されていた Directory 値は使用されず、構成ファイルから生成された値が使用されます。  
  
### <a name="to-modify-the-configuration-setting-of-the-directory-property"></a>Directory プロパティの構成設定を変更するには  
  
1.  前の実習でパッケージ構成ウィザードを使用して作成した SSISTutorial.dtsConfig 構成ファイルを探し、メモ帳などのテキスト エディターで開きます。  
  
2.  値を変更、 **ConfiguredValue**のパスと一致する要素、`New Sample Data`前のタスクで作成したフォルダーにします。 パスは引用符で囲まないでください。 場合、`New Sample Data`フォルダーがドライブのルート レベルにある (たとえば、c:\\)、更新された XML は次の例のようになります。  
  
     `<?xml version="1.0"?><DTSConfiguration><DTSConfigurationHeading><DTSConfigurationFileInfo GeneratedBy="DOMAIN\UserName" GeneratedFromPackageName="Lesson 5" GeneratedFromPackageID="{F4475E73-59E3-478F-8EB2-B10AFA61D3FA}" GeneratedDate="6/10/2012 8:16:50 AM"/></DTSConfigurationHeading><Configuration ConfiguredType="Property" Path="\Package.Variables[User::varFolderName].Properties[Value]" ValueType="String"><ConfiguredValue></ConfiguredValue></Configuration></DTSConfiguration>`  
  
     見出しは、 `GeneratedBy`、 `GeneratedFromPackageID`、および**GeneratedDate**なります別ファイルで、もちろんです。 `Configuration` 要素に注目してください。 変数の `Value` プロパティである `User::varFolderName` に、C:\New Sample Data が含まれています。  
  
3.  変更を保存し、テキスト エディターを閉じます。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [手順 4:レッスン 5 のチュートリアル パッケージのテスト](../integration-services/lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
  
