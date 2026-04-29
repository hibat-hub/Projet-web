Explication complète du code HTML/CSS et JAVASCRIPT
les balises essentielle utilises:
<html>Racine de toute la page
  <head>Infos techniques (non visibles)
    <body>Contenu visible
      <header>En-tête / barre de navigation
        <nav>Zone de navigation
          <a>Lien cliquable
            <section>Section de contenu
              <div>Conteneur générique
                <h1>, <h2>Titres 
                  <p>Paragraphe de texte
                    <img>Image
                     <button>Bouton cliquable
                      <span>Conteneur inline (en ligne)
                        <footer>Pied de page
                          <script>Code JavaScript
                           <link>Importer ressource externe (police...) 
                            <meta>Métadonnées (charset, viewport...)
STRUCTURE GÉNÉRALE
Un fichier HTML est divisé en 3 grandes parties :
<!DOCTYPE html>  ← déclaration du type de fichier
<html>           ← début de la page
  <head>         ← informations cachées (non visibles sur la page)
  <body>         ← contenu visible sur la page
</html>          ← fin de la page

 PARTIE 1 — Le <head> (en-tête invisible)
<!DOCTYPE html>
Dit au navigateur : "Ce fichier est un document HTML5". Toujours la 1ère ligne.
<head>
 Début de la zone d'informations techniques (non affichée à l'écran).
<title>Trips with Sara</title>
 Le texte qui apparaît dans l'onglet du navigateur.
<meta name="viewport" content="width=device-width, initial-scale=1.0">
 Rend la page responsive (adaptée aux téléphones). Sans ça, la page serait trop petite sur mobile.
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display..." rel="stylesheet"/>
 Importe 2 polices de Google Fonts :
Playfair Display → police élégante avec empattements (pour les titres)
Lato → police moderne et lisible (pour le texte normal)

 PARTIE 2 — Le CSS (le style)
Les variables CSS
:root {
    --gold: #c9a84c;
    --dark: #1a1a1a;
    --bg: #faf9f7;
    --text: #2c2c2c;
}
:root = la racine de la page entière. On définit des variables réutilisables :

--gold → couleur dorée (utilisée partout dans le site)
--dark → noir profond
--bg → blanc cassé (fond de page)
--text → gris foncé (couleur du texte)

Au lieu d'écrire #c9a84c 10 fois, on écrit var(--gold). Si on veut changer la couleur, on la change une seule fois.

Le style de base
* { margin: 0; padding: 0; box-sizing: border-box; }
* = s'applique à tous les éléments. On supprime les marges et espacements par défaut du navigateur.
box-sizing: border-box = la taille des éléments inclut les bordures.
html { scroll-behavior: smooth; }
Quand on clique sur un lien de navigation, le défilement est fluide.
body {
    font-family: 'Lato', sans-serif;
    background-color: var(--bg);
    color: var(--text);
}
 Applique à toute la page : la police Lato, le fond blanc cassé, et le texte gris foncé.

Le Header (barre de navigation)
header {
    background-color: rgba(26,26,26,0.95);
    backdrop-filter: blur(10px);
    color: white;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 18px 50px;
    position: fixed;
    width: 100%;
    top: 0;
    z-index: 100;
    border-bottom: 1px solid rgba(201,168,76,0.3);
    flex-wrap: wrap;
}
Propriété par propriété :
background-color: rgba(...)Fond noir à 95% de transparence
backdrop-filter: blur(10px)Flou artistique derrière le header
display: flexAligne les éléments en ligne (logo + nav)
justify-content: space-betweenLogo à gauche, nav à droite
align-items: centerCentre verticalement
padding: 18px 50pxEspace intérieur (haut/bas : 18px, gauche/droite : 50px)
position: fixedReste collé en haut même quand on scroll
width: 100%Prend toute la largeur de l'écran
top: 0Collé tout en haut
z-index: 100Passe au-dessus de tous les autres éléments
border-bottomLigne dorée fine en bas du header

Le logo
.logo img {
    width: 80px;
    height: 80px;
    border-radius: 50%;
    object-fit: cover;
}
 L'image du logo est en cercle (border-radius: 50%), taille 80x80px. 
 object-fit: cover = l'image remplit le cercle sans se déformer.

Le bouton menu barrenav (mobile)
.barrenav {
    display: none;        /* Caché sur ordinateur */
    flex-direction: column;
    gap: 5px;
    width: 34px;
    cursor: pointer;
    background: none;
    border: none;
    padding: 4px;
}
.barrenav span {
    display: block;
    width: 100%;
    height: 2px;
    background: var(--gold);
    border-radius: 2px;
}
 Ce sont les 3 barres du menu barrenav (≡) visible sur téléphone.
 Chaque <span> = une barre dorée.

Les liens de navigation
nav a {
    color: #ddd;
    padding: 6px 14px;
    text-decoration: none;
    font-size: 0.85em;
    text-transform: uppercase;
    font-weight: 500;
    letter-spacing: 0.08em;
    position: relative;
}
Les liens sont en majuscules, gris clair, sans soulignement, espacés entre les lettres.
nav a::after {
    content: '';
    position: absolute;
    left: 0;
    bottom: -4px;
    width: 0;
    height: 2px;
    background: var(--gold);
    transition: width 0.3s ease;
}
nav a:hover::after { width: 100%; }
::after crée un pseudo-élément (une ligne invisible sous chaque lien). Au survol (hover), la ligne dorée s'étend de gauche à droite en 0.3 secondes.
C'est une animation CSS !
nav a.active { color: var(--gold); }
nav a.active::after { width: 100%; }
 Le lien de la page actuelle est doré avec la ligne visible en permanence.

La section UP-text (grande image d'accueil)
section#accueil {
    background-image: url("images/image.avif");
    background-size: cover;
    background-position: center;
    width: 100%;
    height: 70vh;
    margin-top: 116px;
    position: relative;
    display: flex;
    align-items: flex-end;
    justify-content: center;
}
 La grande image en haut de la page :

background-size: cover → l'image remplit tout l'espace sans se déformer
height: 70vh → hauteur = 70% de l'écran
margin-top: 116px → espace pour ne pas être caché par le header fixe
align-items: flex-end → le texte est placé en bas de l'image

section#accueil::after {
    content: '';
    position: absolute;
    bottom: 0; left: 0; right: 0;
    height: 50%;
    background: linear-gradient(to bottom, transparent, var(--bg));
}
 Un dégradé qui fond l'image vers le fond blanc en bas. Effet visuel élégant.
.UP-text {
    position: relative;
    z-index: 2;
    text-align: center;
    padding-bottom: 40px;
    color: white;
}
 Le texte est au-dessus du dégradé (z-index: 2), centré, avec espace en bas.
.UP-text h1 {
    font-family: 'Playfair Display', serif;
    font-size: 3rem;
    text-shadow: 0 2px 20px rgba(0,0,0,0.5);
}
 Titre principal : grande police élégante, ombre noire pour lisibilité sur l'image.

La section "About Us"
section.about-us {
    padding: 70px 40px 80px;
    display: flex;
    flex-direction: column;
    align-items: center;
}
 Section centrée verticalement avec espacements confortables.
.PARAG {
    width: 60px;
    height: 2px;
    background: var(--gold);
    margin: 0 auto 40px;
}
La petite ligne dorée décorative sous le titre "About Us".
.about-box {
    max-width: 820px;
    background: #fff;
    border: 1px solid #e8e0d0;
    border-top: 4px solid var(--gold);
    padding: 50px 55px;
    box-shadow: 0 8px 40px rgba(0,0,0,0.07);
}
 La carte blanche du texte :

max-width: 820px → ne dépasse pas 820px (reste lisible)
border-top: 4px solid var(--gold) → barre dorée épaisse en haut
box-shadow → ombre légère pour un effet de carte surélevée


Le responsive (mobile)
@media (max-width: 768px) {
    .barrenav { display: flex; }  /* Affiche le menu barrenav */
    nav { display: none; }         /* Cache la nav horizontale */
    nav.open { display: flex; }    /* La montre si ouverte */
    section#accueil { height: 55vh; margin-top: 80px; }
    .UP-text h1 { font-size: 2rem; }
    .about-box { padding: 32px 24px; }
}
 @media (max-width: 768px) = s'applique uniquement sur écrans ≤ 768px (téléphones). Le menu barrenav apparaît, la navigation se cache et s'ouvre au clic, les tailles sont réduites.

PARTIE 3 — Le <body> (contenu visible)
Le Header HTML
<header>
    <div class="logo"><img src="images/logo.jpeg" alt="logo"></div>
 <header> = zone d'en-tête. Le logo est une image dans un <div>.
  <button class="barrenav" onclick="toggleMenu()">
        <span></span><span></span><span></span>
    </button>
 Bouton barrenav avec 3 <span> (les 3 barres). Au clic → appelle la fonction toggleMenu().
    <nav id="mainNav">
        <a href="index.html" class="active">Accueil</a>
        <a href="page2.html">Activités</a>
        <a href="page3.html">Excursions</a>
        <a href="page4.html">Contact</a>
        <a href="page5.html">Avis</a>
    </nav>
</header>
<nav> = barre de navigation. Chaque <a href="..."> = un lien vers une page. class="active" sur Accueil car c'est la page actuelle.

La section Hero
<section id="accueil">
    <div class="UP-text">
        <h1>Discover Marrakech With Us</h1>
        <p>Authentic experiences in Marrakech &amp; beyond</p>
    </div>
</section>
 Grande section avec l'image de fond. &amp; = le symbole & en HTML (écriture sécurisée). <h1> = titre principal (le plus important de la page).

La section About Us
<section class="about-us">
    <h2>About Us</h2>
    <div class="PARAG"></div>
    <div class="about-box">
        <p>At Trips with Sara, we specialize in...</p>
        <div class="signature">— Trips with Sara —</div>
    </div>
</section>
 <h2> = titre secondaire. <div class="PARAG"> = la ligne dorée décorative (vide, mais stylée en CSS). <div class="about-box"> = la carte blanche avec le texte.

Le Footer
<footer>
    <span>Trips with Sara</span>
    <p>&copy; Marrakech, Morocco — 2026</p>
</footer>
 Pied de page. &copy; = le symbole copyright ©.

Le JavaScript
<script>
function toggleMenu() {
    var nav = document.getElementById('mainNav');
    nav.className = nav.className === 'open' ? '' : 'open';
}
</script>
 La fonction qui ouvre/ferme le menu sur mobile :

getElementById('mainNav') → trouve l'élément nav
Si la classe est 'open' → on la supprime (menu se ferme)
Sinon → on ajoute 'open' (menu s'ouvre)

C'est ce qu'on appelle un toggle (interrupteur).
