---
title: パッケージのコピーの保存 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.savecopyas.f1
helpviewer_keywords:
- Save Copy of Package dialog box
ms.assetid: 7b44c0d7-d8fa-4491-8836-0899f621d3a8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 649c972b001a0627a568f0bd9e1ac2b42d5175ce
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66056319"
---
# <a name="save-copy-of-package"></a>[パッケージのコピーの保存]
  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] の **[パッケージのコピーの保存]** ダイアログ ボックスを使用すると、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージのコピーを [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] から別の場所に保存し、必要に応じてパッケージの保護レベルを変更できます。  
  
## <a name="options"></a>および  
 **[パッケージの場所]**  
 パッケージ コピーを保存する格納場所の種類を選択します。 使用できるオプションは以下のとおりです。  
  
 **SQL Server**  
  
 **[ファイル システム]**  
  
 **[SSIS パッケージ ストア]**  
  
 **[サーバー]**  
 サーバー名を入力するか、サーバーを一覧から選択します。 このオプションは、格納場所が **[SQL Server]** または **[SSIS パッケージ ストア]** の場合のみ使用できます。  
  
 **[認証]**  
 Windows 認証または [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 認証を選択します。 このオプションは、格納場所が [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の場合のみ使用できます。  
  
> [!IMPORTANT]  
>  可能であれば、Windows 認証を使用します。  
  
 **認証の種類**  
 認証の種類を選択します。  
  
 **ユーザー名**  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 認証を使用する場合は、ユーザー名を指定します。  
  
 **Password**  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 認証を使用する場合は、パスワードを指定します。  
  
 **[パッケージのパス]**  
 パッケージのパスを入力するか、[参照] をクリックして **([...])** ボタンをクリックし、パッケージを格納するフォルダーを探します。  
  
 **保護レベル**  
 参照 をクリックして **(...)** ボタンをクリックしで保護レベルを更新、**パッケージの保護レベル** ダイアログ ボックス。 詳細については、「 [[パッケージの保護レベル] ダイアログ ボックス](../../2014/integration-services/package-and-project-protection-level-dialog-box.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [[パッケージのインポート] ダイアログ ボックスの UI リファレンス](../../2014/integration-services/import-package-dialog-box-ui-reference.md)   
 [[パッケージのエクスポート] ダイアログ ボックスの UI リファレンス](../../2014/integration-services/export-package-dialog-box-ui-reference.md)   
 [パッケージを保存する](save-packages.md)   
 [パッケージをインポートおよびエクスポートする &#40;SSIS サービス&#41;](../../2014/integration-services/import-and-export-packages-ssis-service.md)  
  
  
