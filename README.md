# Frontend-crud
REALISATION D'UN FRONTEND POUR LA GESTION SATATISTIQUES DE JOUEURS DE FOOT

RESSOURCES : Javascript, Json, Git

METHODES: Create, read, delete, update

PROCEDUIRES
  
Céer un dossier   

Créer un fichier index.html dans le dossier principal  

<!doctype html>
  <html lang="fr">
    <meta charset="UTF-8" />
    <title>FTF</title>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css">
  </head>
  <body>


    
    <input type="search" class="form-control" placeholder="Rechercher par titre" />

    
    
    <section class="container mt-1">

        <button class="btn btn-outline-primary" id="form-add">Ajouter un footballeur</button> <br>

        <form action="javascript:void(0);" id="form" class="mt-4">
          <div class="form-group">
            <label for="title">Name</label>
            <input type="text" name="title" id="name" class="form-control" required />
          </div>
          
          <div class="form-group">
            <label for="year">Wins</label>
            <input type="number" name="year" id="wins" class="form-control" required />
          </div>
          <div class="form-group">
            <label for="year">Loses</label>
            <input type="number" name="year" id="lose" class="form-control" required />
          </div>
          <div class="form-group">
            <label for="year">Score</label>
            <input type="number" name="year" id="score" class="form-control" required />
          </div>

          <input type="hidden" id="hidden" />
          <button class="btn btn-xs btn-primary" id="form-save">Enregistrer</button>
          <button class="btn btn-xs" id="form-cancel">Annuler</button>
        </form>

      <div id="content">
        <h1 class="text-center">FEDERATION TOGOLAISE DE FOOTBALL</h1>
        <table class="table table-bordered">
          <thead class="thead-light">
            <tr>
              <th scope="col">Name</th>
              <th scope="col">Wins</th>
              <th scope="col">Loses</th>
              <th scope="col">Scores</th>
              <th scope="col">Action</th>
            </tr>

          </thead>
          <tbody>
          </tbody>
        </table>
      </div>
    </section>
  </body>
  <script type="module" src="app.js"></script>

</html>



Ensuite un fichier Javascript pour gérer le crud    

import { movies } from "./movies.js";

function fetchAllMovies(movies) {
    // Récupération de l'élement
    const elApp = document.getElementsByTagName("tbody")[0];
    elApp.innerHTML = "";
  
    let data = "";
    // Récupération des données
   
    movies.forEach((m, index) => {
        data += `
    <tr>
          <td>${m.name}</td>
          <td>${m.wins}</td>
          <td>${m.Loses}</td>
          <td>${m.Scores}</td>
    <td>
          
    <button class="edit btn btn-sm btn-outline-success" value="${index}">
            Modifier
          </button>
          <button class="delete btn btn-sm btn-outline-danger" value="${index}">
            Supprimer
          </button>
    </td>

    </tr>`;
      });
  
    // Affichage des éléments dans le HTML
    if (data.length > 0) {
        // Affichage des données dans le tableau
    elApp.innerHTML += data;

    // Chaque bouton "Editer"
document.querySelectorAll("button.edit").forEach(b => {
    b.addEventListener("click", function() {
      return editMovie(this.value);
    });
  });
// Chaque bouton "Supprimer"
document.querySelectorAll("button.delete").forEach(b => {
    b.addEventListener("click", function() {
      return deleteMovie(this.value);
    });
  });
} else {
    // Aucune donnée
    elApp.innerHTML += "<p>Aucune ligne trouvée</p>";
  }

  } 
  fetchAllMovies(movies);
  
  document.querySelectorAll("input[type=search]")[0]
  .addEventListener("input", search);


  function search() {
    const filteredData = movies.filter(movie =>
      movie.name.toLowerCase().includes(this.value.toLowerCase())
    );
    fetchAllMovies(filteredData);
  }

  const elForm = document.getElementById("form");
  elForm.style.display = "none";
  const elContent = document.getElementById("content");
document.getElementById("form-add").addEventListener("click", function() {
  displayForm();
});

function displayForm() {
    elForm.style.display = "block";
    elContent.style.display = "none";
  }

  document.getElementById("form-save").addEventListener("click", function() {
    // Récupération des champs
    const name = document.getElementById("name").value;
    const wins = document.getElementById("wins").value;
    const loses = document.getElementById("lose").value;
    const scores = document.getElementById("score").value;
  
    if (name && wins && loses && scores) {
      // Nouvelle ligne
      const movie = { name: name, wins: wins , Loses: loses, Scores: scores};
  
      // Ajout de la nouvelle ligne
      if (document.getElementById("hidden").value.length > 0) {
        movies.splice(document.getElementById("hidden").value, 1, movie);
      } else {
        movies.push(movie);
      }
  
      // Affichage du nouveau tableau
      return fetchAllMovies(movies);
    }

  });
  function hideForm() {
    elForm.style.display = "none";
    elContent.style.display = "block";
  
    document.getElementById("name").value = "";
    document.getElementById("wins").value = "";
    document.getElementById("lose").value = "";
    document.getElementById("score").value = "";
    document.getElementById("hidden").value = "";
  }
  document.getElementById("form-cancel").addEventListener("click", function() {
   
   
   hideForm();
  });
  function editMovie(index) {
    // Récupération de la ligne via son index
    const movie = movies.find((m ,i) => {
      return i == index;
      
    });
    
    // Alimentation des champs
    document.getElementById("name").value = movie.name;
    document.getElementById("wins").value = movie.Wins;
    document.getElementById("lose").value = movie.Loses;
    document.getElementById("score").value = movie.Scores;
    document.getElementById("hidden").value = index;

    displayForm();
   }


function deleteMovie(index) {
  if (confirm("Confirmez-vous la suppression de ce film ?")) {
    movies.splice(index, 1);
    fetchAllMovies(movies);
  }
}

console.table(movies);



Et enfin un fichier Json pour readme pour récupérer les données.

Exemple :   

export const movies = [
    {
      name: "Adebayor",
      wins: 2014,
      Loses: 3,
      Scores:12
    },{
        name: "Djene",
        wins: 2014,
        Loses: 3,
        Scores:12
      },{
        name: "Agassa",
        wins: 2014,
        Loses: 3,
        Scores:12
      },{
        name: "Gagpe",
        wins: 2014,
        Loses: 3,
        Scores:12
      },{
        name: "Interstellar",
        wins: 2014,
        Loses: 3,
        Scores:12
      }
  ];

  
DEPLOIEMENT : NETLIFY (herbergement gratuit)

- Créer un compte sur Netify,    

- exporter le dossier,   

- changer le nom de domaine.




