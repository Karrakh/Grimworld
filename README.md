# Grimworld

<!DOCTYPE html>

<html lang="fr">
<head>
<link href="https://fonts.googleapis.com/css2?family=IM+Fell+DW+Pica+SC&display=swap" rel="stylesheet"/><link href="https://fonts.googleapis.com/css2?family=IM+Fell+English&amp;display=swap" rel="stylesheet"/>
<meta charset="utf-8"/>
<meta content="width=device-width, initial-scale=1.0" name="viewport"/>
<title>Grimworld Générateur</title>
<style>
    body { font-family: 'IM Fell English', serif; background: #f4f4f4; padding: 20px; max-width: 900px; margin: auto; }
    h1, h2 { text-align: center; }
    label, select, button { font-size: 1rem; margin: 5px; }
    .fiche { background: #fff; padding: 20px; margin-top: 20px; border-radius: 10px; box-shadow: 0 0 10px #ccc; text-align: left; }
    ul { list-style: none; padding: 0; }
    .ligne-haut { display: flex; justify-content: space-between; font-weight: bold; font-size: 1.1rem; }
    .equipement-zone { margin-top: 10px; display: flex; align-items: center; gap: 10px; }
    select#selectEquip { font-size: 1rem; padding: 4px; }
    .equiper-btn, .retirer-btn { font-size: 1rem; padding: 4px 8px; }
  
  @media print {
    button, .equipement-zone, select, label, .no-print {
      display: none !important;
    }
    body {
      background: white !important;
      padding: 0 !important;
    }
  }

button, select {
  font-family: 'IM Fell English', serif;
}

@media screen and (max-width: 600px) {
  body {
    padding: 10px;
  }
  .ligne-haut {
    flex-direction: column;
    align-items: flex-start;
    font-size: 1rem;
  }
  .equipement-zone {
    flex-direction: column;
    align-items: stretch;
  }
  button, select {
    width: 100%;
  }
}


button.generer {
  background-color: #5a3f2f;
  color: white;
  border: none;
  border-radius: 8px;
  padding: 8px 16px;
  font-weight: bold;
  box-shadow: 2px 2px 6px #00000033;
  transition: background-color 0.2s ease;
}
button.generer:hover {
  background-color: #7a5b3f;
}


<style>
  .fiche.compact {
    font-size: 0.7rem;
    padding: 5px;
    line-height: 1.1;
  }
  .fiche.compact h2,
  .fiche.compact h3 {
    font-size: 0.9rem;
    margin: 4px 0;
  }
  .fiche.compact ul {
    margin: 0;
    padding: 0;
  }
  .fiche.compact li {
    margin: 0;
  }



</style>




</style>
<link href="https://fonts.googleapis.com/css2?family=IM+Fell+English&amp;display=swap" rel="stylesheet"/>
<style>
.fiche h2, .fiche h3 {
  font-family: 'IM Fell DW Pica SC', serif;
  text-transform: uppercase;
}
</style>

</head>
<body><div id="menu-principal" style="text-align: center; margin: 2rem;">
<button onclick="afficherSection('recrutement')">Recruter des mercenaires</button>
<button onclick="afficherSection('capitaine')">Choisir son Capitaine</button>
<button onclick="afficherSection('evenements')">Évènements aléatoires</button>
<button onclick="afficherSection('feuille')">Feuille de bande</button>
<button onclick="afficherSection('magasin')">Magasin</button>
</div>
<div id="section-recrutement"><div id="changelog" style="
  position: fixed;
  top: 0; left: 0;
  width: 100%; height: 100%;
  background: white;
  color: black;
  z-index: 9999;
  display: none;
  padding: 2rem;
  box-sizing: border-box;
  overflow-y: auto;
">
<div id="changelog-content">Chargement des notes...</div>
<button onclick="fermerChangelog()">Ok</button>
</div><div id="changelog-icon" style="
  position: fixed;
  top: 1rem;
  right: 1rem;
  background: #222;
  color: white;
  padding: 0.5rem 1rem;
  border-radius: 4px;
  cursor: pointer;
  z-index: 9998;
  font-weight: bold;
">
  i
</div><h1>Grimworld - Générateur de Mercenaire</h1><label>Rôle :</label><select id="role">
<option value="Combattant">Combattant</option>
<option value="Gardien">Gardien</option>
<option value="Avant-Garde">Avant-Garde</option>
<option value="Érudit">Érudit</option>
</select><label>Origine :</label><select id="origine">
<option value="Humain">Humain</option>
<option value="ElfeHab">Elfe noir</option>
<option value="ElfeInt">Haut elfe</option>
<option value="Nain">Nain</option>
<option value="Ogre">Ogre</option>
<option value="HommeRat">Homme-rat</option>
<option value="Orc">Orc</option>
<option value="Gobelin">Gobelin</option>
</select><label>Rang :</label><select id="rang">
<option value="Recrue (10Co)">Recrue (10Co)</option>
<option value="Aguerri (20Co)">Aguerri (20Co)</option>
<option value="Expérimenté (30Co)">Expérimenté (30Co)</option>
<option value="Élite (50Co)">Élite (50Co)</option>
<option value="Vétéran (100Co)">Vétéran (100Co)</option>
</select><button class="generer" onclick="generer()">Générer</button><button class="no-print" onclick="resetFiches()">Reset</button><div class="fiche" id="fiche"></div><button class="no-print" onclick="captureImage()">Enregistrer</button></div>
<!-- Icône info -->
<script>
const equipementDisponible = [
  { nom: "Épée", prix: 15 },
  { nom: "Bouclier", prix: 10 },
  { nom: "Cotte de mailles", prix: 30 },
  { nom: "Potion de soin", prix: 20 },
  { nom: "Arbalète de poing", prix: 10},
  { nom: "Arbalète lourde", prix: 20},
  { nom: "Claymore", prix: 30},
  { nom: "Hache d'arme", prix: 15},
  { nom: "Lance", prix: 15},
  { nom: "Gambison", prix: 20}
,
  { nom: "Armure de cuir", prix: 10 },
  { nom: "Dague", prix: 5 }
];

const bonusRoles = {
  "Combattant": { FOR: 30, END: 10 },
  "Gardien": { END: 30, COU: 10 },
  "Avant-Garde": { HAB: 30, INT: 10 },
  "Érudit": { INT: 30, COU: 10 }
};

const bonusOrigines = {
  Humain: {},
  ElfeHab: { HAB: 10, END: -10 },
  ElfeInt: { INT: 10, END: -10 },
  Nain: { END: 10, HAB: -10 },
  Ogre: { FOR: 10, END: 10, HAB: -10, INT: -10 },
  HommeRat: { HAB: 10, COU: -10 },
  Orc: { FOR: 10, HAB: -10 },
  Gobelin: { HAB: 10, FOR: -10 }
};

const competences = ['Bretteur', 'Parade', 'Franc Tireur', 'Réflexes', 'Port d’armure', 'Maîtrise du bouclier', 'Mage de guerre', 'Endurci', 'Endurant', 'Robuste', 'Coureur', 'Focalisateur', 'Maitrise du flux', 'Résilient'];

const descriptionCompetences = {
  "Bretteur": "augmente l’attaque lors d’un assaut de +1/niveau avec les armes de mêlée.",
  "Parade": "augmente la défense lors d’un assaut de +1/niveau avec les armes de mêlée.",
  "Franc Tireur": "augmente l’attaque lors d’un tir de +1/niveau.",
  "Réflexes": "augmente la défense de +1/niveau lors d’une Esquive.",
  "Port d’armure": "réduit l’encombrement des armures légères de 1/niveau.",
  "Maîtrise du bouclier": "augmente la défense avec un bouclier lors d’un assaut et d’un tir de +1/niveau.",
  "Mage de guerre": "augmente la puissance lors d’un lancer de sort de +1/niveau.",
  "Endurci": "augmente les points de vie de +2/niveau.",
  "Endurant": "augmente la fatigue max de +1/niveau.",
  "Robuste": "augmente l’encombrement maximum de +1/niveau.",
  "Coureur": "augmente le maximum de déplacement de +1/niveau.",
  "Focalisateur": "augmente le maximum de flux de +1/niveau.",
  "Maitrise du flux": "dissipe 1 flux Chaotique supplémentaire par tour.",
  "Résilient": "peut dépenser 1💧 par niveau au lieu de recevoir 1💥."
};


const atoutsParRole = {
  "Combattant": {
    "Charge écrasante": "(A) **3 Fatigue** : Le bonus en attaque conféré par une charge passe à +3 au lieu de +1. Si l’attaque réussit, le défenseur subit 2 dégâts supplémentaires et recule de 1”.",
    "Parade de Ferlay": "(R) **2 Fatigue** : Augmente la défense de +3 lors d’un assaut. Chaque désavantage obtenu réduit les dégâts de -1.",
    "Balayage": "(A) **3 Fatigue** : Effectue une attaque circulaire contre jusqu’à 3 ennemis. Seule la meilleure défense est retenue.",
    "Duelliste": "(P) **0 Fatigue** : +2 en attaque et défense contre un seul adversaire. -1 si en sous-nombre."
  },
  "Gardien": {
    "Posture défensive": "(A) **2 Fatigue** : +4 en défense, +2 discipline, -2 attaque jusqu’à fin du tour.",
    "Parade de Ferlay": "(R) **2 Fatigue** : Augmente la défense de +3 lors d’un assaut. Chaque désavantage obtenu réduit les dégâts de -1.",
    "Cri de défi": "(R) **2 Fatigue** : Provoque un ennemi à 6”. Il gagne +2 attaque contre vous, -2 contre les autres."
  },
  "Avant-Garde": {
    "Tir précis": "(A) **2 Fatigue** : Tir ignore la protection si la cible n’a pas de couvert.",
    "Tir assuré": "(A) **2 Fatigue** : +4 en précision lors du tir.",
    "Tir rapide": "(A) **3 Fatigue** : Effectue 2 tirs. Le second a -2 précision. Incompatible avec 'Recharge'."
  },
  "Érudit": {
    "Accumulation arcanique": "(A) **2 Fatigue** : Lance un sort avec puissance +4.",
    "Résonance Chaotique": "(A) **3 Fatigue** : Relance les dés du chaos et lance un sort.",
    "Maîtrise des flux": "(A) **3 Fatigue** : Lance un sort et gagne +4 canalisation temporaire."
  }
};

const traits = ['Cupide', 'Bourrin', 'Imperturbable', 'Fourbe', 'Hémophile', 'Brave', 'Rusé', 'Pleutre', 'Chanceux', 'Véloce', 'Vision parfaite', 'Athlétique', 'Peau épaisse', 'Alcoolique', 'Visage difforme', 'Fayot', 'Boiteux', 'Distrait', 'Asthme à l’effort', 'Force de la nature', 'Tête de mule', 'Mâchoire carrée'];

const descriptionTraits = {
  "Cupide": "garde 50% des couronnes qu’il récupère pendant une mission.",
  "Bourrin": "inflige +2 dégâts mais subit une pénalité permanente de défense de -1.",
  "Imperturbable": "gagne définitivement 1 en discipline.",
  "Fourbe": "gagne +1 en attaque lorsqu’il effectue un assaut contre un ennemi engagé.",
  "Hémophile": "est considéré comme Blessé lorsqu’il est à moins de 6 de vitalité (au lieu de 4).",
  "Brave": "+2 en discipline lors d’un test de moral. Ne peut pas être Couard.",
  "Rusé": "+1 à l’INT lors d’un test.",
  "Pleutre": "-2 en discipline lors d’un test de moral. Ne peut pas être Brave.",
  "Chanceux": "une fois par mission, si le mercenaire devait rater un test, il est réussi comme s’il avait obtenu 1 succès.",
  "Véloce": "lorsqu’il sprint ou charge, le mercenaire gagne +6” de déplacement au lieu de +4”.",
  "Vision parfaite": "réduit de 1 les modificateurs liés à la portée lors d’un tir.",
  "Athlétique": "le gain de fatigue est toujours réduit de 1 (minimum 1).",
  "Peau épaisse": "l’encaissement augmente de +1 mais la récupération de Vitalité est réduite de moitié.",
  "Alcoolique": "avant la mission, lancer 1d100: 01-50: +3 COU / -1 autres tests. 51-75: pas de bonus de déplacement. 76-00: sobre.",
  "Visage difforme": "le mercenaire est suspecté d’avoir subi des mutations. -1 en discipline à tous les ennemis engagés avec lui.",
  "Fayot": "+1 en attaque s’il est en LdV du Capitaine.",
  "Boiteux": "le mercenaire perd 2” de déplacement.",
  "Distrait": "-2 en initiative si aucun ennemi ou objectif dans sa LdV.",
  "Asthme à l’effort": "subit systématiquement 1 fatigue après un sprint ou une charge.",
  "Force de la nature": "+1 en FOR lors d’un test.",
  "Tête de mule": "il est impossible d’annuler l’action ou la manœuvre de ce mercenaire.",
  "Mâchoire carrée": "+2 en END lors d’une mise hors combat."
};
const fichesEquipement = new Map();
const fichesOr = new Map();

function genererNom() {
const prenoms = [
  "Aldran",
  "Berric",
  "Dornak",
  "Fenrik",
  "Gareth",
  "Ithran",
  "Jorik",
  "Kaelis",
  "Morwin",
  "Oran",
  "Peryn",
  "Quoril",
  "Ravok",
  "Tharek",
  "Ulwyn",
  "Vaelis",
  "Werrin",
  "Xanrik",
  "Zulmir",
  "Ashen",
  "Cendrik",
  "Delios",
  "Faelar",
  "Gaelis",
  "Halwyn",
  "Jarn",
  "Kareth",
  "Lioren",
  "Mervan",
  "Neralis",
  "Orrin",
  "Perwyn",
  "Sarnak",
  "Talien",
  "Vorik",
  "Xandor",
  "Zeren",
  "Branik",
  "Drogan",
  "Ervik",
  "Farn",
  "Griswold",
  "Harok",
  "Isendil",
  "Jarrek",
  "Kelmar",
  "Lorik",
  "Magnor",
  "Nivrak",
  "Torvak",
  "Erdor",
  "Kelmod",
  "Torgar",
  "Zandur",
  "Wenmir",
  "Kelmir",
  "Sardan",
  "Orthil",
  "Isthas",
  "Valvek",
  "Beldon",
  "Perros",
  "Ismon",
  "Lorven",
  "Marlor",
  "Kelven",
  "Perdan",
  "Perrian",
  "Isdor",
  "Yorthas",
  "Dargorn",
  "Hardon",
  "Sargorn",
  "Erran",
  "Harrik",
  "Kellor",
  "Norlen",
  "Torgorn",
  "Rallor",
  "Quormir",
  "Lorvek",
  "Jarven",
  "Erros",
  "Erdon",
  "Xanmon",
  "Valdon",
  "Quorrik",
  "Kelgar",
  "Tormir",
  "Xanvik",
  "Normir",
  "Erven",
  "Fendor",
  "Orrian",
  "Jarrian",
  "Wenvek",
  "Isvek",
  "Yormir",
  "Ulran",
  "Vallor",
  "Quorlor",
  "Quorven",
  "Orrik",
  "Althas",
  "Tormon",
  "Perran",
  "Yorlor",
  "Jardon",
  "Fendon",
  "Hargar",
  "Yorven",
  "Althil",
  "Xanthil",
  "Lorthil",
  "Lorlor",
  "Marmod",
  "Jarlor",
  "Marros",
  "Margar",
  "Ordur",
  "Kelros",
  "Wenthas",
  "Zanmod",
  "Darvek",
  "Alvik",
  "Valrik",
  "Lordan",
  "Valven",
  "Galdon",
  "Quorvik",
  "Fenvik",
  "Ulvek",
  "Orran",
  "Wenmon",
  "Quormod",
  "Kelrian",
  "Quorthas",
  "Jarvik",
  "Wenlen",
  "Marthas",
  "Zanvek",
  "Quordan",
  "Galthil",
  "Norran",
  "Kelran",
  "Valvik",
  "Lorlen",
  "Norven",
  "Jardor",
  "Marvek",
  "Bellor",
  "Harlen",
  "Xanthas",
  "Yorgorn",
  "Northil",
  "Ismir",
  "Aldon",
  "Xanven",
  "Zanran",
  "Marlen",
  "Kellen",
  "Darvik",
  "Xanlor",
  "Zandon",
  "Erdur",
  "Beldur",
  "Tordur",
  "Valmon",
  "Dardor",
  "Zangorn",
  "Wenran",
  "Almir",
  "Uldon",
  "Ralmir",
  "Isdan",
  "Jardur",
  "Fenmon",
  "Marrik",
  "Ralrik",
  "Zanvik",
  "Erthas",
  "Raldur",
  "Norgorn",
  "Ulvik",
  "Darthas",
  "Ulgorn",
  "Belthil",
  "Wendan",
  "Isgar",
  "Ullor",
  "Norrian",
  "Gallor",
  "Islen",
  "Wenthil",
  "Ulthil",
  "Marmon",
  "Quorvek",
  "Fenros",
  "Ermod",
  "Normod"
];
  const surnoms = [
  "le Silencieux", "la Louve", "le Brisé", "la Lame", "le Cruel", "la Flèche", "le Borgne", "la Mère", "le Vieux", "le Sombre",
  "le Tordu", "le Couteau", "la Griffe", "le Noir", "la Sanglante", "l'Égaré", "l'Ancien", "le Patient", "le Juste", "le Hargneux",
  "le Banni", "la Sorcière", "le Moine", "le Fourbe", "le Fratricide", "le Défunt", "le Muet", "le Fielleux", "le Chien", "le Corbeau",
  "le Serpent", "le Faucheur", "Sanguinaire", "Crocs-de-Fer", "l’Ombre du Désert", "Chant-de-Guerre", "Marche-Cendres", "Larmes-d’Acier", "Hurle-Mort", "Cœur-de-Pierre",
  "Griffe-Sombre", "Œil-Unique", "Brise-Os", "Tête-Rouge", "Flamme-Perdue", "Chasse-la-Nuit", "Main-Creuse", "Voix-d’Épine", "Sabre-Brisé", "Sans-Visage",
  "Dents-Sèches", "Crâne-Fendu", "Poing-de-Verre", "Main-Sanglante", "Tisse-Rancune", "Feu-Follet", "Ronces-Sang", "Fumée-de-Feu", "Langue-Piquante", "Rire-Sec",
  "Nuit-Morte", "Bras-Cassé", "Pas-Sage", "Vengeance-Lente", "Souffle-Brûlé", "Gueule-de-Pierre", "le Traître", "le Vagabond", "le Fou", "l'Insatiable",
  "la Vipère", "l’Oublié", "le Méprisé", "le Damné", "le Voleur", "le Lâche", "le Loup", "le Boiteux", "le Fléau", "le Témoin",
  "le Souillé", "l’Implacable", "l’Inconnu", "le Dissident", "le Fanatique", "le Vengeur", "le Justicier", "le Fracasseur", "le Téméraire", "le Veilleur",
  "le Saigneur", "l’Exilé", "le Mordeur", "le Découpeur", "le Ravageur", "le Survivant", "le Déchu", "le Pur", "le Tourmenté", "le Reclus",
  "le Gelé", "le Frisson", "le Marteau", "le Sceptique", "le Gardien", "le Vigilant", "le Calciné", "le Hurleur", "le Frémissant", "le Tempétueux",
  "le Marteleur", "le Grincheux", "le Volontaire", "le Prédateur", "le Discret", "le Réprouvé", "le Sage", "le Meurtri", "le Démoniaque", "le Givré",
  "le Charognard", "le Nécrosé", "le Boucher", "le Méfiant", "le Renégat", "le Calme", "le Possédé", "le Dévoreur", "le Ténébreux", "le Saignant",
  "le Griffé", "le Sans-Nom", "le Souffrant", "le Désespéré", "le Fracassé", "le Rôdeur", "le Torturé", "le Foudroyé", "le Maudit", "le Sanglant",
  "le Flétri", "le Balafré", "le Flottant", "le Faussaire", "le Confus", "le Glacial", "le Grondant", "le Froid", "le Disloqué", "le Démembré",
  "le Défiguré", "le Sang-Vif", "le Poète", "le Dément", "le Brûlé", "le Brisé-d'Âme", "le Tordu-d’Esprit", "le Broyeur", "le Saigneur-du-Matin", "le Croc-de-Glace",
  "le Garde-sans-Refuge", "le Marche-Nuit", "le Pilleur", "le Vide", "le Non-Vivant", "le Repoussant", "le Rôdeur-du-Bleu", "le Lame-Fendue", "le Dévoreur-d’Espoirs", "le Rouillé",
  "le Lointain", "le Rasoir", "le Scindé", "le Broyeur-d’Échos", "le Sans-Larmes", "le Pendu", "le Replié", "le Glorieux", "le Massacreur", "le Sang-Chaud",
  "le Pourfendeur", "le Revenu", "le Vagissant", "le Claquant", "le Fossile", "le Regard-Perdu", "le Brumeux", "le Grondeur", "le Condamné", "le Lourd",
  "le Morcelé", "le Rejeton", "le Dissimulé", "le Lointain-Hurlant", "le Noyé", "le Submergé", "le Menaçant", "le Dernier", "le Premier"
];
  return prenoms[Math.floor(Math.random() * prenoms.length)] + " " +
         surnoms[Math.floor(Math.random() * surnoms.length)];
}

function rollD100() {
  return Math.floor(Math.random() * 100) + 1;
}

function convertValeur(val) {
  if (val <= 40) return 2;
  if (val <= 70) return 3;
  if (val <= 90) return 4;
  return 5;
}

function tirerCompetences(rang) {
  const pool = new Set();
  const tirage = (niveau) => {
    let essais = 0;
    while (essais < 100) {
      const base = competences[Math.floor(Math.random() * competences.length)];
      const tag = base + " " + "I".repeat(niveau);
      if (![...pool].some(x => x.startsWith(base))) {
        pool.add(tag);
        return;
      }
      essais++;
    }
  };
  if (rang.includes("Recrue")) tirage(1);
  if (rang.includes("Aguerri")) { tirage(1); tirage(1); }
  if (rang.includes("Expérimenté")) { tirage(2); tirage(1); }
  if (rang.includes("Élite")) { tirage(3); tirage(1); tirage(1); }
  if (rang.includes("Vétéran")) { tirage(3); tirage(2); tirage(1); }
  return [...pool];
}

function tirerAtouts(rang) {
  const tirages = {
    "Aguerri": 1,
    "Expérimenté": 1,
    "Élite": 2,
    "Vétéran": 2
  };
  const n = Object.entries(tirages).find(([k]) => rang.includes(k));
  const res = new Set();
  const count = n ? n[1] : 0;
  while (res.size < count) {
    res.add(atouts[Math.floor(Math.random() * atouts.length)]);
  }
  return [...res];
}

function calculerSolde(equipement, rang) {
  const base = parseInt(rang.match(/\d+/)[0]);
  return base + equipement.reduce((s, e) => s + e.prix, 0);
}

function generer() {
  const container = document.getElementById("fiche");
  const fiche = document.createElement("div");
  fiche.className = "fiche";
  const ficheId = crypto.randomUUID().replace(/-/g, "");
  fiche.dataset.id = ficheId;
  container.appendChild(fiche);

  const role = document.getElementById("role").value;
  const origine = document.getElementById("origine").value;
  const rang = document.getElementById("rang").value;
  const traitNom = traits[Math.floor(Math.random() * traits.length)];
  const nom = genererNom();

  const caracs = ["FOR", "END", "HAB", "INT", "COU"];
  const valeurs = {};
const details = {};
caracs.forEach(c => {
  const bonus = (bonusRoles[role]?.[c] || 0) + (bonusOrigines[origine]?.[c] || 0);
  const tirage = rollD100();
  const total = Math.min(100, tirage + bonus);
  valeurs[c] = convertValeur(total);
  details[c] = { val: valeurs[c], bonus, tirage, total };
});

  const secondaires = {
    Déplacement: valeurs.HAB + valeurs.END,
    Initiative: valeurs.HAB + valeurs.COU,
    Vie: valeurs.FOR + valeurs.END + valeurs.COU,
    Encombrement: valeurs.FOR + valeurs.END,
    Fatigue: valeurs.END + valeurs.COU
  ,
    Canalisation: valeurs.INT + valeurs.COU
};

  
  const equipement = [];
  let orInitial = 0;
  if (rang.includes("Recrue")) orInitial = 20;
  if (rang.includes("Aguerri")) orInitial = 50;
  if (rang.includes("Expérimenté")) orInitial = 90;
  if (rang.includes("Élite")) orInitial = 140;
  if (rang.includes("Vétéran")) orInitial = 200;
  const orDisponible = orInitial;
  fichesOr.set(ficheId, orDisponible);

  fichesEquipement.set(ficheId, equipement);

  
  let texteRang = "";
  if (rang.includes("Recrue")) texteRang = "Choisir 1 compétence niveau 1.";
  if (rang.includes("Aguerri")) texteRang = "Choisir 1 compétence niveau 2 et 1 compétence niveau 1.";
  if (rang.includes("Expérimenté")) texteRang = "Choisir 2 compétences niveau 2 et 1 compétence niveau 1.";
  if (rang.includes("Élite")) texteRang = "Choisir 1 compétence niveau 3 et 2 compétences niveau 2.";
  if (rang.includes("Vétéran")) texteRang = "Choisir 3 compétences niveau 3, 2 compétences niveau 2 et 2 compétences niveau 1.";

  let texteAtout = "";
  if (rang.includes("Recrue")) texteAtout = "Choisir 1 atout.";
  if (rang.includes("Aguerri")) texteAtout = "Choisir 1 atout.";
  if (rang.includes("Expérimenté")) texteAtout = "Choisir 2 atouts.";
  if (rang.includes("Élite")) texteAtout = "Choisir 2 atouts.";
  if (rang.includes("Vétéran")) texteAtout = "Choisir 3 atouts.";

fiche.innerHTML = `
    <div style="display:flex; justify-content:space-between; align-items:center;">
      <h2>${nom}</h2>
      <button onclick="this.parentElement.parentElement.remove()" class="no-print" style="font-size:1.2rem;">✖</button>
    </div>
    <div class="ligne-haut"><span>Rôle : ${role}</span><span>Origine : ${origine === "ElfeHab" ? "Elfe noir" : origine === "ElfeInt" ? "Haut elfe" : origine}</span></div>
    <div class="ligne-haut"><span>Rang : ${rang}</span><span>Solde : <span class="solde">${calculerSolde(equipement, rang)}</span> Co</span></div>
    <h3>Caractéristiques</h3>
    <ul>${caracs.map(c => `<li>${c} : ${valeurs[c]}</li>`).join("")}</ul>
    <h3>Secondaires</h3>
    <ul>
      <li>Déplacement : ${secondaires.Déplacement}</li>
      <li>Initiative : ${secondaires.Initiative}</li>
      <li>Vie : ${secondaires.Vie}</li>
      <li>Encombrement : ${secondaires.Encombrement}</li>
      <li>Fatigue : ${secondaires.Fatigue}</li>
      <li>Canalisation : ${secondaires.Canalisation}</li>
    </ul>
    
<h3>Compétences</h3><p style="font-style:italic;" class="texte-rang hide-on-capture">${texteRang}</p>
<ul class="liste-competences"></ul>
<div class="equipement-zone">
  <select class="selectCompetence">
    ${competences.map(c => `<option value="${c}">${c}</option>`).join("")}
  </select>
  <select class="selectNiveau">
    <option value="I">I</option>
    <option value="II">II</option>
    <option value="III">III</option>
  </select>
  <button class="equiper-btn" onclick="ajouterCompetence(this)">Ajouter</button>
</div>

    <h3>Traits</h3><div>
  <strong>${traitNom}</strong><br>
  <span>${descriptionTraits[traitNom]}</span>
</div>
    <h3>Atouts</h3><p style="font-style:italic;" class="texte-atout hide-on-capture">${texteAtout}</p>
    <ul class="liste-atouts"></ul>
<div class="description-atout" style="margin-top:10px; font-style:italic;"></div>
<div class="description-atout" style="margin-top:10px; font-style:italic;"></div>
    <div class="equipement-zone">
      <select class="selectAtout" onchange="mettreAJourDescriptionAtout(this, role)" onchange="mettreAJourDescriptionAtout(this, role)">
        ${Object.keys(atoutsParRole[role] || {}).map(a => `<option value="${a}">${a}</option>`).join("")}
      </select>
      <button class="equiper-btn" onclick="ajouterAtout(this)">Ajouter</button>
    </div>
    <h3>Équipement</h3><div style="font-weight:bold;">Or possédé : <span class="or-pos">${orDisponible}</span> Co</div>
    <ul class="equipementListe"></ul>
    <div class="equipement-zone">
      <select class="selectEquip">
        ${equipementDisponible.map(e => `<option value="${e.nom}">${e.nom} (${e.prix}Co)</option>`).join("")}
      </select>
      <button class="equiper-btn" onclick="ajouterEquipement(this)">Équiper</button>
    </div>
  `;
  afficherEquipement(fiche);
}

function afficherEquipement(fiche) {
  const ul = fiche.querySelector(".equipementListe");
  const ficheId = fiche.dataset.id;
  const equipement = fichesEquipement.get(ficheId);
  ul.innerHTML = "";
  equipement.forEach(e => {
    const li = document.createElement("li");
    li.textContent = `${e.nom} (${e.prix}Co)`;
    const btn = document.createElement("button");
    btn.textContent = "✕";
    btn.className = "retirer-btn";
    btn.onclick = () => {
      const updated = equipement.filter(eq => eq.nom !== e.nom);
      fichesEquipement.set(ficheId, updated);
      afficherEquipement(fiche);
      fiche.querySelector(".solde").textContent = calculerSolde(updated, document.getElementById("rang").value);
    const newOr = fichesOr.get(ficheId) + e.prix;
    fichesOr.set(ficheId, newOr);
    fiche.querySelector(".or-pos").textContent = newOr;
    };
    li.appendChild(btn);
    ul.appendChild(li);
  });
}

function ajouterEquipement(button) {
  const fiche = button.closest(".fiche");
  const ficheId = fiche.dataset.id;
  const equipement = fichesEquipement.get(ficheId);
  const select = fiche.querySelector(".selectEquip");
  const nom = select.value;
  const item = equipementDisponible.find(e => e.nom === nom);
  if (!item || equipement.find(e => e.nom === nom)) return;
  if (fichesOr.get(ficheId) < item.prix) {
    alert("Pas assez d'or !");
    return;
  }
  equipement.push(item);
  fichesEquipement.set(ficheId, equipement);
  afficherEquipement(fiche);
  fiche.querySelector(".solde").textContent = calculerSolde(equipement, document.getElementById("rang").value);
    const newOr = fichesOr.get(ficheId) - item.prix;
    fichesOr.set(ficheId, newOr);
    fiche.querySelector(".or-pos").textContent = newOr;
}

function resetFiches() {
  document.getElementById("fiche").innerHTML = "";
}
</script><script>
window.onload = function () {
  fetch("changelog.html")
    .then(res => res.text())
    .then(html => {
      const content = document.getElementById("changelog-content");
      content.innerHTML = html;

      const versionDiv = content.querySelector("#changelog-version");
      const versionFromFile = versionDiv ? versionDiv.dataset.version : null;
      const versionVue = localStorage.getItem("grimworld_version_vue");

      if (versionFromFile && versionFromFile !== versionVue) {
        document.getElementById("changelog").style.display = "block";
      }
    });
};

function fermerChangelog() {
  const versionDiv = document.getElementById("changelog-content").querySelector("#changelog-version");
  const version = versionDiv ? versionDiv.dataset.version : "unknown";
  document.getElementById("changelog").style.display = "none";
  localStorage.setItem("grimworld_version_vue", version);
}

document.getElementById("changelog-icon").onclick = function () {
  document.getElementById("changelog").style.display = "block";
};
</script>
<div id="section-capitaine" style="display:none; text-align:left; margin-top:2rem;">
<h1>Grimworld - Générateur de Capitaine</h1>
<label>Rôle :</label>
<select id="role-capitaine">
<option value="Combattant">Combattant</option>
<option value="Gardien">Gardien</option>
<option value="Avant-Garde">Avant-Garde</option>
<option value="Érudit">Érudit</option>
</select>
<label>Origine :</label>
<select id="origine-capitaine">
<option value="Humain">Humain</option>
<option value="ElfeHab">Elfe noir</option>
<option value="ElfeInt">Haut elfe</option>
<option value="Nain">Nain</option>
<option value="Ogre">Ogre</option>
<option value="HommeRat">Homme-rat</option>
<option value="Orc">Orc</option>
<option value="Gobelin">Gobelin</option>
</select>
<label>Modus Operandi :</label>
<select id="modus">
<option value="La tactique avant tout">La tactique avant tout</option>
<option value="Foncer dans le tas">Foncer dans le tas</option>
</select>
<button class="generer" onclick="genererCapitaine()">Générer</button>
<button class="no-print" onclick="resetCapitaine()">Reset</button>
<div class="fiche" id="fiche-capitaine"></div>
<button class="no-print" onclick="captureImageCapitaine()">Enregistrer</button>
</div>
<div id="section-evenements" style="display:none; text-align:center; margin-top:2rem;">
<p><em>Coming soon...</em></p>
</div>
<div id="section-feuille" style="display:none; text-align:center; margin-top:2rem;">
<p><em>Coming soon...</em></p>
</div><div id="section-magasin" style="display:none; text-align:center; margin-top:2rem;"><h2>Magasin - Offre actuelle</h2><div id="magasin-stock" style="margin: 1rem auto;"></div><button onclick="genererStock()">Rafraîchir l'offre</button></div>
<script>
function afficherSection(id) {
  const sections = document.querySelectorAll("div[id^='section-']");
  sections.forEach(s => s.style.display = "none");
  const target = document.getElementById("section-" + id);
  if (target) target.style.display = "block";
}
</script><script>
document.addEventListener("DOMContentLoaded", () => {
  const ficheZone = document.getElementById("fiche");

  ficheZone.addEventListener("click", function(e) {
    if (e.target && e.target.classList.contains("equip-button")) {
      const container = e.target.closest(".fiche");
      const select = container.querySelector("select.selectEquip");
      const value = select.options[select.selectedIndex];
      const nom = value.value;

      const equipementList = container.querySelector(".equipements ul");
      const existants = [...equipementList.querySelectorAll("li")].map(li => li.dataset.nom);
      if (!existants.includes(nom)) {
        const item = document.createElement("li");
        item.dataset.nom = nom;
        item.textContent = `${value.value} (${value.dataset.degats}, ${value.dataset.prix} po) `;
        const btn = document.createElement("button");
        btn.textContent = "✕";
        btn.onclick = () => item.remove();
        btn.style.marginLeft = "0.5em";
        item.appendChild(btn);
        equipementList.appendChild(item);
      }
    }
  });
});

function ajouterCompetence(button) {
  const fiche = button.closest(".fiche");
  const selectCompetence = fiche.querySelector(".selectCompetence");
  const selectNiveau = fiche.querySelector(".selectNiveau");
  const nom = selectCompetence.value;
  const niveau = selectNiveau.value;
  const nomComplet = `${nom} ${niveau}`;

  const liste = fiche.querySelector(".liste-competences");
  const existants = [...liste.querySelectorAll("li")].map(li => li.dataset.nom);
  if (!existants.includes(nomComplet)) {
    const li = document.createElement("li");
    li.dataset.nom = nomComplet;
    li.innerHTML = `<strong>${nomComplet}</strong><br><span>${descriptionCompetences[nom]}</span>`;
    const btn = document.createElement("button");
    btn.textContent = "✕";
    btn.onclick = () => li.remove();
    btn.style.marginLeft = "0.5em";
    li.appendChild(btn);
    liste.appendChild(li);
  }
}

</script><script>
function genererStock() {
  const stockZone = document.getElementById("magasin-stock");

  const armes = ["Épée", "Hache", "Dague", "Arbalète", "Lance", "Claymore"];
  const armures = ["Cotte de mailles", "Armure de cuir", "Gambison", "Bouclier"];

  const communs = ["Torche", "Corde", "Carquois"];
  const peuCommuns = ["Sifflet", "Trousse de soins", "Potion de vigueur"];
  const rares = ["Grappin", "Potion de soin", "Balles de fronde"];
  const exceptionnels = ["Potion d'invisibilité", "Flèches elfiques", "Amulette ancienne"];

  const stock = {
    "Armes": [],
    "Armures": [],
    "Objets": [],
    "Consommables": [],
    "Munitions": []
  };

  const totalItems = Math.floor(Math.random() * 11) + 10;

  while (Object.values(stock).flat().length < totalItems) {
    const choix = Math.random();
    let nom = "", rarete = "", prix = 0, type = "";

    if (choix < 0.5) {
      const isArme = Math.random() < 0.5;
      const liste = isArme ? armes : armures;
      nom = liste[Math.floor(Math.random() * liste.length)];
      type = isArme ? "Armes" : "Armures";
      const baseItem = equipementDisponible.find(e => e.nom === nom);
      const basePrix = baseItem ? baseItem.prix : 10;
      const roll = Math.floor(Math.random() * 100) + 1;
      if (roll <= 30) { rarete = "Commun"; prix = basePrix; }
      else if (roll <= 70) { rarete = "Peu commun"; prix = basePrix + 10; }
      else if (roll <= 90) { rarete = "Rare"; prix = basePrix + 20; }
      else { rarete = "Exceptionnel"; prix = basePrix + 50; }
    } else {
      const tirage = Math.random() * 100;
      if (tirage <= 50 && communs.length > 0) {
        nom = communs[Math.floor(Math.random() * communs.length)];
        rarete = "Commun"; prix = 10;
        type = nom === "Carquois" ? "Munitions" : "Objets";
      } else if (tirage <= 80 && peuCommuns.length > 0) {
        nom = peuCommuns[Math.floor(Math.random() * peuCommuns.length)];
        rarete = "Peu commun"; prix = 20;
        type = nom.includes("Potion") ? "Consommables" : "Objets";
      } else if (tirage <= 95 && rares.length > 0) {
        nom = rares[Math.floor(Math.random() * rares.length)];
        rarete = "Rare"; prix = 30;
        type = nom.includes("Potion") ? "Consommables" : (nom.includes("fronde") ? "Munitions" : "Objets");
      } else if (exceptionnels.length > 0) {
        nom = exceptionnels[Math.floor(Math.random() * exceptionnels.length)];
        rarete = "Exceptionnel"; prix = 50;
        type = nom.includes("Potion") ? "Consommables" : (nom.includes("Flèches") ? "Munitions" : "Objets");
      } else {
        continue;
      }
    }

    prix = Math.max(5, Math.round(prix / 5) * 5);
    stock[type].push({ nom, rarete, prix });
  }

  let lignes = '';
  for (const [categorie, objets] of Object.entries(stock)) {
    if (objets.length === 0) continue;
    lignes += `<tr><th colspan="3" style="background:#222; color:white;">— ${categorie.toUpperCase()} —</th></tr>`;
    objets.forEach(o => {
      lignes += `
        <tr>
          <td style="border:1px solid #999; padding:4px;">${o.nom}</td>
          <td style="border:1px solid #999; padding:4px;">${o.rarete}</td>
          <td style="border:1px solid #999; padding:4px;">${o.prix} Co</td>
        </tr>`;
    });
  }

  stockZone.innerHTML = `
    <table style="margin:auto; border-collapse: collapse; width:90%;">
      <thead>
        <tr style="background:#ddd;">
          <th style="border:1px solid #999; padding:4px;">Objet</th>
          <th style="border:1px solid #999; padding:4px;">Rareté</th>
          <th style="border:1px solid #999; padding:4px;">Prix</th>
        </tr>
      </thead>
      <tbody>${lignes}</tbody>
    </table>`;
}

document.addEventListener("DOMContentLoaded", genererStock);
</script>
<script>

function genererCapitaine() {
  const container = document.getElementById("fiche-capitaine");
  container.innerHTML = "";
  const fiche = document.createElement("div");
  fiche.className = "fiche";
  const ficheId = crypto.randomUUID().replace(/-/g, "");
  fiche.dataset.id = ficheId;
  container.appendChild(fiche);

  const role = document.getElementById("role-capitaine").value;
  const origine = document.getElementById("origine-capitaine").value;
  const modus = document.getElementById("modus").value;
  const traitNom = traits[Math.floor(Math.random() * traits.length)];
  const nom = genererNom();

  const caracs = ["FOR", "END", "HAB", "INT", "COU"];
  const valeurs = {};
const details = {};
caracs.forEach(c => {
  const bonus = (bonusRoles[role]?.[c] || 0) + (bonusOrigines[origine]?.[c] || 0);
  const tirage = rollD100();
  const total = Math.min(100, tirage + bonus);
  valeurs[c] = convertValeur(total);
  details[c] = { val: valeurs[c], bonus, tirage, total };
});

  const secondaires = {
    Déplacement: valeurs.HAB + valeurs.END,
    Initiative: valeurs.HAB + valeurs.COU,
    Vie: valeurs.FOR + valeurs.END + valeurs.COU,
    Encombrement: valeurs.FOR + valeurs.END,
    Fatigue: valeurs.END + valeurs.COU,
    Canalisation: valeurs.INT + valeurs.COU,
    Commandement: valeurs.INT + valeurs.COU
  };

  const orInitial = 200;
  const orDisponible = orInitial;
  fichesOr.set(ficheId, orDisponible);
  fichesEquipement.set(ficheId, []);

  fiche.innerHTML = `
    <div style="display:flex; justify-content:space-between; align-items:center;">
      <h2>${nom}</h2>
      <button onclick="this.parentElement.parentElement.remove()" class="no-print" style="font-size:1.2rem;">✖</button>
    </div>
    <div class="ligne-haut"><span>Modus Operandi : ${modus}</span><span>Solde : <span class="solde">0</span> Co</span></div>
    <h3>Caractéristiques</h3>
    <ul>${caracs.map(c => `<li>${c} : ${valeurs[c]}</li>`).join("")}</ul>
    <h3>Secondaires</h3>
    <ul>
      <li>Déplacement : ${secondaires.Déplacement}</li>
      <li>Initiative : ${secondaires.Initiative}</li>
      <li>Vie : ${secondaires.Vie}</li>
      <li>Encombrement : ${secondaires.Encombrement}</li>
      <li>Fatigue : ${secondaires.Fatigue}</li>
      <li>Canalisation : ${secondaires.Canalisation}</li>
      <li>Commandement : ${secondaires.Commandement}</li>
    </ul>

    <h3>Ordres</h3><p style="font-style:italic;">Choisissez 1 ordre de Capitaine</p>
    <ul class="liste-ordres"></ul>
    <div class="equipement-zone">
      <select class="selectOrdre">
        <option value="Ralliement !">Ralliement !</option>
        <option value="Tenez la position!">Tenez la position!</option>
      </select>
      <button class="equiper-btn" onclick="ajouterOrdre(this)">Ajouter</button>
    </div>

    <h3>Traits</h3><div>
      <strong>${traitNom}</strong><br>
      <span>${descriptionTraits[traitNom]}</span>
    </div>

    <h3>Atouts</h3><p style="font-style:italic;">Choisissez 1 atout</p><ul class="liste-atouts"></ul>
<div class="description-atout" style="margin-top:10px; font-style:italic;"></div>
<div class="description-atout" style="margin-top:10px; font-style:italic;"></div>
    <div class="equipement-zone">
      <select class="selectAtout" onchange="mettreAJourDescriptionAtout(this, role)" onchange="mettreAJourDescriptionAtout(this, role)">
        ${Object.keys(atoutsParRole[role] || {}).map(a => `<option value="${a}">${a}</option>`).join("")}
      </select>
      <button class="equiper-btn" onclick="ajouterAtout(this)">Ajouter</button>
    </div>

    <h3>Équipement</h3><div style="font-weight:bold;">Or possédé : <span class="or-pos">${orDisponible}</span> Co</div>
    <ul class="equipementListe"></ul>
    <div class="equipement-zone">
      <select class="selectEquip">
        ${equipementDisponible.map(e => `<option value="${e.nom}">${e.nom} (${e.prix}Co)</option>`).join("")}
      </select>
      <button class="equiper-btn" onclick="ajouterEquipement(this)">Équiper</button>
    </div>
  `;

  fiche.querySelector(".solde").textContent = orInitial;
  afficherEquipement(fiche);
}

function captureImageCapitaine() {
  const node = document.getElementById("fiche-capitaine");
  if (!node || node.children.length === 0) {
    alert("Aucune fiche à enregistrer !");
    return;
  }
  const boutons = node.querySelectorAll("button, .equipement-zone, select, label");
  boutons.forEach(b => b.style.visibility = "hidden");
  html2canvas(node).then(canvas => {
    const link = document.createElement("a");
    link.download = "grimworld_capitaine.png";
    link.href = canvas.toDataURL();
    link.click();
    boutons.forEach(b => b.style.visibility = "visible");
  });
}

function ajouterOrdre(button) {
  const fiche = button.closest(".fiche");
  const select = fiche.querySelector(".selectOrdre");
  const nom = select.value;
  const liste = fiche.querySelector(".liste-ordres");
  const existants = [...liste.querySelectorAll("li")].map(li => li.dataset.nom);
  if (!existants.includes(nom)) {
    const li = document.createElement("li");
    li.dataset.nom = nom;
    li.textContent = nom + " ";
    const btn = document.createElement("button");
    btn.textContent = "✕";
    btn.onclick = () => li.remove();
    btn.style.marginLeft = "0.5em";
    li.appendChild(btn);
    liste.appendChild(li);
  }
}
</script>
<script>
function mettreAJourDescriptionAtout(select, role) {
  const descriptionBox = select.closest(".fiche").querySelector(".description-atout");
  const atout = select.value;
  const desc = atoutsParRole[role]?.[atout] || "";
  descriptionBox.innerHTML = desc.replace(/\*\*(.*?)\*\*/g, "<strong>$1</strong>");
}

function ajouterAtout(button) {
  const fiche = button.closest(".fiche");
  const select = fiche.querySelector(".selectAtout");
  const nom = select.value;
  const role = fiche.querySelector(".selectAtout").getAttribute("data-role") || "Combattant";
  const desc = atoutsParRole[role]?.[nom] || "";
  const liste = fiche.querySelector(".liste-atouts");
  const existants = [...liste.querySelectorAll("li")].map(li => li.dataset.nom);
  if (!existants.includes(nom)) {
    const li = document.createElement("li");
    li.dataset.nom = nom;
    li.innerHTML = "<strong>" + nom + "</strong><br><em>" + desc.replace(/\*\*(.*?)\*\*/g, "<strong>$1</strong>") + "</em>";
    const btn = document.createElement("button");
    btn.textContent = "✕";
    btn.onclick = () => li.remove();
    btn.style.marginLeft = "0.5em";
    li.appendChild(btn);
    liste.appendChild(li);
  }
}
</script>

<script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
<script>
function captureImage() {
  const node = document.getElementById("fiche");
  if (!node || node.children.length === 0) {
    alert("Aucune fiche à enregistrer !");
    return;
  }
  node.classList.add("compact");

  const elementsToHide = node.querySelectorAll("button, .equipement-zone, select, label");
  elementsToHide.forEach(e => e.style.display = "none");

  html2canvas(node).then(canvas => {
    const link = document.createElement("a");
    link.download = "grimworld_mercenaires.png";
    link.href = canvas.toDataURL();
    link.click();

    elementsToHide.forEach(e => e.style.display = "");
    node.classList.remove("compact");
  });
}

function captureImageCapitaine() {
  const node = document.getElementById("fiche-capitaine");
  if (!node || node.children.length === 0) {
    alert("Aucune fiche à enregistrer !");
    return;
  }
  node.classList.add("compact");

  const elementsToHide = node.querySelectorAll("button, .equipement-zone, select, label");
  elementsToHide.forEach(e => e.style.display = "none");

  html2canvas(node).then(canvas => {
    const link = document.createElement("a");
    link.download = "grimworld_capitaine.png";
    link.href = canvas.toDataURL();
    link.click();

    elementsToHide.forEach(e => e.style.display = "");
    node.classList.remove("compact");
  });
}
</script>


<script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
<script>
function captureImage() {
  const node = document.getElementById("fiche");
  if (!node || node.children.length === 0) {
    alert("Aucune fiche à enregistrer !");
    return;
  }
  node.classList.add("compact");

  const elementsToHide = node.querySelectorAll("button, .equipement-zone, select, label, .hide-on-capture");
  elementsToHide.forEach(e => e.style.display = "none");

  html2canvas(node).then(canvas => {
    const link = document.createElement("a");
    link.download = "grimworld_mercenaires.png";
    link.href = canvas.toDataURL();
    link.click();

    elementsToHide.forEach(e => e.style.display = "");
    node.classList.remove("compact");
  });
}

function captureImageCapitaine() {
  const node = document.getElementById("fiche-capitaine");
  if (!node || node.children.length === 0) {
    alert("Aucune fiche à enregistrer !");
    return;
  }
  node.classList.add("compact");

  const elementsToHide = node.querySelectorAll("button, .equipement-zone, select, label, .hide-on-capture");
  elementsToHide.forEach(e => e.style.display = "none");

  html2canvas(node).then(canvas => {
    const link = document.createElement("a");
    link.download = "grimworld_capitaine.png";
    link.href = canvas.toDataURL();
    link.click();

    elementsToHide.forEach(e => e.style.display = "");
    node.classList.remove("compact");
  });
}
</script>

</body>
</html>
<script>
function resetCapitaine() {
  const container = document.getElementById("fiche-capitaine");
  if (container) container.innerHTML = "";
}
</script>
<script>
function mettreAJourDescriptionAtout(select, role) {
  const descriptionBox = select.closest(".fiche").querySelector(".description-atout");
  const atout = select.value;
  const desc = atoutsParRole[role]?.[atout] || "";
  descriptionBox.innerHTML = desc.replace(/\*\*(.*?)\*\*/g, "<strong>$1</strong>");
}
</script>
