---
ms.openlocfilehash: 77f74be505d72c6c0fd55d5f2650e32d03d63348
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822831"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="2e77c-101">Dans cet exercice, vous allez étendre l’application de l’exercice précédent pour prendre en charge l’authentification avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e77c-101">In this exercise you will extend the application from the previous exercise to support authentication with Azure AD.</span></span> <span data-ttu-id="2e77c-102">Cela est nécessaire pour obtenir le jeton d’accès OAuth nécessaire pour appeler Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="2e77c-102">This is required to obtain the necessary OAuth access token to call the Microsoft Graph.</span></span> <span data-ttu-id="2e77c-103">Dans cette étape, vous allez intégrer la bibliothèque de la [bibliothèque d’authentification Microsoft](https://github.com/AzureAD/microsoft-authentication-library-for-js) dans l’application.</span><span class="sxs-lookup"><span data-stu-id="2e77c-103">In this step you will integrate the [Microsoft Authentication Library](https://github.com/AzureAD/microsoft-authentication-library-for-js) library into the application.</span></span>

1. <span data-ttu-id="2e77c-104">Créez un fichier dans le répertoire racine nommé **config.js** et ajoutez le code suivant.</span><span class="sxs-lookup"><span data-stu-id="2e77c-104">Create a new file in the root directory named **config.js** and add the following code.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/config.example.js" id="msalConfigSnippet":::

    <span data-ttu-id="2e77c-105">Remplacez `YOUR_APP_ID_HERE` par l’ID de l’application dans le portail d’inscription des applications.</span><span class="sxs-lookup"><span data-stu-id="2e77c-105">Replace `YOUR_APP_ID_HERE` with the application ID from the Application Registration Portal.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="2e77c-106">Si vous utilisez le contrôle de code source tel que git, il est maintenant recommandé d’exclure le **config.js** fichier du contrôle de code source afin d’éviter une fuite accidentelle de votre ID d’application.</span><span class="sxs-lookup"><span data-stu-id="2e77c-106">If you're using source control such as git, now would be a good time to exclude the **config.js** file from source control to avoid inadvertently leaking your app ID.</span></span>

1. <span data-ttu-id="2e77c-107">Ouvrez **auth.js** et ajoutez le code suivant au début du fichier.</span><span class="sxs-lookup"><span data-stu-id="2e77c-107">Open **auth.js** and add the following code to the beginning of the file.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/auth.js" id="authInitSnippet":::

## <a name="implement-sign-in"></a><span data-ttu-id="2e77c-108">Implémentation de la connexion</span><span class="sxs-lookup"><span data-stu-id="2e77c-108">Implement sign-in</span></span>

<span data-ttu-id="2e77c-109">Dans cette section, vous allez implémenter les `signIn` `signOut` fonctions et.</span><span class="sxs-lookup"><span data-stu-id="2e77c-109">In this section you'll implement the `signIn` and `signOut` functions.</span></span>

1. <span data-ttu-id="2e77c-110">Remplacez la fonction `signIn` existante par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="2e77c-110">Replace the existing `signIn` function with the following.</span></span>

    ```javascript
    async function signIn() {
      // Login
      try {
        // Use MSAL to login
        const authResult = await msalClient.loginPopup(msalRequest);
        console.log('id_token acquired at: ' + new Date().toString());
        // Save the account username, needed for token acquisition
        sessionStorage.setItem('msalAccount', authResult.account.username);
        // TEMPORARY
        updatePage(Views.error, {
          message: 'Login successful',
          debug: `Token: ${authResult.accessToken}`
        });
      } catch (error) {
        console.log(error);
        updatePage(Views.error, {
          message: 'Error logging in',
          debug: error
        });
      }
    }
    ```

    <span data-ttu-id="2e77c-111">Ce code temporaire affiche le jeton d’accès après une connexion réussie.</span><span class="sxs-lookup"><span data-stu-id="2e77c-111">This temporary code will display the access token after a successful login.</span></span>

1. <span data-ttu-id="2e77c-112">Remplacez la fonction `signOut` existante par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="2e77c-112">Replace the existing `signOut` function with the following.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/auth.js" id="signOutSnippet":::

1. <span data-ttu-id="2e77c-113">Enregistrez vos modifications et actualisez la page.</span><span class="sxs-lookup"><span data-stu-id="2e77c-113">Save your changes and refresh the page.</span></span> <span data-ttu-id="2e77c-114">Une fois connecté, un message d’erreur s’affiche pour afficher le jeton d’accès.</span><span class="sxs-lookup"><span data-stu-id="2e77c-114">After you sign in, you should see an error box that shows the access token.</span></span>

## <a name="get-the-users-profile"></a><span data-ttu-id="2e77c-115">Obtenir le profil de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="2e77c-115">Get the user's profile</span></span>

<span data-ttu-id="2e77c-116">Dans cette section, vous allez améliorer la `signIn` fonction permettant d’utiliser le jeton d’accès pour obtenir le profil de l’utilisateur à partir de Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="2e77c-116">In this section you'll improve the `signIn` function to use the access token to get the user's profile from Microsoft Graph.</span></span>

1. <span data-ttu-id="2e77c-117">Ajoutez la fonction suivante dans **auth.js** pour récupérer le jeton d’accès de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2e77c-117">Add the following function in **auth.js** to retrieve the user's access token.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/auth.js" id="getTokenSnippet":::

1. <span data-ttu-id="2e77c-118">Créez un fichier à la racine du projet nommé **graph.js** et ajoutez le code suivant.</span><span class="sxs-lookup"><span data-stu-id="2e77c-118">Create a new file in the root of the project named **graph.js** and add the following code.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="graphInitSnippet":::

    <span data-ttu-id="2e77c-119">Ce code crée un fournisseur d’autorisation qui encapsule la `getToken` méthode dans **auth.js** et initialise le client Graph avec ce fournisseur.</span><span class="sxs-lookup"><span data-stu-id="2e77c-119">This code creates an authorization provider that wraps the `getToken` method in **auth.js** , and initializes the Graph client with this provider.</span></span>

1. <span data-ttu-id="2e77c-120">Ajoutez la fonction suivante dans **graph.js** pour obtenir le profil de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2e77c-120">Add the following function in **graph.js** to get the user's profile.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="getUserSnippet":::

1. <span data-ttu-id="2e77c-121">Remplacez la fonction `signIn` existante par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="2e77c-121">Replace the existing `signIn` function with the following.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/auth.js" id="signInSnippet":::

1. <span data-ttu-id="2e77c-122">Enregistrez vos modifications et actualisez la page.</span><span class="sxs-lookup"><span data-stu-id="2e77c-122">Save your changes and refresh the page.</span></span> <span data-ttu-id="2e77c-123">Une fois que vous êtes connecté, vous devez revenir sur la page d’accueil, mais l’interface utilisateur doit changer pour indiquer que vous êtes connecté.</span><span class="sxs-lookup"><span data-stu-id="2e77c-123">After you sign in, you should end up back on the home page, but the UI should change to indicate that you are signed-in.</span></span>

    ![Capture d’écran de la page d’accueil après la connexion](./images/user-signed-in.png)

1. <span data-ttu-id="2e77c-125">Cliquez sur Avatar de l’utilisateur dans le coin supérieur droit pour accéder au lien **déconnexion** .</span><span class="sxs-lookup"><span data-stu-id="2e77c-125">Click the user avatar in the top right corner to access the **Sign out** link.</span></span> <span data-ttu-id="2e77c-126">Cliquez sur **déconnexion** pour réinitialiser la session et revenir à la page d’accueil.</span><span class="sxs-lookup"><span data-stu-id="2e77c-126">Clicking **Sign out** resets the session and returns you to the home page.</span></span>

    ![Capture d’écran du menu déroulant avec le lien Déconnexion](./images/sign-out-button.png)

## <a name="storing-and-refreshing-tokens"></a><span data-ttu-id="2e77c-128">Stockage et actualisation des jetons</span><span class="sxs-lookup"><span data-stu-id="2e77c-128">Storing and refreshing tokens</span></span>

<span data-ttu-id="2e77c-129">À ce stade, votre application a un jeton d’accès, qui est envoyé dans l' `Authorization` en-tête des appels d’API.</span><span class="sxs-lookup"><span data-stu-id="2e77c-129">At this point your application has an access token, which is sent in the `Authorization` header of API calls.</span></span> <span data-ttu-id="2e77c-130">Il s’agit du jeton qui permet à l’application d’accéder à Microsoft Graph pour le compte de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2e77c-130">This is the token that allows the app to access the Microsoft Graph on the user's behalf.</span></span>

<span data-ttu-id="2e77c-131">Cependant, ce jeton est de courte durée.</span><span class="sxs-lookup"><span data-stu-id="2e77c-131">However, this token is short-lived.</span></span> <span data-ttu-id="2e77c-132">Le jeton expire une heure après son émission.</span><span class="sxs-lookup"><span data-stu-id="2e77c-132">The token expires an hour after it is issued.</span></span> <span data-ttu-id="2e77c-133">C’est là que le jeton d’actualisation devient utile.</span><span class="sxs-lookup"><span data-stu-id="2e77c-133">This is where the refresh token becomes useful.</span></span> <span data-ttu-id="2e77c-134">Le jeton d’actualisation permet à l’application de demander un nouveau jeton d’accès sans obliger l’utilisateur à se reconnecter.</span><span class="sxs-lookup"><span data-stu-id="2e77c-134">The refresh token allows the app to request a new access token without requiring the user to sign in again.</span></span>

<span data-ttu-id="2e77c-135">Étant donné que l’application utilise la bibliothèque MSAL, vous n’avez pas besoin d’implémenter de logique d’actualisation ou de stockage de jetons.</span><span class="sxs-lookup"><span data-stu-id="2e77c-135">Because the app is using the MSAL library, you do not have to implement any token storage or refresh logic.</span></span> <span data-ttu-id="2e77c-136">MSAL met en cache le jeton dans la session de navigateur.</span><span class="sxs-lookup"><span data-stu-id="2e77c-136">MSAL caches the token in the browser session.</span></span> <span data-ttu-id="2e77c-137">La `acquireTokenSilent` méthode vérifie d’abord le jeton mis en cache et, s’il n’a pas expiré, il le renvoie.</span><span class="sxs-lookup"><span data-stu-id="2e77c-137">The `acquireTokenSilent` method first checks the cached token, and if it is not expired, it returns it.</span></span> <span data-ttu-id="2e77c-138">Si elle a expiré, elle utilise le jeton d’actualisation mis en cache pour en obtenir une nouvelle.</span><span class="sxs-lookup"><span data-stu-id="2e77c-138">If it is expired, it uses the cached refresh token to obtain a new one.</span></span> <span data-ttu-id="2e77c-139">L’objet client Graph appelle la `getToken` méthode dans **auth.js** à chaque demande, en s’assurant qu’il dispose d’un jeton à jour.</span><span class="sxs-lookup"><span data-stu-id="2e77c-139">The Graph client object calls the `getToken` method in **auth.js** on every request, ensuring that it has an up-to-date token.</span></span>
