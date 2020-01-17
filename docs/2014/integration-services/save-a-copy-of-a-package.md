---
title: パッケージのコピーの保存 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, saving
- packages [Integration Services], saving
- saving packages
- SSIS packages, saving
- SQL Server Integration Services packages, saving
ms.assetid: 21482a20-e420-4452-b7eb-8f9fa1929f31
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: bdd8754ac3d4a63e038218c054d064f20485344b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66056265"
---
# <a name="save-a-copy-of-a-package"></a>パッケージのコピーを保存する
  この手順では、パッケージのコピーをファイル システム、パッケージ ストア、または [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の **msdb** データベースに保存する方法について説明します。 パッケージのコピーを保存する場所を指定するとき、パッケージの名前を更新することもできます。  
  
 パッケージ ストアには、 **msdb** データベースとファイル システム内のフォルダーの両方、 **msdb**のみ、またはファイル システム内のフォルダーのみを含めることができます。 **msdb**では、パッケージは **sysssispackages** テーブルに保存されます。 このテーブルには、パッケージが属する論理フォルダーを識別する **folderid** 列があります。 論理フォルダーは、 **msdb** に保存されるパッケージをグループ化するための便利な方法を提供します。これは、ファイル システムのフォルダーが、ファイル システムに保存されるパッケージをグループ化する方法を提供するのと同じです。 **msdb** 内の **sysssispackagefolders** テーブルの行は、フォルダーを定義します。  
  
 **msdb** がパッケージ ストアの一部として定義されていない場合は、 **[パッケージのパス]** オプションで [SQL Server] を選択するときに、引き続きパッケージを既存の論理フォルダーに関連付けることができます。  
  
> [!NOTE]  
>  パッケージのコピーを保存するには、事前にパッケージを [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーで開いておく必要があります。  
  
### <a name="to-save-a-copy-of-a-package"></a>パッケージのコピーを保存するには  
  
1.  ソリューション エクスプローラーで、コピーを保存するパッケージをダブルクリックします。  
  
2.  **[ファイル]** メニューの **[\<パッケージ ファイル> のコピーに名前を付けて保存]** をクリックします。  
  
3.  **[パッケージのコピーの保存]** ダイアログ ボックスで、 **[パッケージの場所]** 一覧からパッケージの保存場所を選択します。  
  
4.  保存場所が **[SQL Server]** または **[SSIS パッケージ ストア]** の場合、サーバー名を指定します。  
  
5.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]に保存する場合は、認証の種類を指定します。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 認証を使用する場合、ユーザー名とパスワードを指定します。  
  
6.  パッケージのパスを指定するには、パスを入力するか、参照ボタン **[...]** をクリックしてパッケージの場所を指定します。 パッケージの既定の名前は Package です。 必要に応じて、パッケージの名前をニーズに合う名前に更新します。  
  
     **[パッケージのパス]** オプションとして **[SQL Server]** を選択した場合、パッケージのパスは、 **msdb** 内の論理フォルダーとパッケージ名で構成されます。 たとえば、パッケージ DownloadMonthlyData が [MSDB] フォルダー ( **msdb**内のルート論理フォルダーの既定の名前) 内の [Finance] フォルダーと関連付けられている場合、DownloadMonthlyData という名前のパッケージのパッケージ パスは MSDB/Finance/DownloadMonthlyData になります。  
  
     **[パッケージのパス]** オプションとして **[SSIS パッケージ ストア]** を選択した場合、パッケージのパスは、Integration Services サービスが管理するフォルダーで構成されます。 たとえば、パッケージ UpdateDeductions が、Integration Services サービスが管理するファイル システム フォルダー内の [HumanResources] フォルダーに存在する場合、パッケージのパスは /File System/HumanResources/UpdateDeductions になります。同様に、パッケージ PostResumes が [MSDB] フォルダー内の [HumanResources] フォルダーに関連付けられている場合、パッケージのパスは MSDB/HumanResources/PostResumes になります。  
  
     **[パッケージのパス]** オプションとして **[ファイル システム]** を選択した場合、パッケージのパスは、ファイル システム内の場所とファイル名になります。 たとえば、パッケージ名が UpdateDemographics の場合、パッケージのパスは C:\HumanResources\Quarterly\UpdateDemographics.dtsx になります。  
  
7.  パッケージの保護レベルを確認します。  
  
8.  必要に応じて、 **[保護レベル]** ボックスの近くの参照ボタン **[...]** をクリックし、保護レベルを変更します。  
  
    -   **[パッケージの保護レベル]** ダイアログ ボックスで、別の保護レベルを選択します。  
  
    -   **[OK]** をクリックします。  
  
9. **[OK]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [Integration Services &#40;SSIS&#41; パッケージ](../../2014/integration-services/integration-services-ssis-packages.md)   
 [サービスをサービスの統合を構成する&#40;SSIS サービス&#41;](service/integration-services-service-ssis-service.md)  
  
  
