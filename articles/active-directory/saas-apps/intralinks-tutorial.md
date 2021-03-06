---
title: チュートリアル:Azure Active Directory と Intralinks の統合 | Microsoft Docs
description: Azure Active Directory と Intralinks の間でシングル サインオンを構成する方法について説明します。
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: 147f2bf9-166b-402e-adc4-4b19dd336883
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 41aac9c64922a3d551ae685bb5b642bf72dd52b2
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/13/2019
ms.locfileid: "56166225"
---
# <a name="tutorial-azure-active-directory-integration-with-intralinks"></a>チュートリアル:Azure Active Directory と Intralinks の統合

このチュートリアルでは、Intralinks と Azure Active Directory (Azure AD) を統合する方法について説明します。

Intralinks と Azure AD の統合には、次の利点があります。

- Intralinks にアクセスする Azure AD ユーザーを制御できます。
- ユーザーが自分の Azure AD アカウントで自動的に Intralinks にサインオン (シングル サインオン) できるようにします。
- 1 つの中央サイト (Azure Portal) でアカウントを管理できます

SaaS アプリと Azure AD の統合の詳細については、「[Azure Active Directory のアプリケーション アクセスとシングル サインオンとは](../manage-apps/what-is-single-sign-on.md)」をご覧ください。

## <a name="prerequisites"></a>前提条件

Intralinks と Azure AD の統合を構成するには、次のものが必要です。

- Azure AD サブスクリプション
- Intralinks でのシングル サインオンが有効なサブスクリプション

> [!NOTE]
> このチュートリアルの手順をテストする場合、運用環境を使用しないことをお勧めします。

このチュートリアルの手順をテストするには、次の推奨事項に従ってください。

- 必要な場合を除き、運用環境は使用しないでください。
- Azure AD の評価環境がない場合は、 [こちら](https://azure.microsoft.com/pricing/free-trial/)から 1 か月の評価版を入手できます。

## <a name="scenario-description"></a>シナリオの説明
このチュートリアルでは、テスト環境で Azure AD のシングル サインオンをテストします。 このチュートリアルで説明するシナリオは、主に次の 2 つの要素で構成されています。

1. ギャラリーからの Intralinks の追加
1. Azure AD シングル サインオンの構成とテスト

## <a name="adding-intralinks-from-the-gallery"></a>ギャラリーからの Intralinks の追加
Azure AD への Intralinks の統合を構成するには、ギャラリーから管理対象 SaaS アプリの一覧に Intralinks を追加する必要があります。

**ギャラリーから Intralinks を追加するには、次の手順に従います。**

1. **[Azure Portal](https://portal.azure.com)** の左側のナビゲーション ウィンドウで、**[Azure Active Directory]** アイコンをクリックします。 

    ![Active Directory][1]

1. **[エンタープライズ アプリケーション]** に移動します。 次に、**[すべてのアプリケーション]** に移動します。

    ![[アプリケーション]][2]
    
1. 新しいアプリケーションを追加するには、ダイアログの上部にある **[新しいアプリケーション]** をクリックします。

    ![[アプリケーション]][3]

1. 検索ボックスに、「 **Intralinks**」と入力します。

    ![Azure AD のテスト ユーザーの作成](./media/intralinks-tutorial/tutorial_intralinks_search.png)

1. 結果パネルで **[Intralinks]** を選び、**[追加]** をクリックして、アプリケーションを追加します。

    ![Azure AD のテスト ユーザーの作成](./media/intralinks-tutorial/tutorial_intralinks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Azure AD シングル サインオンの構成とテスト
このセクションでは、"Britta Simon" というテスト ユーザーに基づいて、Intralinks で Azure AD のシングル サインオンを構成し、テストします。

シングル サインオンを機能させるには、Azure AD ユーザーに対応する Intralinks ユーザーが Azure AD で認識されている必要があります。 言い換えると、Azure AD ユーザーと Intralinks の関連ユーザーの間で、リンク関係が確立されている必要があります。

Intralinks で、Azure AD の **[ユーザー名]** の値を **[Username]** の値として割り当ててリンク関係を確立します。

Intralinks で Azure AD のシングル サインオンを構成してテストするには、次の構成要素を完了する必要があります。

1. **[Azure AD シングル サインオンの構成](#configuring-azure-ad-single-sign-on)** - ユーザーがこの機能を使用できるようにします。
1. **[Azure AD のテスト ユーザーの作成](#creating-an-azure-ad-test-user)** - Britta Simon で Azure AD のシングル サインオンをテストします。
1. **[Intralinks テスト ユーザーの作成](#creating-an-intralinks-test-user)** - Intralinks で Britta Simon に対応するユーザーを作成し、Azure AD の Britta Simon にリンクさせます。
1. **[Azure AD テスト ユーザーの割り当て](#assigning-the-azure-ad-test-user)** - Britta Simon が Azure AD のシングル サインオンを使用できるようにします。
1. **[シングル サインオンのテスト](#testing-single-sign-on)** - 構成が機能するかどうかを確認します。

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD シングル サインオンの構成

このセクションでは、Azure Portal で Azure AD のシングル サインオンを有効にして、Intralinks アプリケーションでシングル サインオンを構成します。

**Intralinks で Azure AD シングル サインオンを構成するには、次の手順に従います。**

1. Azure Portal の **Intralinks** アプリケーション統合ページで、**[シングル サインオン]** をクリックします。

    ![Configure single sign-on][4]

1. **[シングル サインオン]** ダイアログで、**[モード]** として **[SAML ベースのサインオン]** を選択し、シングル サインオンを有効にします。
 
    ![Configure single sign-on](./media/intralinks-tutorial/tutorial_intralinks_samlbase.png)

1. **[Intralinks のドメインと URL]** セクションで、次の手順を実行します。

    ![Configure single sign-on](./media/intralinks-tutorial/tutorial_intralinks_url.png)

    **[サインオン URL]** ボックスに、`https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>` のパターンを使用して URL を入力します。

    > [!NOTE] 
    > これは実際の値ではありません。 実際のサインオン URL でこの値を更新してください。 この値を取得するには、[Intralinks クライアント サポート チーム](https://www.intralinks.com/contact)にお問い合わせください。 
 
1. **[SAML 署名証明書]** セクションで、**[Metadata XML (メタデータ XML)]** をクリックし、コンピューターにメタデータ ファイルを保存します。

    ![Configure single sign-on](./media/intralinks-tutorial/tutorial_intralinks_certificate.png) 

1. **[保存]** ボタンをクリックします。

    ![Configure single sign-on](./media/intralinks-tutorial/tutorial_general_400.png)

1. **Intralinks** 側にシングル サインオンを構成するには、ダウンロードした**メタデータ XML** を [Intralinks サポート チーム](https://www.intralinks.com/contact)に送信する必要があります。 サポート チームはこれを設定して、SAML SSO 接続が両方の側で正しく設定されるようにします。

> [!TIP]
> アプリのセットアップ中、[Azure Portal](https://portal.azure.com) 内で上記の手順の簡易版を確認できるようになりました。  **[Active Directory] の [エンタープライズ アプリケーション]** セクションからこのアプリを追加した後、**[シングル サインオン]** タブをクリックし、一番下の **[構成]** セクションから組み込みドキュメントにアクセスするだけです。 埋め込みドキュメント機能の詳細については、[Azure AD の埋め込みドキュメント]( https://go.microsoft.com/fwlink/?linkid=845985)に関するページを参照してください。

### <a name="creating-an-azure-ad-test-user"></a>Azure AD のテスト ユーザーの作成
このセクションの目的は、Azure Portal で Britta Simon というテスト ユーザーを作成することです。

![Azure AD ユーザーの作成][100]

**Azure AD でテスト ユーザーを作成するには、次の手順に従います。**

1. **Azure Portal** の左側のナビゲーション ウィンドウで、**[Azure Active Directory]** アイコンをクリックします。

    ![Azure AD のテスト ユーザーの作成](./media/intralinks-tutorial/create_aaduser_01.png) 

1. **[ユーザーとグループ]** に移動し、**[すべてのユーザー]** をクリックして、ユーザーの一覧を表示します。
    
    ![Azure AD のテスト ユーザーの作成](./media/intralinks-tutorial/create_aaduser_02.png) 

1. ダイアログの上部にある **[追加]** をクリックして、**[ユーザー]** ダイアログを開きます。
 
    ![Azure AD のテスト ユーザーの作成](./media/intralinks-tutorial/create_aaduser_03.png) 

1. **[ユーザー]** ダイアログ ページで、次の手順を実行します。
 
    ![Azure AD のテスト ユーザーの作成](./media/intralinks-tutorial/create_aaduser_04.png) 

    a. **[名前]** ボックスに「**BrittaSimon**」と入力します。

    b. **[ユーザー名]** ボックスに BrittaSimon の**電子メール アドレス**を入力します。

    c. **[パスワードを表示]** を選択し、**[パスワード]** の値をメモします。

    d.[Tableau Server return URL]: Tableau Server ユーザーがアクセスする URL。 **Create** をクリックしてください。
 
### <a name="creating-an-intralinks-test-user"></a>Intralinks テスト ユーザーの作成

このセクションでは、Intralinks で Britta Simon というユーザーを作成します。 Intralinks プラットフォームにユーザーを追加する方法については、[Intralinks サポート チーム](https://www.intralinks.com/contact)にお問い合わせください。

### <a name="assigning-the-azure-ad-test-user"></a>Azure AD テスト ユーザーの割り当て

このセクションでは、Britta Simon に Intralinks へのアクセスを許可することで、このユーザーが Azure シングル サインオンを使用できるようにします。

![ユーザーの割り当て][200] 

**Intralinks に Britta Simon を割り当てるには、次の手順に従います。**

1. Azure Portal でアプリケーション ビューを開き、ディレクトリ ビューに移動します。次に、**[エンタープライズ アプリケーション]** に移動し、**[すべてのアプリケーション]** をクリックします。

    ![ユーザーの割り当て][201] 

1. アプリケーションの一覧で **[Intralinks]** を選択します。

    ![Configure single sign-on](./media/intralinks-tutorial/tutorial_intralinks_app.png) 

1. 左側のメニューで **[ユーザーとグループ]** をクリックします。

    ![ユーザーの割り当て][202] 

1. **[追加]** ボタンをクリックします。 次に、**[割り当ての追加]** ダイアログで **[ユーザーとグループ]** を選択します。

    ![ユーザーの割り当て][203]

1. **[ユーザーとグループ]** ダイアログで、ユーザーの一覧から **[Britta Simon]** を選択します。

1. **[ユーザーとグループ]** ダイアログで **[選択]** をクリックします。

1. **[割り当ての追加]** ダイアログで **[割り当て]** ボタンをクリックします。

### <a name="add-intralinks-via-or-elite-application"></a>Intralinks VIA または Elite アプリケーションの追加

Intralinks では、Deal Nexus アプリケーションを除くその他すべての Intralinks アプリケーションで、同じ SSO ID プラットフォームを使用します。 Intralinks の他のアプリケーションを使用する予定の場合、最初に上述の手順に従って 1 つのプライマリ Intralinks アプリケーションに対して SSO を構成する必要があります。

その後、後述の手順に従ってテナントに別の Intralinks アプリケーションを追加し、このテナントでプライマリ アプリケーションを SSO で利用できます。 

>[!NOTE]
>この機能は、Azure AD "Premium" SKU のお客様のみ使用できます。"無料" SKU または "Basic" SKU のお客様は使用できません。

1. **[Azure Portal](https://portal.azure.com)** の左側のナビゲーション ウィンドウで、**[Azure Active Directory]** アイコンをクリックします。 

    ![Active Directory][1]


1. **[エンタープライズ アプリケーション]** に移動します。 次に、**[すべてのアプリケーション]** に移動します。

    ![[アプリケーション]][2]
    
1. 新しいアプリケーションを追加するには、ダイアログの上部にある **[新しいアプリケーション]** をクリックします。

    ![[アプリケーション]][3]

1. 検索ボックスに、「 **Intralinks**」と入力します。

    ![Azure AD のテスト ユーザーの作成](./media/intralinks-tutorial/tutorial_intralinks_search.png)

1. **[Intralinks Add アプリ]** で、次の手順を実行します。

    ![Intralinks VIA または Elite アプリケーションの追加](./media/intralinks-tutorial/tutorial_intralinks_addapp.png)

    a. **[名前]** ボックスに、「**Intralinks Elite**」など、適切なアプリケーションの名前を入力します。

    b. **[追加]** ボタンをクリックします。

1.  Azure Portal の **Intralinks** アプリケーション統合ページで、**[シングル サインオン]** をクリックします。

    ![Configure single sign-on][4]

1. **[シングル サインオン]** ダイアログで、**[モード]** として **[リンクされたサインオン]** を選択します。
 
    ![Configure single sign-on](./media/intralinks-tutorial/tutorial_intralinks_linkedsignon.png)

1. 他の Intralinks アプリケーションの [Intralinks チーム](https://www.intralinks.com/contact)から SP によって開始される SSO URL を取得し、その URL を **[サインオン URL の構成]** に以下のように入力します。 
    
     ![Configure single sign-on](./media/intralinks-tutorial/tutorial_intralinks_customappurl.png)
    
     [サインオン URL] ボックスで、ユーザーが Intralinks アプリケーションへのサインオンに使用する URL を次の形式で入力します。
   
    `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`

1. **[保存]** ボタンをクリックします。

    ![Configure single sign-on](./media/intralinks-tutorial/tutorial_general_400.png)

1. 「**[Azure AD テスト ユーザーの割り当て](#assigning-the-azure-ad-test-user)**」セクションの手順に従って、アプリケーションをユーザーまたはグループに割り当てます。

### <a name="testing-single-sign-on"></a>シングル サインオンのテスト

このセクションでは、アクセス パネルを使用して Azure AD のシングル サインオン構成をテストします。

アクセス パネルで Intralinks のタイルをクリックすると、自動的に Intralinks アプリケーションにサインオンします。
アクセス パネルの詳細については、[アクセス パネルの概要](../user-help/active-directory-saas-access-panel-introduction.md)に関する記事を参照してください。

## <a name="additional-resources"></a>その他のリソース

* [SaaS アプリと Azure Active Directory を統合する方法に関するチュートリアルの一覧](tutorial-list.md)
* [Azure Active Directory のアプリケーション アクセスとシングル サインオンとは](../manage-apps/what-is-single-sign-on.md)


<!--Image references-->

[1]: ./media/intralinks-tutorial/tutorial_general_01.png
[2]: ./media/intralinks-tutorial/tutorial_general_02.png
[3]: ./media/intralinks-tutorial/tutorial_general_03.png
[4]: ./media/intralinks-tutorial/tutorial_general_04.png

[100]: ./media/intralinks-tutorial/tutorial_general_100.png

[200]: ./media/intralinks-tutorial/tutorial_general_200.png
[201]: ./media/intralinks-tutorial/tutorial_general_201.png
[202]: ./media/intralinks-tutorial/tutorial_general_202.png
[203]: ./media/intralinks-tutorial/tutorial_general_203.png

