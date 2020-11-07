---
ms.openlocfilehash: 0ef683278142776d6895b8655dd16e3635b90fa4
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822856"
---
<!-- markdownlint-disable MD002 MD041 -->

Commencez par créer un répertoire vide pour le projet. Il peut s’agir d’un serveur HTTP ou d’un répertoire de votre ordinateur de développement. S’il se trouve sur votre ordinateur de développement, vous devez le copier sur un serveur à des fins de test, ou exécuter un serveur HTTP sur votre ordinateur de développement. Si vous n’en avez pas, la section suivante fournit des instructions.

## <a name="start-a-local-web-server-optional"></a>Démarrer un serveur Web local (facultatif)

> [!NOTE]
> Les étapes de cette section nécessitent [Node.js](https://nodejs.org).

Dans cette section, vous allez utiliser le [protocole HTTP-Server](https://www.npmjs.com/package/http-server) pour exécuter un serveur http simple à partir de la ligne de commande.

1. Ouvrez votre interface de ligne de commande (CLI) dans le répertoire que vous avez créé pour le projet.
1. Exécutez la commande suivante pour démarrer un serveur Web dans ce répertoire.

    ```Shell
    npx http-server -c-1
    ```

1. Ouvrez votre navigateur et accédez à `http://localhost:8080` .

Vous devriez voir un **index de/** page. Cela confirme que le serveur HTTP est en cours d’exécution.

![Capture d’écran de la page d’index traitée par http-Server.](images/run-web-server.png)

## <a name="design-the-app"></a>Concevoir l’application

Dans cette section, vous allez créer la mise en page de base de l’interface utilisateur de l’application.

1. Créez un fichier à la racine du projet nommé **index.html** et ajoutez le code suivant.

    :::code language="html" source="../demo/graph-tutorial/index.html" id="indexSnippet":::

    Cette définition définit la disposition de base de l’application, y compris une barre de navigation. Il ajoute également les éléments suivants :

    - [Bootstrap](https://getbootstrap.com/) et son code JavaScript de prise en charge
    - [FontAwesome](https://fontawesome.com/)
    - [Moment.js](https://momentjs.com/)
    - [Bibliothèque d’authentification Microsoft pour JavaScript (MSAL.js) 2,0](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-browser)
    - [Bibliothèque cliente JavaScript Microsoft Graph](https://github.com/microsoftgraph/msgraph-sdk-javascript)

    > [!TIP]
    > La page inclut un favorite, ( `<link rel="shortcut icon" href="g-raph.png">` ). Vous pouvez supprimer cette ligne, ou vous pouvez télécharger le fichier **g-raph.png** à partir de [GitHub](https://github.com/microsoftgraph/g-raph).

1. Créez un fichier nommé **style. CSS** et ajoutez le code suivant.

    :::code language="css" source="../demo/graph-tutorial/style.css":::

1. Créez un fichier nommé **auth.js** et ajoutez le code suivant.

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

1. Créez un fichier nommé **ui.js** et ajoutez le code suivant.

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

1. Enregistrez toutes vos modifications et actualisez la page. À présent, l’application doit être très différente.

    ![Capture d’écran de la page d’accueil repensée](images/app-layout.png)
