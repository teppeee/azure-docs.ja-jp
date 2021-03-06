---
title: インクルード ファイル
description: インクルード ファイル
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mtillman
editor: ''
ms.service: active-directory
ms.devlang: na
ms.topic: include
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 09/17/2018
ms.author: andret
ms.custom: include file
ms.openlocfilehash: f3048daa7d597d92041733cdf5c6f299cebc2f73
ms.sourcegitcommit: 0f54b9dbcf82346417ad69cbef266bc7804a5f0e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/26/2018
ms.locfileid: "50142796"
---
## <a name="configure-your-aspnet-web-app-with-the-applications-registration-information"></a>アプリケーションの登録情報を使用した ASP.NET Web アプリの構成

この手順では、SSL を使用するようにプロジェクトを構成した後、SSL URL を使用してアプリケーションの登録情報を構成します。 その後、*web.config* を介して、アプリケーションの登録情報をソリューションに追加します。

1. ソリューション エクスプローラーで、プロジェクト選択して [`Properties`] \(プロパティ) ウィンドウを確認します ([プロパティ] ウィンドウが表示されない場合は F4 キーを押します)。
2. `SSL Enabled` を `True` に変更します。
3. 上の画像にある [`SSL URL`] の値をコピーしてこのページの最上部にある [`Redirect URL`] \(リダイレクト URL) フィールドに貼り付け、*[更新]* をクリックします。<br/><br/>![プロジェクトのプロパティ](media/active-directory-develop-guidedsetup-aspnetwebapp-configure/vsprojectproperties.png)<br />
4. `configuration\appSettings` セクションのルート フォルダーにあるファイル `web.config` に、以下のコードを追加します。

```xml
<add key="ClientId" value="[Enter the application Id here]" />
<add key="RedirectUri" value="[Enter the Redirect URL here]" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
