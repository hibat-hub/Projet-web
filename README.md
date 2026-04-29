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

La section UP
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

Explication du code NOUVEAU dans page2.html 
Seulement les éléments nouveaux qui n'existaient pas dans la page 1 

 1 — La section UP (différente de page 1)
Page 1 avait une grande image en fond. Page 2 utilise un dégradé de couleurs :
.up-text {
    margin-top: 116px;
    padding: 80px 40px 60px;
    text-align: center;
    background: linear-gradient(135deg, #1a1a1a 0%, #2c2416 100%);
    color: white;
}
 linear-gradient(135deg, #1a1a1a 0%, #2c2416 100%) = dégradé diagonal (135°) du noir vers un marron très foncé. Pas d'image, juste des couleurs.
<section class="up-text">
    <p>Découvrez</p>
    <h1>Nos Activités</h1>
    <div class="PARAG"></div>
</section>
Le <p> est au-dessus du <h1> (inverse de page 1). La ligne dorée .PARAG est en dessous du titre.

2 — Le système de grille (Grid)
.activity {
    display: grid;
    grid-template-columns: 1fr 1fr;
    ...
}
 display: grid = système de grille. grid-template-columns: 1fr 1fr = 2 colonnes égales (image à gauche, texte à droite).
C'est différent de display: flex — grid est fait pour des layouts en 2D (lignes ET colonnes).
.activity:nth-child(even) { direction: rtl; }
.activity:nth-child(even) > * { direction: ltr; }
 :nth-child(even) = les activités paires (02, 04). direction: rtl = Right To Left → inverse l'ordre : texte à gauche, image à droite. Puis direction: ltr sur les enfants pour que le texte reste normal (gauche à droite).

 3 — Le Slider (carrousel d'images)
C'est la partie la plus nouvelle et complexe !
CSS du slider
.activity-slider {
    position: relative;
    overflow: hidden;
    min-height: 380px;
}
 Le conteneur du slider. overflow: hidden = cache les images qui dépassent.
.activity-slider .slide {
    position: absolute;
    inset: 0;
    opacity: 0;
    transition: opacity 0.6s ease;
    background-size: cover;
    background-position: center;
}
.activity-slider .slide.active { opacity: 1; }
Toutes les images sont superposées (position: absolute, inset: 0 = couvre tout). Elles sont invisibles (opacity: 0) sauf celle avec la classe active (opacity: 1). La transition de 0.6s = fondu enchaîné entre les images.
.activity-slider .s-arrow {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    z-index: 10;
    width: 34px; height: 34px;
    background: rgba(201,168,76,0.85);
    ...
}
.activity-slider .s-arrow.prev { left: 10px; }
.activity-slider .s-arrow.next { right: 10px; }
 Les flèches gauche/droite. top: 50% + translateY(-50%) = parfaitement centrées verticalement. .prev à gauche, .next à droite.
.s-dot {
    width: 7px; height: 7px;
    border-radius: 50%;
    background: rgba(255,255,255,0.5);
    transition: background 0.3s, transform 0.3s;
}
.s-dot.active {
    background: var(--gold);
    transform: scale(1.3);
}
Les petits points en bas du slider. Le point actif est doré et légèrement agrandi.

HTML du slider
<div class="activity-slider" 
     data-slides='["images/agafay-1.jpeg","images/agafay-2.jpeg","images/agafay-3.jpeg"]'>
    <div class="s-dots"></div>
    <button class="s-arrow prev">&#8249;</button>
    <button class="s-arrow next">&#8250;</button>
</div>
 data-slides='[...]' = attribut personnalisé (data attribute). Stocke la liste des images en format JSON. Le JavaScript va lire cette liste pour créer les slides automatiquement.
&#8249; = le caractère ‹ (flèche gauche)
&#8250; = le caractère › (flèche droite)

 Le <article> vs <div>
<article class="activity">
 Page 1 utilisait <div>. Ici on utilise <article> = balise sémantique qui signifie "contenu indépendant" (chaque activité est un article complet). C'est mieux pour le SEO et l'accessibilité.

 4 — JavaScript du Slider (le plus important)
document.querySelectorAll('.activity-slider').forEach(function(slider) {
 Sélectionne tous les sliders de la page et fait une boucle sur chacun.
var images = JSON.parse(slider.dataset.slides);
 Lit la liste d'images depuis data-slides et la convertit en tableau JavaScript.
Ex: ["agafay-1.jpeg", "agafay-2.jpeg", "agafay-3.jpeg"]
images.forEach(function(src, i) {
    var div = document.createElement('div');
    div.className = 'slide' + (i === 0 ? ' active' : '');
    div.style.backgroundImage = "url('" + src + "')";
    slider.insertBefore(div, dotsEl);
});
 Pour chaque image → crée un <div> avec la classe slide, met l'image en fond, et l'insère dans le slider. La première image (i === 0) reçoit aussi la classe active.
images.forEach(function(_, i) {
    var d = document.createElement('button');
    d.className = 's-dot' + (i === 0 ? ' active' : '');
    d.onclick = function() { goTo(i); };
    dotsEl.appendChild(d);
});
 Crée un point pour chaque image. Au clic → appelle goTo(i).
if (images.length <= 1) {
    slider.querySelectorAll('.s-arrow').forEach(function(a) { a.style.display = 'none'; });
    dotsEl.style.display = 'none';
}
Si une activité a une seule image → cache les flèches et les points (inutiles).
function goTo(n) {
    allSlides[current].classList.remove('active');
    allDots[current].classList.remove('active');
    current = (n + images.length) % images.length;
    allSlides[current].classList.add('active');
    allDots[current].classList.add('active');
}
 La fonction principale du slider :

Enlève active de l'image et du point actuel
Calcule le nouvel index avec % (modulo) → permet de boucler (après la dernière image, retour à la première)
Ajoute active à la nouvelle image et son point

slider.querySelector('.s-arrow.prev').onclick = function() { goTo(current - 1); };
slider.querySelector('.s-arrow.next').onclick = function() { goTo(current + 1); };
 Flèche gauche → image précédente. Flèche droite → image suivante.

Résumé — Ce qui est nouveau
linear-gradient= UP-text sans image, juste couleurs
display: grid =Mise en page 2 colonnes
:nth-child(even) + direction: rtl=Alternance image/texte
<article>=Balise sémantique (vs <div>)
data-slides=Attribut personnalisé pour stocker données
Slider complet=Carrousel d'images avec flèches et points
opacity + transition=Animation de fondu entre images
JSON.parse=Lire données JSON en JavaScript
createElement=Créer des éléments HTML via JavaScript
% modulo=Boucler le slider (retour au début)






Éléments NOUVEAUX dans page3.html 
Seulement les éléments nouveaux qui n'existaient pas dans la page 2 

 1 — UP plus élaboré
Le ::before (nouveau !)
.UP-text::before {
    content: '';
    position: absolute;
    inset: 0;
    background: radial-gradient(ellipse at center, rgba(201,168,76,0.08) 0%, transparent 70%);
}
 ::before = pseudo-élément placé avant le contenu. Crée un halo doré subtil au centre du hero. radial-gradient = dégradé circulaire (du centre vers l'extérieur), différent de linear-gradient qui est en ligne droite.
Le .UP-text-tag (nouveau !)
.up-text .UP-text-tag {
    display: inline-block;
    border: 1px solid rgba(201,168,76,0.4);
    padding: 6px 20px;
}
<div class="UP-text-tag">Voyages &amp; Séjours</div>
Une petite étiquette encadrée dorée au-dessus du titre. N'existait pas dans les pages précédentes.
Le .hero-sub (nouveau !)
<p class="hero-sub">Évadez-vous au Maroc...</p>
 Un sous-titre en blanc semi-transparent sous le titre principal. Page 2 n'avait pas ça.

2 — Le compteur de photos
CSS
.excursion-slider .photo-counter {
    position: absolute;
    top: 16px; right: 16px;
    z-index: 10;
    background: rgba(26,26,26,0.75);
    color: var(--gold);
    font-size: 0.72rem;
    padding: 5px 12px;
    backdrop-filter: blur(4px);
}
Une pastille en haut à droite du slider qui affiche "1 / 4", "2 / 4"... Page 2 n'avait pas ça.
HTML
<div class="photo-counter"></div>
 Vide dans le HTML — c'est le JavaScript qui remplit le texte.
JavaScript
javascriptvar counter = slider.querySelector('.photo-counter');

function updateCounter() { 
    counter.textContent = (current + 1) + ' / ' + images.length; 
}
updateCounter(); // Affiche "1 / 4" au départ
 textContent = modifie le texte à l'intérieur d'un élément.
(current + 1) = on ajoute 1 car les tableaux commencent à 0 (image 0 = "1/4").
updateCounter() est aussi appelée dans goTo() pour mettre à jour à chaque changement.
Différence avec page 2
Page 2 → pas de compteur
Page 3 → compteur "1 / 4" en haut à droite 

 3 — L'ombre sur les slides
.excursion-slider .slide::after {
    content: '';
    position: absolute;
    inset: 0;
    background: linear-gradient(to top, rgba(15,10,3,0.45) 0%, transparent 50%);
}
Chaque image a une ombre en bas (dégradé du noir transparent vers le haut). Donne un effet cinématographique. Page 2 n'avait pas ça sur les slides.

 4 — Les Badges
.badge { font-size: 0.75rem; text-transform: uppercase; padding: 5px 14px; }
.badge-gold { background: var(--gold); color: var(--dark); }
.badge-outline { border: 1px solid var(--gold); color: var(--gold); }
.badge-dark { background: var(--dark); color: rgba(255,255,255,0.7); }
<div class="badges">
    <span class="badge badge-gold">Journée</span>
    <span class="badge badge-outline">Transfert inclus</span>
    <span class="badge badge-dark">Privé</span>
</div>
 Des étiquettes colorées avec 3 styles différents :

Doré plein → durée
Contour doré → ce qui est inclus
Fond noir → type de service

Page 2 utilisait juste .meta (texte simple). Page 3 utilise des badges visuels.
 5 — Le séparateur .content-divider
.content-divider {
    width: 40px;
    height: 1px;
    background: var(--gold);
    opacity: 0.6;
    margin-bottom: 20px;
}
<div class="content-divider"></div>
 Une petite ligne dorée horizontale entre les badges et le contenu. Sert à séparer visuellement les sections.

 6 — La liste "Inclus"
.includes li::before {
    content: '';
    display: inline-block;
    width: 6px; height: 6px;
    background: var(--gold);
    border-radius: 50%;
    flex-shrink: 0;
}
<ul class="includes">
    <li>Transport privé aller-retour</li>
    <li>Chauffeur professionnel</li>
</ul>
 Une liste <ul> sans les puces par défaut (list-style: none). À la place, ::before crée un petit rond doré devant chaque item. C'est plus élégant que les puces normales.

 7 — Le Programme (timeline)
C'est l'élément le plus complexe et nouveau !
La ligne verticale
.prog-step:not(:last-child)::after {
    content: '';
    position: absolute;
    left: 15px;
    top: 32px; bottom: 0;
    width: 1px;
    background: #e8e0d0;
}
 :not(:last-child) = s'applique à tous les steps sauf le dernier. Crée une ligne verticale entre les étapes (comme une timeline). Elle part du bas de l'icône (top: 32px) jusqu'en bas.
L'icône ronde
.prog-icon {
    width: 32px; height: 32px;
    border-radius: 50%;
    background: #faf4e8;
    border: 1px solid #e8d9b4;
    flex-shrink: 0;
    z-index: 1;
}
<div class="prog-icon">🚐</div>
 Chaque étape a une icône emoji dans un cercle doré clair. z-index: 1 pour qu'elle passe au-dessus de la ligne verticale.
Le tag "optionnel"
.opt-tag {
    font-size: 0.68rem;
    color: var(--gold);
    border: 1px solid rgba(201,168,76,0.4);
    padding: 1px 7px;
    margin-left: 6px;
    vertical-align: middle;
}
<span class="opt-tag">optionnel</span>
 Une petite étiquette inline qui indique que cette étape est optionnelle.
Les flèches › dans la liste
.prog-detail ul li::before {
    content: '›';
    color: var(--gold);
}
 Au lieu de ronds, ici les sous-listes utilisent le symbole › doré comme puce.

 8 — overflow-y: auto sur le contenu
.excursion-content {
    overflow-y: auto;
}

 Résumé — Ce qui est nouveau
ÉlémentNouveauté::before + radial-gradientHalo doré dans UP-TEXT
.UP-TEXT-tagÉtiquette encadrée au-dessus du titre
.UP-TEXT-subSous-titre sous le h1
.photo-counterCompteur "1/4" sur le slider
slide::afterOmbre en bas de chaque image
.badgesÉtiquettes colorées (3 styles)
.content-dividerLigne séparatrice fine
.includes avec ::before rondListe avec puces dorées custom
.programme (timeline)Étapes avec icônes, ligne verticale
:not(:last-child)::afterLigne entre les étapes
.opt-tagTag "optionnel" inline
overflow-y: autoScroll interne si contenu long
@media 900pxBreakpoint tablette en plus








Éléments NOUVEAUX dans page4.html (Contact) 🆕

1 — UP-text simple (sans image ni dégradé)
Page 4 n'utilise ni image ni dégradé pour le hero. Juste un <div> simple sur fond blanc :
html<div class="page-title">
    <h1>📞 Contactez-nous</h1>
    <div class="gold-line"></div>
    <p>Nous sommes à votre disposition...</p>
</div>
.page-title {
    text-align: center;
    padding: 140px 20px 50px;
}
 padding-top: 140px = espace pour ne pas être caché par le header fixe. Très simple comparé aux pages précédentes.

2 — Les cartes Contact .contact-card
.contact-card {
    background: #fff;
    border: 1px solid #e8e0d0;
    border-left: 5px solid var(--gold);
    border-radius: 0 8px 8px 0;
    padding: 32px 36px;
    box-shadow: 0 4px 20px rgba(0,0,0,0.06);
    transition: box-shadow 0.3s ease;
}
 Nouveautés par rapport aux pages précédentes :
PropriétéCe qu'elle faitborder-left: 5px solid var(--gold)Barre dorée à gauche (pas en haut comme avant)border-radius: 0 8px 8px 0Coins arrondis à droite seulement (0 à gauche car la barre est là)
Pages 1/2/3 avaient border-top (barre en haut). Page 4 a border-left (barre à gauche). ✅
Le .card-header
.contact-card .card-header {
    display: flex;
    align-items: center;
    gap: 14px;
    margin-bottom: 8px;
}
<div class="card-header">
    <span class="icon">💬</span>
    <h2>WhatsApp</h2>
</div>
 Icône emoji + titre côte à côte avec flex et gap. Simple et nouveau.

3 — Les boutons WhatsApp .wa-btn
.wa-btn {
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 13px 18px;
    background: #f5f0e8;
    border: 1px solid #e0d5c0;
    border-radius: 8px;
    text-decoration: none;
    color: var(--dark);
    transition: background 0.2s, border-color 0.2s;
}

.wa-btn:hover {
    background: var(--gold);
    border-color: var(--gold);
    color: #fff;
}
<a class="wa-btn" href="https://wa.me/212601629828" target="_blank">
    <span class="wa-icon">📱</span>
    <span class="wa-num">+212 601 629 828</span>
</a>
 Plusieurs nouveautés ici :
href="https://wa.me/212..." = lien WhatsApp direct. Quand on clique → ouvre WhatsApp avec ce numéro.
target="_blank" = ouvre dans un nouvel onglet. Sans ça, la page actuelle serait remplacée.
border-radius: 8px = coins arrondis sur tous les côtés (nouveau style arrondi).
Au survol → fond devient doré, texte blanc. Deux propriétés changent en même temps.

4 — Le bouton Instagram .insta-btn
.insta-btn {
    display: inline-flex;
    align-items: center;
    gap: 10px;
    padding: 13px 22px;
    background: linear-gradient(135deg, #833ab4, #fd1d1d, #fcb045);
    color: #fff;
    border-radius: 8px;
    text-decoration: none;
    transition: opacity 0.2s;
}

.insta-btn:hover { opacity: 0.88; }
<a class="insta-btn" href="https://instagram.com/tripswith_sara" target="_blank">
    <span class="insta-icon">📸</span>
    @tripswith_sara
</a>
 Nouveautés :
display: inline-flex = comme flex mais le bouton prend seulement la largeur de son contenu (pas toute la ligne). flex seul = prend toute la largeur.
linear-gradient(135deg, #833ab4, #fd1d1d, #fcb045) = dégradé 3 couleurs (violet → rouge → orange) = couleurs officielles d'Instagram 🎨
.insta-btn:hover { opacity: 0.88; } = au survol, le bouton devient légèrement transparent (88%). Plus simple que changer les couleurs.

5 — .contact-note (texte italique)
css.contact-note {
    font-size: 0.82rem;
    color: #999;
    font-style: italic;
}
<p class="contact-note">👉 Cliquez et envoyez-nous un message...</p>
 font-style: italic = texte en italique. Pas utilisé dans les pages précédentes.

 6 — .contact-wrapper avec gap
.contact-wrapper {
    max-width: 700px;
    margin: 0 auto;
    padding: 10px 30px 80px;
    display: flex;
    flex-direction: column;
    gap: 28px;
}
 Le conteneur des cartes utilise flex-direction: column + gap: 28px = les cartes sont empilées avec un espace de 28px entre elles. Simple et efficace.

 7 — Nom de classe différent : .barrenav
.barrenav{ display: none; ... }
 Pages 1/2/3 appelaient ça .barrenav. Page 4 l'appelle .barrenav. Même chose, nom différent. Ça montre que les deux noms fonctionnent — ce qui compte c'est que le CSS et le HTML utilisent le même nom.

 Résumé — Ce qui est nouveau
ÉlémentNouveauté<div> au lieu de <section> UP simple sans fond spécial
border-left au lieu de border-topBarre dorée à gauche des cartes
border-radius: 0 8px 8px 0Coins arrondis à droite seulement
href="https://wa.me/..."Lien WhatsApp direct
target="_blank"Ouvre dans nouvel onglet
display: inline-flexFlex mais largeur = contenu seulement
Dégradé 3 couleurs Instagramlinear-gradient avec 3 couleurs
opacity au hoverTransparence au survol (au lieu de changer couleur)
font-style: italicTexte en italique
.UP Même chose que .barrenav mais nom différent







Éléments NOUVEAUX dans page5.html (Avis) 

1 — Reset global avec ::before et ::after
*, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }
 Pages précédentes avaient juste *. Ici on ajoute *::before, *::after = les pseudo-éléments aussi sont resetés. Plus complet.

 2 — Nouvelle variable CSS --muted
:root {
    --muted: #9a9489;
}
 Couleur grise utilisée pour les textes secondaires (labels, dates...). Pas dans les pages précédentes.
overflow-x: hidden;
 Sur le body — empêche le scroll horizontal accidentel causé par les animations.

 3 — UP avec animations @keyframes fadeUp
C'est la grande nouveauté du UP !
@keyframes fadeUp {
    from { opacity: 0; transform: translateY(20px); }
    to   { opacity: 1; transform: translateY(0); }
}
Définit une animation : l'élément part de bas (décalé de 20px) et monte vers sa position normale en devenant visible.
.up-text-eyebrow {
    opacity: 0;
    animation: fadeUp 0.8s 0.2s forwards;
}
.up-text h1 {
    opacity: 0;
    animation: fadeUp 0.8s 0.4s forwards;
}
.up-text-sub {
    opacity: 0;
    animation: fadeUp 0.8s 0.6s forwards;
}
.PARAG {
    opacity: 0;
    animation: fadeUp 0.8s 0.8s forwards;
}
 Chaque élément démarre invisible (opacity: 0) et apparaît avec un délai différent :

0.2s → eyebrow en premier
0.4s → titre h1
0.6s → sous-titre
0.8s → ligne dorée en dernier

forwards = garde l'état final (reste visible après l'animation).
C'est ce qu'on appelle un effet cascade — les éléments apparaissent l'un après l'autre.
Les lignes décoratives .up-text-lines
css.up-text-lines {
    background-image: repeating-linear-gradient(
        90deg,
        rgba(201,168,76,0.04) 0px, rgba(201,168,76,0.04) 1px,
        transparent 1px, transparent 80px
    );
    pointer-events: none;
}
 repeating-linear-gradient = dégradé qui se répète automatiquement. Crée des lignes verticales fines et dorées en fond. pointer-events: none = ne bloque pas les clics de la souris.
Le halo .up-text-glow
.up-text-glow {
    position: absolute;
    width: 600px; height: 300px;
    background: radial-gradient(ellipse, rgba(201,168,76,0.07) 0%, transparent 70%);
    top: 50%; left: 50%;
    transform: translate(-50%, -50%);
}
 transform: translate(-50%, -50%) avec top: 50%; left: 50% = parfaitement centré (technique classique de centrage absolu).
Le mot doré dans le h1
<h1>Partagez votre <span>expérience</span></h1>
.up-text h1 span { color: var(--gold); font-style: italic; }
 Un seul mot est doré et italique dans le titre. Effet typographique élégant.

 4 — Layout 2 colonnes asymétriques
.main {
    display: grid;
    grid-template-columns: 1fr 1.5fr;
    gap: 80px;
}
 1fr 1.5fr = colonnes inégales — la droite est 1.5x plus large que la gauche. Pages 2 et 3 utilisaient 1fr 1fr (égales).

 5 — Le formulaire (complètement nouveau)
Les inputs stylisés
.form-group input,
.form-group select,
.form-group textarea {
    border: 1px solid #e0d8cc;
    border-bottom: 2px solid #e0d8cc;
    outline: none;
    transition: border-color 0.25s;
    appearance: none;
    border-radius: 0;
}
.form-group input:focus,
.form-group select:focus {
    border-bottom-color: var(--gold);
}
 Plusieurs nouveautés :

appearance: none = supprime le style par défaut du navigateur sur les select/input
border-radius: 0 = angles droits (pas arrondis)
outline: none = supprime le contour bleu natif au focus
:focus = quand on clique dedans → la bordure du bas devient dorée
border-bottom: 2px = la bordure du bas est plus épaisse (style moderne)

Le <select> avec flèche custom
css.select-wrap { position: relative; }
.select-wrap::after {
    content: '›';
    position: absolute;
    right: 14px; top: 50%;
    transform: translateY(-50%) rotate(90deg);
    color: var(--gold);
    pointer-events: none;
}
 appearance: none cache la flèche native du select. ::after crée une flèche dorée custom à la place. rotate(90deg) = tourne le › de 90° pour faire une flèche vers le bas ↓.
Les étoiles interactives (CSS pur !)
.stars-input {
    display: flex;
    flex-direction: row-reverse;
    justify-content: flex-end;
}
.stars-input input { display: none; }
.stars-input label { font-size: 1.6rem; color: #ddd; cursor: pointer; }

.stars-input label:hover,
.stars-input label:hover ~ label,
.stars-input input:checked ~ label {
    color: var(--gold);
}
<div class="stars-input">
    <input type="radio" id="s5" name="stars" value="5">
    <label for="s5">★</label>
    <input type="radio" id="s4" name="stars" value="4">
    <label for="s4">★</label>
    ...
</div>

input radio caché (display: none)
row-reverse = les étoiles sont dans l'ordre inversé dans le HTML
label:hover ~ label = le sélecteur ~ = tous les frères suivants. Quand on survole une étoile → toutes les étoiles après (qui sont avant visuellement grâce au reverse) deviennent dorées
input:checked ~ label = même effet quand une étoile est sélectionnée

Le bouton submit
.btn-submit {
    background: var(--dark);
    border: 1px solid var(--gold);
    color: var(--gold);
    transition: background 0.3s, color 0.3s;
}
.btn-submit:hover { background: var(--gold); color: var(--dark); }
 Style inversé au hover : fond noir → fond doré, texte doré → texte noir.
Le message de succès
.success-msg {
    display: none;
    border-left: 3px solid var(--gold);
}
Caché par défaut (display: none). Le JavaScript l'affiche après soumission.

 6 — Les cartes d'avis
Animation slideIn
@keyframes slideIn {
    from { opacity: 0; transform: translateX(20px); }
    to   { opacity: 1; transform: translateX(0); }
}
.comment-card { animation: slideIn 0.4s ease forwards; }
 Chaque carte arrive de la droite en apparaissant. translateX = mouvement horizontal (différent de translateY qui est vertical).
Le grand guillemet décoratif
.c-quote {
    font-size: 5rem;
    color: rgba(201,168,76,0.1);
    position: absolute;
    top: 20px; right: 20px;
    user-select: none;
}
<div class="c-quote">"</div>
 Un " géant semi-transparent en fond de carte. user-select: none = ne peut pas être sélectionné avec la souris.
.c-dest (tag destination)
.c-dest {
    font-size: 0.62rem;
    color: var(--gold);
    border: 1px solid rgba(201,168,76,0.35);
    padding: 3px 10px;
}
Similaire au .opt-tag de page 3 mais pour afficher la destination de l'avis.

 7 — JavaScript 
localStorage — mémoire du navigateur
const STORAGE_KEY = 'tripswithsara_reviews';

function getReviews() {
    try { return JSON.parse(localStorage.getItem(STORAGE_KEY)) || []; }
    catch(e) { return []; }
}

function saveReviews(reviews) {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(reviews));
}
localStorage = stockage permanent dans le navigateur. Les avis restent même après fermeture de la page. JSON.stringify = convertit un tableau JS en texte pour le stocker. JSON.parse = reconvertit le texte en tableau.
escapeHtml — sécurité
function escapeHtml(str) {
    return String(str)
        .replace(/&/g, '&amp;')
        .replace(/</g, '&lt;')
        .replace(/>/g, '&gt;')
        .replace(/"/g, '&quot;');
}
Sécurité importante ! Empêche les utilisateurs d'injecter du code HTML malveillant dans les avis. Ex: si quelqu'un écrit <script>alert('hack')</script>, ça sera affiché comme texte normal.
formatDate
function formatDate(ts) {
    const d = new Date(ts);
    return d.toLocaleDateString('fr-FR', { day: 'numeric', month: 'long', year: 'numeric' });
}
Date.now() = timestamp (nombre de millisecondes depuis 1970). toLocaleDateString('fr-FR') = formate en date française : "29 avril 2026".
renderCard — création dynamique
function renderCard(review) {
    const card = document.createElement('div');
    card.className = 'comment-card';
    card.innerHTML = `
        <div class="c-stars">${Array.from({length:5}, (_,i) =>
            `<span style="color:${i < review.stars ? 'var(--gold)' : '#ddd'}">★</span>`
        ).join('')}</div>
        ...
    `;
    return card;
}
 innerHTML avec template literals (backticks `). Array.from({length:5}) = crée un tableau de 5 éléments pour générer les 5 étoiles. i < review.stars = les étoiles jusqu'au nombre choisi sont dorées, les autres grises.
submitReview — validation et sauvegarde
function submitReview() {
    const name = document.getElementById('f-name').value.trim();
    const starsEl = document.querySelector('input[name="stars"]:checked');

    if (!name || !text || !starsEl) {
        alert('Merci de remplir...');
        return;
    }

    const review = { name, country, dest, stars: parseInt(starsEl.value), text, ts: Date.now() };
    reviews.push(review);
    saveReviews(reviews);

    setTimeout(() => { msg.style.display = 'none'; }, 4000);
    renderAll();
}
.trim() = enlève les espaces au début et fin. if (!name || !text || !starsEl) = validation — si un champ obligatoire est vide → alerte et on arrête. setTimeout(..., 4000) = cache le message de succès après 4 secondes. renderAll() = recharge tous les avis.
updateCount — pluriel intelligent
function updateCount(n) {
    document.getElementById('commentsCount').textContent =
        n === 0 ? '0 témoignage' :
        n === 1 ? '1 témoignage' :
        `${n} témoignages`;
}
 Gère le pluriel : 0 témoignage / 1 témoignage / 2 témoignages. Utilise l'opérateur ternaire ? : enchaîné.

Résumé — Ce qui est nouveau
ÉlémentNouveauté*, *::before, *::afterReset plus complet
--mutedNouvelle variable CSS
overflow-x: hiddenEmpêche scroll horizontal
@keyframes fadeUpAnimation d'apparition en cascade
@keyframes slideInAnimation entrée depuis la droite
repeating-linear-gradientLignes décoratives répétées
translate(-50%, -50%)Centrage absolu parfait
1fr 1.5frColonnes grille inégales
Formulaire completinputs, select, textarea, radio stars
appearance: noneSupprime style natif navigateur
::after flèche selectFlèche custom sur le select
Étoiles CSS purrow-reverse + sélecteur ~
user-select: noneEmpêche sélection texte
localStorageDonnées persistantes dans le navigateur
escapeHtmlSécurité anti-injection HTML
Date.now() + formatDateTimestamp et formatage date
Array.from + template literalsGénération dynamique des étoiles
.trim()Nettoyer les espaces
setTimeoutMasquer message après délai
Opérateur ternaire ? :Pluriel intelligent
