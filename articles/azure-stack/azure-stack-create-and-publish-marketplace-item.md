---
title: Azure Stack の Marketplace アイテムの作成と発行 | Microsoft Docs
description: Azure Stack にある Marketplace アイテムを作成および発行します。
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/08/2019
ms.author: sethm
ms.reviewer: avishwan
ms.lastreviewed: 01/08/2019
ms.openlocfilehash: 44cf5b2cc7547a4e85c65215fdc1e4fe2cb585a9
ms.sourcegitcommit: 898b2936e3d6d3a8366cfcccc0fccfdb0fc781b4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2019
ms.locfileid: "55243642"
---
# <a name="create-and-publish-a-marketplace-item"></a>Marketplace アイテムを作成および発行する

*適用対象:Azure Stack 統合システムと Azure Stack Development Kit*

## <a name="create-a-marketplace-item"></a>Marketplace アイテムの作成

1. [Azure Gallery Packager ツール](https://www.aka.ms/azurestackmarketplaceitem)およびサンプルの Azure Stack Marketplace アイテムをダウンロードします。
2. サンプルの Marketplace アイテムを開き、**SimpleVMTemplate** フォルダーの名前を変更します。 Marketplace アイテムと同じ名前 (**Contoso.TodoList** など) を使用します。 このフォルダーには、以下が格納されています。

   ```shell
   /Contoso.TodoList/
   /Contoso.TodoList/Manifest.json
   /Contoso.TodoList/UIDefinition.json
   /Contoso.TodoList/Icons/
   /Contoso.TodoList/Strings/
   /Contoso.TodoList/DeploymentTemplates/
   ```

3. [Azure Resource Manager テンプレートを作成する](../azure-resource-manager/resource-group-authoring-templates.md)か、GitHub からテンプレートを選択します。 Marketplace アイテムでは、このテンプレートを使用して新しいリソースを作成します。

    > [!Note]  
    > プロダクト キー、パスワード、お客様を特定できる情報などの機密情報を Azure Resource Manager テンプレートにハード コーディングしないでください。 テンプレート JSON ファイルは、ギャラリーで公開されると、認証の必要なくアクセスできます。 機密情報はすべて [Key Vault](../azure-resource-manager/resource-manager-keyvault-parameter.md) に格納し、テンプレート内から呼び出してください。

4. リソースを正常にデプロイできるようにするには、Microsoft Azure Stack API を使用してテンプレートをテストします。
5. テンプレートが仮想マシン イメージに依存する場合、指示に従って [Azure Stack に仮想マシン イメージを追加](azure-stack-add-vm-image.md)します。
6. Azure Resource Manager テンプレートを **/Contoso.TodoList/DeploymentTemplates/** フォルダーに保存します。
7. Marketplace アイテムのアイコンとテキストを選択します。 **Icons** フォルダーにアイコンを追加し、**Strings** フォルダー内の **resources** ファイルにテキストを追加します。 アイコンには **small**、**medium**、**large**、および **wide** の名前付け規則を使用します。 これらのサイズの詳細については、「[Marketplace アイテムの UI リファレンス](#reference-marketplace-item-ui)」を参照してください。

   > [!NOTE]
   > Marketplace アイテムを正しく構築するには、4 つすべてのアイコン サイズ (小、中、大、ワイド) が必要です。
   >
   >
8. **Manifest.json** ファイルで、**name** を Marketplace アイテムの名前に変更します。 さらに**発行者**を自分の名前または会社に変更します。
9. **artifacts** で、**name** と **path** を、追加した Azure Resource Manager テンプレートの正しい情報に変更します。

   ```json
   "artifacts": [
      {
          "name": "Your template name",
          "type": "Template",
          "path": "DeploymentTemplates\\your path",
          "isDefault": true
      }
   ```

10. **My Marketplace Items** を Marketplace アイテムを表示するカテゴリの一覧に置き換えます。

   ```json
   "categories":[
   "My Marketplace Items"
   ],
   ```

11. Manifest.json に対するその他の編集については、「[リファレンス: Marketplace アイテム manifest.json](#reference-marketplace-item-manifestjson)」を参照してください。

12. フォルダーを .azpkg ファイルにパッケージ化するには、コマンド プロンプトを開き、次のコマンドを実行します。

   ```shell
   AzureGalleryPackager.exe package –m <path to manifest.json> -o <output location for the package>
   ```

    > [!NOTE]
    > 出力パッケージへの完全パスが存在している必要があります。 たとえば、出力パスが C:\MarketPlaceItem\yourpackage.azpkg の場合は、C:\MarketPlaceItem フォルダーが存在する必要があります。
    >
    >

## <a name="publish-a-marketplace-item"></a>Marketplace アイテムの発行

1. PowerShell または Azure Storage Explorer を使用して、Marketplace アイテム (.azpkg) を Azure Blob Storage にアップロードします。 ローカルの Azure Stack ストレージにアップロードするか、またはパッケージの一時的な場所である Azure Storage にアップロードできます。 BLOB がパブリックにアクセスできることを確認します。
2. Microsoft Azure Stack 環境のクライアント仮想マシンで、PowerShell セッションがサービス管理者の資格情報を使用して設定されていることを確認します。 Azure Stack で PowerShell を認証する方法については、[PowerShell を使用したテンプレートのデプロイ](user/azure-stack-deploy-template-powershell.md)に関するページを参照してください。
3. [PowerShell 1.3.0](azure-stack-powershell-install.md) 以降を使用する場合、**Add-AzsGalleryItem** PowerShell コマンドレットを使用して Marketplace アイテムを Azure Stack に発行できます。 PowerShell 1.3.0 を使用する前は、**Add-AzsGalleryItem** の代わりに、**Add-AzureRMGalleryitem** コマンドレットを使用します。 たとえば、PowerShell 1.3.0 以降を使用する場合

   ```powershell
   Add-AzsGalleryItem -GalleryItemUri `
   https://sample.blob.core.windows.net/gallerypackages/Microsoft.SimpleTemplate.1.0.0.azpkg –Verbose
   ```

   | パラメーター | Description |
   | --- | --- |
   | SubscriptionID |管理者のサブスクリプション ID。 PowerShell を使用して取得できます。 ポータルで取得する場合は、プロバイダーのサブスクリプションに移動し、サブスクリプション ID をコピーします。 |
   | GalleryItemUri |ストレージに既にアップロードされた、ギャラリー パッケージの BLOB URI。 |
   | ApiVersion |**2015-04-01** と設定します。 |

4. ポータルに移動します。 これで、オペレーターまたはユーザーとして、ポータルで Marketplace アイテムを確認できます。 パッケージの表示には数分かかる場合があります。

5. これで Marketplace アイテムが Azure Stack Marketplace に保存されました。 Blob Storage の場所から削除することができます。
    > [!Caution]  
    > すべての既定のギャラリー アイテムと、カスタムのギャラリー アイテムは、次の URL での認証を使用せずにアクセスできるようになりました。  
`https://adminportal.[Region].[external FQDN]:30015/artifact/20161101/[Template Name]/DeploymentTemplates/Template.json`
`https://portal.[Region].[external FQDN]:30015/artifact/20161101/[Template Name]/DeploymentTemplates/Template.json`
`https://systemgallery.blob.[Region].[external FQDN]/dev20161101-microsoft-windowsazure-gallery/[Template Name]/UiDefinition.json`

6. Marketplace アイテムを削除するには、**Remove-AzureRMGalleryItem** コマンドレットを使用します。 例: 

   ```powershell
   Remove-AzsGalleryItem -Name Microsoft.SimpleTemplate.1.0.0  –Verbose
   ```

   > [!NOTE]
   > アイテムを削除した後に Marketplace UI でエラーが表示される可能性があります。 このエラーを解決するには、ポータルで **[設定]** をクリックします。 次に、**[ポータルのカスタマイズ]** で **[変更を破棄する]** を選択します。
   >
   >

## <a name="reference-marketplace-item-manifestjson"></a>リファレンス: Marketplace アイテム manifest.json

### <a name="identity-information"></a>ID 情報

| Name | 必須 | type | 制約 | Description |
| --- | --- | --- | --- | --- |
| Name |X |String |[A-Za-z0-9]+ | |
| Publisher |X |String |[A-Za-z0-9]+ | |
| Version |X |String |[SemVer v2](https://semver.org/) | |

### <a name="metadata"></a>Metadata

| Name | 必須 | type | 制約 | Description |
| --- | --- | --- | --- | --- |
| DisplayName |X |String |推奨 80 文字 |80 文字より長い場合、ポータルでアイテム名が適切に表示されないことがあります。 |
| PublisherDisplayName |X |String |推奨 30 文字 |30 文字より長い場合、ポータルで発行者名が適切に表示されないことがあります。 |
| PublisherLegalName |X |String |最大 256 文字 | |
| Summary |X |String |60 ～ 100 文字 | |
| LongSummary |X |String |140 ～ 256 文字 |Azure Stack ではまだ適用なし。 |
| Description |X |[HTML](https://auxdocs.azurewebsites.net/en-us/documentation/articles/gallery-metadata#html-sanitization) |500 ～ 5,000 文字 | |

### <a name="images"></a>イメージ

Marketplace では、次のアイコンを使用します。

| Name | 幅 | 高さ | メモ |
| --- | --- | --- | --- |
| Wide |255 px |115 px |常に必要 |
| Large |115 px |115 px |常に必要 |
| Medium |90 px |90 px |常に必要 |
| Small |40 px |40 px |常に必要 |
| Screenshot |533 px |32 px |省略可能 |

### <a name="categories"></a>Categories

Marketplace の各アイテムは、そのアイテムのポータル UI における表示場所を識別するカテゴリでタグ付けする必要があります。 Azure Stack 内の既存のカテゴリのいずれか (コンピューティング、データ + ストレージなど) を選択するか、新しいものを選択します。

### <a name="links"></a>リンク

各 Marketplace アイテムには、追加コンテンツへのさまざまなリンクを含めることができます。 これらのリンクは、次の名前と URI の一覧として指定されます。

| Name | 必須 | type | 制約 | Description |
| --- | --- | --- | --- | --- |
| DisplayName |X |String |最大 64 文字 | |
| Uri |X |URI | | |

### <a name="additional-properties"></a>追加のプロパティ

前述のメタデータに加えて、Marketplace 作成者は次の形式でカスタムのキー/値のペアでデータを指定することができます。

| Name | 必須 | type | 制約 | Description |
| --- | --- | --- | --- | --- |
| DisplayName |X |String |最大 25 文字 | |
| Value |X |String |最大 30 文字 | |

### <a name="html-sanitization"></a>HTML のサニタイズ

HTML を許可するフィールドでは、次の要素と属性が許可されます。

`h1, h2, h3, h4, h5, p, ol, ul, li, a[target|href], br, strong, em, b, i`

## <a name="reference-marketplace-item-ui"></a>リファレンス: Marketplace アイテムの UI

Azure Stack ポータルで表示される Marketplace アイテムのアイコンとテキストは、次のとおりです。

### <a name="create-blade"></a>[作成] ブレード

![[作成] ブレード](media/azure-stack-marketplace-item-ui-reference/image1.png)

### <a name="marketplace-item-details-blade"></a>[Marketplace item details (Marketplace アイテムの詳細)] ブレード

![[Marketplace item details (Marketplace アイテムの詳細)] ブレード](media/azure-stack-marketplace-item-ui-reference/image3.png)
