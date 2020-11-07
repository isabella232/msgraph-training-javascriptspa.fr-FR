---
ms.openlocfilehash: 1f2ff0e013bd1b104cd5b353ba2da542382657ab
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822859"
---
<!-- markdownlint-disable MD002 MD041 -->

Dans cet exercice, vous allez incorporer Microsoft Graph dans l’application. Pour cette application, vous allez utiliser la bibliothèque de [bibliothèque cliente JavaScript Microsoft Graph](https://github.com/microsoftgraph/msgraph-sdk-javascript) pour effectuer des appels à Microsoft Graph.

## <a name="get-calendar-events-from-outlook"></a>Récupérer les événements de calendrier à partir d’Outlook

Dans cette section, vous allez utiliser la bibliothèque cliente Microsoft Graph pour obtenir des événements de calendrier pour l’utilisateur.

1. Créez un fichier à la racine du projet nommé **timezones.js** et ajoutez le code suivant.

    :::code language="javascript" source="../demo/graph-tutorial/timezones.js" id="zoneMappingsSnippet":::

    Ce code mappe les identificateurs de fuseau horaire Windows aux identificateurs de fuseau horaire d’IANA pour des incompatibilités avec moment.js.

1. Ajoutez la fonction suivante à **graph.js**.

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="getEventsSnippet":::

    Que fait ce code ?

    - L’URL qui sera appelée est `/me/calendarview`.
    - La `header` méthode ajoute un `Prefer` en-tête spécifiant le fuseau horaire préféré de l’utilisateur.
    - La `query` méthode ajoute les heures de début et de fin pour l’affichage Calendrier.
    - La `select` méthode limite les champs renvoyés pour chaque événement à ceux que l’affichage utilise réellement.
    - La `orderby` méthode trie les résultats en fonction de l’heure de début, avec l’événement le plus tôt en premier.
    - La `top` méthode demande jusqu’à 50 événements dans la réponse.

1. Ouvrez **ui.js** et ajoutez la fonction suivante.

    ```javascript
    function showCalendar(events) {
      // TEMPORARY
      // Render the results as JSON
      var alert = createElement('div', 'alert alert-success');

      var pre = createElement('pre', 'alert-pre border bg-light p-2');
      alert.appendChild(pre);

      var code = createElement('code', 'text-break',
        JSON.stringify(events, null, 2));
      pre.appendChild(code);

      mainContainer.innerHTML = '';
      mainContainer.appendChild(alert);
    }
    ```

1. Mettez à jour l' `switch` instruction de la `updatePage` fonction à appeler `showCalendar` lorsque la vue est `Views.calendar` .

    :::code language="javascript" source="../demo/graph-tutorial/ui.js" id="updatePageSnippet" highlight="18-20":::

1. Enregistrez vos modifications et actualisez l’application. Connectez-vous, puis cliquez sur le lien **calendrier** dans la barre de navigation. Si tout fonctionne, vous devriez voir une image mémoire JSON des événements dans le calendrier de l’utilisateur.

## <a name="display-the-results"></a>Afficher les résultats

Dans cette section, vous allez mettre à jour la `showCalendar` fonction pour afficher les événements de manière plus conviviale.

1. Remplacez la fonction `showCalendar` existante par ce qui suit.

    :::code language="javascript" source="../demo/graph-tutorial/ui.js" id="showCalendarSnippet":::

    Cette méthode effectue une boucle dans la collection d’événements et ajoute une ligne de tableau pour chacun d’eux.

1. Enregistrer les modifications et actualiser l’application. Cliquez sur le lien **calendrier** et l’application doit maintenant afficher un tableau d’événements pour la semaine en cours.

    ![Capture d’écran du tableau des événements](./images/calendar-list.png)
