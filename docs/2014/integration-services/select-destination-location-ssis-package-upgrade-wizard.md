---
title: アップグレード先の場所 (SSIS パッケージ アップグレード ウィザード) を選択します |。Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.is.upgradewizard.selectdestinationlocation.f1
ms.assetid: 89274a71-0ffe-4889-84df-f5a7d78459ef
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d891f456f9c4922b3c680913f767d4e9b14a76a0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66056007"
---
# <a name="select-destination-location-ssis-package-upgrade-wizard"></a>[アップグレード先の場所を選択] (SSIS パッケージ アップグレード ウィザード)
  **[アップグレード先の場所を選択]** ページを使用すると、アップグレードされたパッケージの保存先を指定できます。  
  
> [!NOTE]  
>  このページは、 [!INCLUDE[ssIS](../includes/ssis-md.md)] パッケージ アップグレード ウィザードを [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] またはコマンド プロンプトから実行した場合にのみ使用できます。  
  
 **SSIS パッケージ アップグレード ウィザードを実行するには**  
  
-   [SSIS パッケージ アップグレード ウィザードを使用した Integration Services パッケージのアップグレード](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)  
  
## <a name="static-options"></a>静的オプション  
 **[アップグレード元の場所に保存する]**  
 ウィザードの **[ソースの場所を選択]** ページで指定した場所と同じ場所に、アップグレードされたパッケージを保存します。  
  
 元のパッケージがファイル システムに格納されている場合に、ウィザードでそれらのパッケージをバックアップするには、 **[ソースの場所に保存]** オプションを選択します。 詳細については、「 [SSIS パッケージ アップグレード ウィザードを使用した Integration Services パッケージのアップグレード](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)」を参照してください。  
  
 **[新しいアップグレード先の場所を選択]**  
 このページで指定したアップグレード先の場所に、アップグレードされたパッケージを保存します。  
  
 **[パッケージ ソース]**  
 アップグレード パッケージが格納される場所を指定します。 このオプションには、次の表に示す値があります。  
  
|値|説明|  
|-----------|-----------------|  
|**[ファイル システム]**|アップグレードされたパッケージをローカル コンピューター上のフォルダーに保存することを示します。|  
|**[SSIS パッケージ ストア]**|アップグレードされたパッケージを Integration Services パッケージ ストア内に保存することを示します。 パッケージ ストアは、Integration Services サービスが管理するファイル システム フォルダーのセットで構成されます。 詳細については、「[パッケージの管理 &#40;SSIS サービス&#41;](service/package-management-ssis-service.md)」を参照してください。<br /><br /> この値を選択すると、対応する**パッケージ ソース**動的オプションが表示されます。|  
|**Microsoft SQL Server**|アップグレードされたパッケージを [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の既存のインスタンスに保存することを示します。<br /><br /> この値を選択すると、対応する **パッケージ ソース** 動的オプションが表示されます。|  
  
 **フォルダー**  
 アップグレードされたパッケージを保存するフォルダーの名前を入力するか、 **[参照]** をクリックしてフォルダーを指定します。  
  
 **[参照]**  
 アップグレードされたパッケージを保存するフォルダーを、参照して指定します。  
  
## <a name="package-source-dynamic-options"></a>パッケージ ソース動的オプション  
  
### <a name="package-source--ssis-package-store"></a>[パッケージ ソース] = [SSIS パッケージ ストア]  
 **[サーバー]**  
 アップグレード パッケージを保存するサーバーの名前を入力するか、一覧からサーバーを選択します。  
  
### <a name="package-source--microsoft-sql-server"></a>[パッケージ ソース] = [Microsoft SQL Server]  
 **[サーバー]**  
 アップグレード パッケージを保存するサーバーの名前を入力するか、一覧からこのサーバーを選択します。  
  
 **[Windows 認証を使用する]**  
 Windows 認証を使用してサーバーに接続する場合に選択します。  
  
 **[SQL Server 認証を使用する]**  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 認証を使用してサーバーに接続する場合に選択します。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 認証を使用する場合は、ユーザー名とパスワードを入力する必要があります。  
  
 **ユーザー名**  
 サーバーへの接続時に [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 認証で使用するユーザー名を入力します。  
  
 **Password**  
 サーバーへの接続時に [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 認証で使用するパスワードを入力します。  
  
## <a name="see-also"></a>参照  
 [Integration Services パッケージのアップグレード](install-windows/upgrade-integration-services-packages.md)  
  
  
