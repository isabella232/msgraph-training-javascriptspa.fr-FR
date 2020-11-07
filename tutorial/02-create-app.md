---
ms.openlocfilehash: 0ef683278142776d6895b8655dd16e3635b90fa4
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822856"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="118b4-101">Commencez par créer un répertoire vide pour le projet.</span><span class="sxs-lookup"><span data-stu-id="118b4-101">Start by creating an empty directory for the project.</span></span> <span data-ttu-id="118b4-102">Il peut s’agir d’un serveur HTTP ou d’un répertoire de votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="118b4-102">This can be on an HTTP server, or a directory on your development machine.</span></span> <span data-ttu-id="118b4-103">S’il se trouve sur votre ordinateur de développement, vous devez le copier sur un serveur à des fins de test, ou exécuter un serveur HTTP sur votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="118b4-103">If it is on your development machine, you'll need to copy it to a server for testing, or run an HTTP server on your development machine.</span></span> <span data-ttu-id="118b4-104">Si vous n’en avez pas, la section suivante fournit des instructions.</span><span class="sxs-lookup"><span data-stu-id="118b4-104">If you don't have either of those, the next section provides instructions.</span></span>

## <a name="start-a-local-web-server-optional"></a><span data-ttu-id="118b4-105">Démarrer un serveur Web local (facultatif)</span><span class="sxs-lookup"><span data-stu-id="118b4-105">Start a local web server (optional)</span></span>

> [!NOTE]
> <span data-ttu-id="118b4-106">Les étapes de cette section nécessitent [Node.js](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="118b4-106">The steps in this section require [Node.js](https://nodejs.org).</span></span>

<span data-ttu-id="118b4-107">Dans cette section, vous allez utiliser le [protocole HTTP-Server](https://www.npmjs.com/package/http-server) pour exécuter un serveur http simple à partir de la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="118b4-107">In this section you will use [http-server](https://www.npmjs.com/package/http-server) to run a simple HTTP server from the command line.</span></span>

1. <span data-ttu-id="118b4-108">Ouvrez votre interface de ligne de commande (CLI) dans le répertoire que vous avez créé pour le projet.</span><span class="sxs-lookup"><span data-stu-id="118b4-108">Open your command-line interface (CLI) in the directory you created for the project.</span></span>
1. <span data-ttu-id="118b4-109">Exécutez la commande suivante pour démarrer un serveur Web dans ce répertoire.</span><span class="sxs-lookup"><span data-stu-id="118b4-109">Run the following command to start a web server in that directory.</span></span>

    ```Shell
    npx http-server -c-1
    ```

1. <span data-ttu-id="118b4-110">Ouvrez votre navigateur et accédez à `http://localhost:8080` .</span><span class="sxs-lookup"><span data-stu-id="118b4-110">Open your browser and browse to `http://localhost:8080`.</span></span>

<span data-ttu-id="118b4-111">Vous devriez voir un **index de/** page.</span><span class="sxs-lookup"><span data-stu-id="118b4-111">You should see an **Index of /** page.</span></span> <span data-ttu-id="118b4-112">Cela confirme que le serveur HTTP est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="118b4-112">This confirms that the HTTP server is running.</span></span>

![Capture d’écran de la page d’index traitée par http-Server.](images/run-web-server.png)

## <a name="design-the-app"></a><span data-ttu-id="118b4-114">Concevoir l’application</span><span class="sxs-lookup"><span data-stu-id="118b4-114">Design the app</span></span>

<span data-ttu-id="118b4-115">Dans cette section, vous allez créer la mise en page de base de l’interface utilisateur de l’application.</span><span class="sxs-lookup"><span data-stu-id="118b4-115">In this section you'll create the basic UI layout for the application.</span></span>

1. <span data-ttu-id="118b4-116">Créez un fichier à la racine du projet nommé **index.html** et ajoutez le code suivant.</span><span class="sxs-lookup"><span data-stu-id="118b4-116">Create a new file in the root of the project named **index.html** and add the following code.</span></span>

    :::code language="html" source="../demo/graph-tutorial/index.html" id="indexSnippet":::

    <span data-ttu-id="118b4-117">Cette définition définit la disposition de base de l’application, y compris une barre de navigation.</span><span class="sxs-lookup"><span data-stu-id="118b4-117">This defines the basic layout of the app, including a navigation bar.</span></span> <span data-ttu-id="118b4-118">Il ajoute également les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="118b4-118">It also adds the following:</span></span>

    - <span data-ttu-id="118b4-119">[Bootstrap](https://getbootstrap.com/) et son code JavaScript de prise en charge</span><span class="sxs-lookup"><span data-stu-id="118b4-119">[Bootstrap](https://getbootstrap.com/) and its supporting JavaScript</span></span>
    - [<span data-ttu-id="118b4-120">FontAwesome</span><span class="sxs-lookup"><span data-stu-id="118b4-120">FontAwesome</span></span>](https://fontawesome.com/)
    - [<span data-ttu-id="118b4-121">Moment.js</span><span class="sxs-lookup"><span data-stu-id="118b4-121">Moment.js</span></span>](https://momentjs.com/)
    - [<span data-ttu-id="118b4-122">Bibliothèque d’authentification Microsoft pour JavaScript (MSAL.js) 2,0</span><span class="sxs-lookup"><span data-stu-id="118b4-122">Microsoft Authentication Library for JavaScript (MSAL.js) 2.0</span></span>](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-browser)
    - [<span data-ttu-id="118b4-123">Bibliothèque cliente JavaScript Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="118b4-123">Microsoft Graph JavaScript Client Library</span></span>](https://github.com/microsoftgraph/msgraph-sdk-javascript)

    > [!TIP]
    > <span data-ttu-id="118b4-124">La page inclut un favorite, ( `<link rel="shortcut icon" href="g-raph.png">` ).</span><span class="sxs-lookup"><span data-stu-id="118b4-124">The page includes a favicon, (`<link rel="shortcut icon" href="g-raph.png">`).</span></span> <span data-ttu-id="118b4-125">Vous pouvez supprimer cette ligne, ou vous pouvez télécharger le fichier **g-raph.png** à partir de [GitHub](https://github.com/microsoftgraph/g-raph).</span><span class="sxs-lookup"><span data-stu-id="118b4-125">You can remove this line, or you can download the **g-raph.png** file from [GitHub](https://github.com/microsoftgraph/g-raph).</span></span>

1. <span data-ttu-id="118b4-126">Créez un fichier nommé **style. CSS** et ajoutez le code suivant.</span><span class="sxs-lookup"><span data-stu-id="118b4-126">Create a new file named **style.css** and add the following code.</span></span>

    :::code language="css" source="../demo/graph-tutorial/style.css":::

1. <span data-ttu-id="118b4-127">Créez un fichier nommé **auth.js** et ajoutez le code suivant.</span><span class="sxs-lookup"><span data-stu-id="118b4-127">Create a new file named **auth.js** and add the following code.</span></span>

    ```javascript
    function signIn() {
      // TEMPORARY
      updatePage({name: 'Megan Bowen', userName: 'meganb@contoso.com'});
    }

    function signOut() {
      // TEMPORARY
      updatePage();
    }
    ```

1. <span data-ttu-id="118b4-128">Créez un fichier nommé **ui.js** et ajoutez le code suivant.</span><span class="sxs-lookup"><span data-stu-id="118b4-128">Create a new file named **ui.js** and add the following code.</span></span>

    ```javascript
    // Select DOM elements to work with
    const authenticatedNav = document.getElementById('authenticated-nav');
    const accountNav = document.getElementById('account-nav');
    const mainContainer = document.getElementById('main-container');

    const Views = { error: 1, home: 2, calendar: 3 };

    function createElement(type, className, text) {
      var element = document.createElement(type);
      element.className = className;

      if (text) {
        var textNode = document.createTextNode(text);
        element.appendChild(textNode);
      }

      return element;
    }

    function showAuthenticatedNav(user, view) {
      authenticatedNav.innerHTML = '';

      if (user) {
        // Add Calendar link
        var calendarNav = createElement('li', 'nav-item');

        var calendarLink = createElement('button',
          `btn btn-link nav-link${view === Views.calendar ? ' active' : '' }`,
          'Calendar');
        calendarLink.setAttribute('onclick', 'getEvents();');
        calendarNav.appendChild(calendarLink);

        authenticatedNav.appendChild(calendarNav);
      }
    }

    function showAccountNav(user) {
      accountNav.innerHTML = '';

      if (user) {
        // Show the "signed-in" nav
        accountNav.className = 'nav-item dropdown';

        var dropdown = createElement('a', 'nav-link dropdown-toggle');
        dropdown.setAttribute('data-toggle', 'dropdown');
        dropdown.setAttribute('role', 'button');
        accountNav.appendChild(dropdown);

        var userIcon = createElement('i',
          'far fa-user-circle fa-lg rounded-circle align-self-center');
        userIcon.style.width = '32px';
        dropdown.appendChild(userIcon);

        var menu = createElement('div', 'dropdown-menu dropdown-menu-right');
        dropdown.appendChild(menu);

        var userName = createElement('h5', 'dropdown-item-text mb-0', user.displayName);
        menu.appendChild(userName);

        var userEmail = createElement('p', 'dropdown-item-text text-muted mb-0', user.mail || user.userPrincipalName);
        menu.appendChild(userEmail);

        var divider = createElement('div', 'dropdown-divider');
        menu.appendChild(divider);

        var signOutButton = createElement('button', 'dropdown-item', 'Sign out');
        signOutButton.setAttribute('onclick', 'signOut();');
        menu.appendChild(signOutButton);
      } else {
        // Show a "sign in" button
        accountNav.className = 'nav-item';

        var signInButton = createElement('button', 'btn btn-link nav-link', 'Sign in');
        signInButton.setAttribute('onclick', 'signIn();');
        accountNav.appendChild(signInButton);
      }
    }

    function showWelcomeMessage(user) {
      // Create jumbotron
      var jumbotron = createElement('div', 'jumbotron');

      var heading = createElement('h1', null, 'JavaScript SPA Graph Tutorial');
      jumbotron.appendChild(heading);

      var lead = createElement('p', 'lead',
        'This sample app shows how to use the Microsoft Graph API to access' +
        ' a user\'s data from JavaScript.');
      jumbotron.appendChild(lead);

      if (user) {
        // Welcome the user by name
        var welcomeMessage = createElement('h4', null, `Welcome ${user.displayName}!`);
        jumbotron.appendChild(welcomeMessage);

        var callToAction = createElement('p', null,
          'Use the navigation bar at the top of the page to get started.');
        jumbotron.appendChild(callToAction);
      } else {
        // Show a sign in button in the jumbotron
        var signInButton = createElement('button', 'btn btn-primary btn-large',
          'Click here to sign in');
        signInButton.setAttribute('onclick', 'signIn();')
        jumbotron.appendChild(signInButton);
      }

      mainContainer.innerHTML = '';
      mainContainer.appendChild(jumbotron);
    }

    function showError(error) {
      var alert = createElement('div', 'alert alert-danger');

      var message = createElement('p', 'mb-3', error.message);
      alert.appendChild(message);

      if (error.debug)
      {
        var pre = createElement('pre', 'alert-pre border bg-light p-2');
        alert.appendChild(pre);

        var code = createElement('code', 'text-break text-wrap',
          JSON.stringify(error.debug, null, 2));
        pre.appendChild(code);
      }

      mainContainer.innerHTML = '';
      mainContainer.appendChild(alert);
    }

    function updatePage(view, data) {
      if (!view) {
        view = Views.home;
      }

      const user = JSON.parse(sessionStorage.getItem('graphUser'));

      showAccountNav(user);
      showAuthenticatedNav(user, view);

      switch (view) {
        case Views.error:
          showError(data);
          break;
        case Views.home:
          showWelcomeMessage(user);
          break;
        case Views.calendar:
          break;
      }
    }

    updatePage(Views.home);
    ```

1. <span data-ttu-id="118b4-129">Enregistrez toutes vos modifications et actualisez la page.</span><span class="sxs-lookup"><span data-stu-id="118b4-129">Save all of your changes and refresh the page.</span></span> <span data-ttu-id="118b4-130">À présent, l’application doit être très différente.</span><span class="sxs-lookup"><span data-stu-id="118b4-130">Now, the app should look very different.</span></span>

    ![Capture d’écran de la page d’accueil repensée](images/app-layout.png)
