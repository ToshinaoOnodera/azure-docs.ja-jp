---
title: チュートリアル:Azure Active Directory と Zscaler Private Access Administrator の統合 | Microsoft Docs
description: Azure Active Directory と Zscaler Private Access Administrator の間でシングル サインオンを構成する方法について説明します。
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: barbkess
ms.assetid: c87392a7-e7fe-4cdc-a8e6-afe1ed975172
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 04/03/2019
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: ce75431de24886c038cd2eb4ee7db02d2b6cde31
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "65864915"
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-private-access-administrator"></a>チュートリアル:Azure Active Directory と Zscaler Private Access Administrator の統合

このチュートリアルでは、Zscaler Private Access Administrator と Azure Active Directory (Azure AD) を統合する方法について説明します。
Zscaler Private Access Administrator と Azure AD の統合には、次の利点があります。

* Zscaler Private Access Administrator にアクセスする Azure AD ユーザーを制御できます。
* ユーザーが自分の Azure AD アカウントで Zscaler Private Access Administrator に自動的にサインイン (シングル サインオン) するように設定できます。
* 1 つの中央サイト (Azure Portal) でアカウントを管理できます。

SaaS アプリと Azure AD の統合の詳細については、「 [Azure Active Directory のアプリケーション アクセスとシングル サインオンとは](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)」を参照してください。
Azure サブスクリプションをお持ちでない場合は、開始する前に[無料アカウントを作成](https://azure.microsoft.com/free/)してください。

## <a name="prerequisites"></a>前提条件

Zscaler Private Access Administrator と Azure AD の統合を構成するには、次のものが必要です。

* Azure AD サブスクリプション。 Azure AD の環境がない場合は、[無料アカウント](https://azure.microsoft.com/free/)を取得できます
* Zscaler Private Access Administrator でのシングル サインオンが有効なサブスクリプション

## <a name="scenario-description"></a>シナリオの説明

このチュートリアルでは、テスト環境で Azure AD のシングル サインオンを構成してテストします。

* Zscaler Private Access Administrator では **SP** Initiated SSO と **IDP** Initiated SSO がサポートされます

## <a name="adding-zscaler-private-access-administrator-from-the-gallery"></a>ギャラリーからの Zscaler Private Access Administrator の追加

Azure AD への Zscaler Private Access Administrator の統合を構成するには、ギャラリーから管理対象 SaaS アプリの一覧に Zscaler Private Access Administrator を追加する必要があります。

**ギャラリーから Zscaler Private Access Administrator を追加するには、次の手順を実行します。**

1. **[Azure Portal](https://portal.azure.com)** の左側のナビゲーション ウィンドウで、**[Azure Active Directory]** アイコンをクリックします。

    ![Azure Active Directory のボタン](common/select-azuread.png)

2. **[エンタープライズ アプリケーション]** に移動し、**[すべてのアプリケーション]** オプションを選択します。

    ![[エンタープライズ アプリケーション] ブレード](common/enterprise-applications.png)

3. 新しいアプリケーションを追加するには、ダイアログの上部にある **[新しいアプリケーション]** をクリックします。

    ![[新しいアプリケーション] ボタン](common/add-new-app.png)

4. 検索ボックスに「**Zscaler Private Access Administrator**」と入力し、結果パネルから **[Zscaler Private Access Administrator]** を選択してから **[追加]** ボタンをクリックしてアプリケーションを追加します。

    ![結果一覧の Zscaler Private Access Administrator](common/search-new-app.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Azure AD シングル サインオンの構成とテスト

このセクションでは、**Britta Simon** というテスト ユーザーに基づいて、Zscaler Private Access Administrator で Azure AD のシングル サインオンを構成し、テストします。
シングル サインオンを機能させるには、Azure AD ユーザーと Zscaler Private Access Administrator の関連ユーザーの間で、リンク関係が確立されている必要があります。

Zscaler Private Access Administrator で Azure AD のシングル サインオンを構成してテストするには、次の構成要素を完了する必要があります。

1. **[Azure AD シングル サインオンの構成](#configure-azure-ad-single-sign-on)** - ユーザーがこの機能を使用できるようにします。
2. **[Zscaler Private Access Administrator シングル サインオンの構成](#configure-zscaler-private-access-administrator-single-sign-on)** - アプリケーション側でシングル サインオン設定を構成します。
3. **[Azure AD のテスト ユーザーの作成](#create-an-azure-ad-test-user)** - Britta Simon で Azure AD のシングル サインオンをテストします。
4. **[Azure AD テスト ユーザーの割り当て](#assign-the-azure-ad-test-user)** - Britta Simon が Azure AD シングル サインオンを使用できるようにします。
5. **[Zscaler Private Access Administrator のテスト ユーザーの作成](#create-zscaler-private-access-administrator-test-user)** - Zscaler Private Access Administrator で Britta Simon に対応するユーザーを作成し、Azure AD の Britta Simon にリンクさせます。
6. **[シングル サインオンのテスト](#test-single-sign-on)** - 構成が機能するかどうかを確認します。

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD シングル サインオンの構成

このセクションでは、Azure portal 上で Azure AD のシングル サインオンを有効にします。

Zscaler Private Access Administrator で Azure AD シングル サインオンを構成するには、次の手順を実行します。

1. [Azure portal](https://portal.azure.com/) の **Zscaler Private Access Administrator** アプリケーション統合ページで、**[シングル サインオン]** を選択します。

    ![シングル サインオン構成のリンク](common/select-sso.png)

2. **[シングル サインオン方式の選択]** ダイアログで、**[SAML/WS-Fed]** モードを選択して、シングル サインオンを有効にします。

    ![シングル サインオン選択モード](common/select-saml-option.png)

3. **[SAML でシングル サインオンをセットアップします]** ページで、**[編集]** アイコンをクリックして **[基本的な SAML 構成]** ダイアログを開きます。

    ![基本的な SAML 構成を編集する](common/edit-urls.png)

4. **[基本的な SAML 構成]** セクションで、アプリケーションを **IDP** 開始モードで構成する場合は、次の手順を実行します。

    ![Zscaler Private Access Administrator のドメインと URL のシングル サインオン情報](common/idp-relay.png)

    a. **[識別子]** ボックスに、`https://<subdomain>.private.zscaler.com/auth/metadata` の形式で URL を入力します。

    b. **[応答 URL]** ボックスに、`https://<subdomain>.private.zscaler.com/auth/sso` のパターンを使用して URL を入力します

    c. **[追加の URL を設定します]** をクリックします。

    d. **[リレー状態]** テキスト ボックスに、URL `idpadminsso` を入力します

5.  **SP** 開始モードでアプリケーションを構成する場合は、次の手順を実行します。

    ![Zscaler Private Access Administrator のドメインと URL のシングル サインオン情報](common/both-signonurl.png)

    **[サインオン URL]** ボックスに、`https://<subdomain>.private.zscaler.com/auth/sso` という形式で URL を入力します。   

    > [!NOTE]
    > これらは実際の値ではありません。 実際の識別子、応答 URL、サインオン URL でこれらの値を更新します。 これらの値を取得するには、[Zscaler Private Access Administrator クライアント サポート チーム](https://help.zscaler.com/zpa-submit-ticket)に連絡してください。 Azure portal の **[基本的な SAML 構成]** セクションに示されているパターンを参照することもできます。

6. **[SAML でシングル サインオンをセットアップします]** ページの **[SAML 署名証明書]** セクションで、**[ダウンロード]** をクリックして、要件のとおりに指定したオプションから**フェデレーション メタデータ XML** をダウンロードして、お使いのコンピューターに保存します。

    ![証明書のダウンロードのリンク](common/metadataxml.png)

7. **[Zscaler Private Access Administrator のセットアップ]** セクションで、要件に従って適切な URL をコピーします。

    ![構成 URL のコピー](common/copy-configuration-urls.png)

    a. ログイン URL

    b. Azure AD 識別子

    c. ログアウト URL

### <a name="configure-zscaler-private-access-administrator-single-sign-on"></a>Zscaler Private Access Administrator のシングル サインオンの構成

1. 別の Web ブラウザー ウィンドウで、Zscaler Private Access Administrator 企業サイトに管理者としてサインインします。

2. 上部の **[Administration]** をクリックして **[AUTHENTICATION]** セクションに移動し、**[IdP Configuration]** をクリックします。

    ![Zscaler Private Access Administrator の管理](./media/zscalerprivateaccessadministrator-tutorial/tutorial_zscalerprivateaccessadministrator_admin.png)

3. 右上隅の **[Add IdP Configuration]** をクリックします。 

    ![Zscaler Private Access Administrator の addidp](./media/zscalerprivateaccessadministrator-tutorial/tutorial_zscalerprivateaccessadministrator_addpidp.png)

4. **[Add IdP Configuration]** ページで、次の手順に従います。
 
    ![Zscaler Private Access Administrator の idpselect](./media/zscalerprivateaccessadministrator-tutorial/tutorial_zscalerprivateaccessadministrator_idpselect.png)

    a. **[IdP Metadata File Upload]** フィールドの **[Select File]** をクリックして、Azure AD からダウンロードしたメタデータ ファイルをアップロードします。

    b. Azure AD から **IdP メタデータ** が読み取られ、以下に示すようにすべてのフィールド情報が設定されます。

    ![Zscaler Private Access Administrator の idpconfig](./media/zscalerprivateaccessadministrator-tutorial/idpconfig.png)

    c. **[Administrator]** として **[Single Sign On]** を選択します。

    d. **[Domains]** フィールドから自分のドメインを選択します。
    
    e. **[Save]** をクリックします。

### <a name="create-an-azure-ad-test-user"></a>Azure AD のテスト ユーザーの作成 

このセクションの目的は、Azure Portal で Britta Simon というテスト ユーザーを作成することです。

1. Azure portal の左側のウィンドウで、**[Azure Active Directory]**、**[ユーザー]**、**[すべてのユーザー]** の順に選択します。

    ![[ユーザーとグループ] と [すべてのユーザー] リンク](common/users.png)

2. 画面の上部にある **[新しいユーザー]** を選択します。

    ![[新しいユーザー] ボタン](common/new-user.png)

3. [ユーザーのプロパティ] で、次の手順を実行します。

    ![[ユーザー] ダイアログ ボックス](common/user-properties.png)

    a. **[名前]** フィールドに「**BrittaSimon**」と入力します。
  
    b. **[ユーザー名]** フィールドに「`brittasimon@yourcompanydomain.extension`」と入力します。 たとえば、BrittaSimon@contoso.com のように指定します。

    c. **[パスワードを表示]** チェック ボックスをオンにし、[パスワード] ボックスに表示された値を書き留めます。

    d. **Create** をクリックしてください。

### <a name="assign-the-azure-ad-test-user"></a>Azure AD テスト ユーザーの割り当て

このセクションでは、Britta Simon に Zscaler Private Access Administrator へのアクセスを許可することで、このユーザーが Azure シングル サインオンを使用できるようにします。

1. Azure portal 上で **[エンタープライズ アプリケーション]** を選択し、**[すべてのアプリケーション]** を選択してから、**[Zscaler Private Access Administrator]** を選択します。

    ![[エンタープライズ アプリケーション] ブレード](common/enterprise-applications.png)

2. アプリケーションの一覧で、**[Zscaler Private Access Administrator]** を選択します。

    ![アプリケーションの一覧の Zscaler Private Access Administrator リンク](common/all-applications.png)

3. 左側のメニューで **[ユーザーとグループ]** を選びます。

    ![[ユーザーとグループ] リンク](common/users-groups-blade.png)

4. **[ユーザーの追加]** をクリックし、**[割り当ての追加]** ダイアログで **[ユーザーとグループ]** を選択します。

    ![[割り当ての追加] ウィンドウ](common/add-assign-user.png)

5. **[ユーザーとグループ]** ダイアログの [ユーザー] の一覧で **[Britta Simon]** を選択し、画面の下部にある **[選択]** ボタンをクリックします。

6. SAML アサーション内に任意のロール値が必要な場合、**[ロールの選択]** ダイアログでユーザーに適したロールを一覧から選択し、画面の下部にある **[選択]** をクリッします。

7. **[割り当ての追加]** ダイアログで、**[割り当て]** ボタンをクリックします。

### <a name="create-zscaler-private-access-administrator-test-user"></a>Zscaler Private Access Administrator のテスト ユーザーの作成

Azure AD ユーザーが Zscaler Private Access Administrator にサインインできるようにするには、ユーザーを Zscaler Private Access Administrator にプロビジョニングする必要があります。 Zscaler Private Access Administrator の場合、プロビジョニングは手動で行います。

**ユーザー アカウントをプロビジョニングするには、次の手順に従います。**

1. 管理者として Zscaler Private Access Administrator の会社サイトにサインインします。

2. 上部の **[Administration]** をクリックして **[AUTHENTICATION]** セクションに移動し、**[IdP Configuration]** をクリックします。

    ![Zscaler Private Access Administrator の管理](./media/zscalerprivateaccessadministrator-tutorial/tutorial_zscalerprivateaccessadministrator_admin.png)

3. メニューの左側にある **[Administrators]** をクリックします。

    ![Zscaler Private Access Administrator の管理者](./media/zscalerprivateaccessadministrator-tutorial/tutorial_zscalerprivateaccessadministrator_adminstrator.png)

4. 右上隅の **[Add Administrator]** をクリックします。

    ![Zscaler Private Access Administrator の管理者の追加](./media/zscalerprivateaccessadministrator-tutorial/tutorial_zscalerprivateaccessadministrator_addadmin.png)

5. **[Add Administrator]** ページで、次の手順に従います。

    ![Zscaler Private Access Administrator のユーザー管理](./media/zscalerprivateaccessadministrator-tutorial/tutorial_zscalerprivateaccessadministrator_useradmin.png)

    a. **[Username]** ボックスに、ユーザーのメール (BrittaSimon@contoso.com など) を入力します。

    b. **[Password]** ボックスに、ユーザーのパスワードを入力します。

    c. **[Confirm Password]** ボックスに、パスワードを入力します。

    d. **[Role]** に **[Zscaler Private Access Administrator]** を選択します。

    e. **[メール]** ボックスに、ユーザーのメール (BrittaSimon@contoso.com など) を入力します。

    f. **[Phone]** ボックスに、電話番号を入力します。

    g. **[Timezone]** ボックスで、タイム ゾーンを選択します。

    h. **[Save]** をクリックします。

### <a name="test-single-sign-on"></a>シングル サインオンのテスト 

このセクションでは、アクセス パネルを使用して Azure AD のシングル サインオン構成をテストします。

アクセス パネルで Zscaler Private Access Administrator のタイルをクリックすると、SSO をセットアップする Zscaler Private Access Administrator に自動的にサインインします。 アクセス パネルの詳細については、[アクセス パネルの概要](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)に関する記事を参照してください。

## <a name="additional-resources"></a>その他のリソース

- [SaaS アプリと Azure Active Directory を統合する方法に関するチュートリアルの一覧](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)

- [Azure Active Directory のアプリケーション アクセスとシングル サインオンとは](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)

- [Azure Active Directory の条件付きアクセスとは](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)

