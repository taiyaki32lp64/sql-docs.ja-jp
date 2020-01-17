---
title: ソースの場所 (SSIS パッケージ アップグレード ウィザード) を選択します |。Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.is.upgradewizard.selectsourcelocation.f1
ms.assetid: 429f146e-edb4-4401-a225-f2c8468971c5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1ba348d3a47945bf9bb4f375310c5c92e6be7705
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66055942"
---
# <a name="select-source-location-ssis-package-upgrade-wizard"></a>[ソースの場所を選択] (SSIS パッケージ アップグレード ウィザード)
  **[ソースの場所を選択]** ページを使用すると、パッケージのアップグレード元を指定できます。  
  
> [!NOTE]  
>  このページは、 [!INCLUDE[ssIS](../includes/ssis-md.md)] パッケージ アップグレード ウィザードを [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] またはコマンド プロンプトから実行した場合にのみ使用できます。  
  
 **SSIS パッケージ アップグレード ウィザードを実行するには**  
  
-   [SSIS パッケージ アップグレード ウィザードを使用した Integration Services パッケージのアップグレード](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)  
  
## <a name="static-options"></a>静的オプション  
 **[パッケージ ソース]**  
 アップグレードするパッケージが格納されている場所を選択します。 このオプションには、次の表に示す値があります。  
  
|値|説明|  
|-----------|-----------------|  
|**[ファイル システム]**|アップグレードするパッケージがローカル コンピューター上のフォルダーにあることを示します。<br /><br /> パッケージをアップグレードする前に元のパッケージをウィザードでバックアップするには、元のパッケージがファイル システムに格納されている必要があります。 詳細については、方法に関するトピックを参照してください。|  
|**[SSIS パッケージ ストア]**|アップグレードするパッケージがパッケージ ストア内にあることを示します。 パッケージ ストアは、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスが管理するファイル システム フォルダーのセットで構成されます。 詳細については、「[パッケージの管理 (SSIS サービス)](service/package-management-ssis-service.md)」を参照してください。<br /><br /> この値を選択すると、対応する**パッケージ ソース**動的オプションが表示されます。|  
|**Microsoft SQL Server**|アップグレードするパッケージが [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の既存のインスタンス内にあることを示します。<br /><br /> この値を選択すると、対応する**パッケージ ソース**動的オプションが表示されます。|  
  
 **フォルダー**  
 アップグレードするパッケージが格納されているフォルダーの名前を入力するか、 **[参照]** をクリックしてフォルダーを指定します。  
  
 **[参照]**  
 アップグレードするパッケージが格納されているフォルダーを参照して指定します。  
  
## <a name="package-source-dynamic-options"></a>パッケージ ソース動的オプション  
  
### <a name="package-source--ssis-package-store"></a>[パッケージ ソース] = [SSIS パッケージ ストア]  
 **[サーバー]**  
 アップグレードするパッケージが存在するサーバーの名前を入力するか、一覧からこのサーバーを選択します。  
  
### <a name="package-source--microsoft-sql-server"></a>[パッケージ ソース] = [Microsoft SQL Server]  
 **[サーバー]**  
 アップグレードするパッケージが存在するサーバーの名前を入力するか、一覧からこのサーバーを選択します。  
  
 **[Windows 認証を使用する]**  
 Windows 認証を使用してサーバーに接続する場合に選択します。  
  
 **[SQL Server 認証を使用する]**  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 認証を使用してサーバーに接続する場合に選択します。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 認証を使用する場合は、ユーザー名とパスワードを入力する必要があります。  
  
 **ユーザー名**  
 サーバーへの接続時に [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 認証で使用するユーザー名を入力します。  
  
 **Password**  
 サーバーへの接続時に [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 認証で使用するパスワードを入力します。  
  
## <a name="see-also"></a>関連項目  
 [Integration Services パッケージのアップグレード](install-windows/upgrade-integration-services-packages.md)  
  
  
