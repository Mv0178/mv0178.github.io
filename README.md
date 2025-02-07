<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chocolats AJSPF M.VICQ + A.BRETON</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
        }
        header {
            background-color: #4CAF50;
            color: white;
            text-align: center;
            padding: 10px 0;
        }
        .container {
            width: 80%;
            margin: 0 auto;
        }
        .product {
            display: inline-block;
            width: 30%;
            margin: 10px;
            padding: 20px;
            border: 1px solid #ddd;
            border-radius: 8px;
            background-color: white;
            text-align: center;
        }
        .product img {
            width: 100%;
            border-radius: 8px;
        }
        .product h3 {
            color: #333;
        }
        .product p {
            font-size: 14px;
            color: #777;
        }
        .btn {
            background-color: #4CAF50;
            color: white;
            padding: 10px;
            border: none;
            cursor: pointer;
            border-radius: 5px;
            text-align: center;
        }
        .btn:hover {
            background-color: #45a049;
        }
        .cart {
            margin-top: 20px;
            padding: 20px;
            background-color: white;
            border-radius: 8px;
            border: 1px solid #ddd;
        }
        .cart h2 {
            text-align: center;
        }
        .cart-items {
            margin-top: 20px;
            list-style: none;
            padding: 0;
        }
        .cart-items li {
            padding: 10px;
            border-bottom: 1px solid #ddd;
        }
        .total {
            font-size: 20px;
            text-align: center;
            margin-top: 10px;
        }
    </style>
</head>
<body>

    <header>
        <h1>Bienvenue sur Chocolats AJSPF M.VICQ + A.BRETON</h1>
    </header>

    <div class="container">
        <h2>Nos Produits de Saison</h2>

        <!-- Liste de 56 articles -->
        <div id="products-container">
            <!-- Chaque produit est une div avec une image, un titre, une description, et un bouton d'ajout au panier -->
        </div>

        <div class="cart">
            <h2>Panier</h2>
            <ul class="cart-items" id="cart-items">
                <!-- Les articles du panier s'afficheront ici -->
            </ul>
            <div class="total">
                Total: <span id="total">0€</span>
            </div>
        </div>
    </div>

    <script>
        // Liste des produits
        const produits = [
            { nom: "Chocolat de Noël 1", prix: 15 },
            { nom: "Chocolat de Noël 2", prix: 18 },
            { nom: "Chocolat de Noël 3", prix: 16 },
            { nom: "Chocolat de Pâques 1", prix: 12 },
            { nom: "Chocolat de Pâques 2", prix: 14 },
            { nom: "Chocolat de Pâques 3", prix: 13 },
            { nom: "Chocolat de Saint-Valentin 1", prix: 20 },
            { nom: "Chocolat de Saint-Valentin 2", prix: 22 },
            { nom: "Chocolat de Saint-Valentin 3", prix: 21 },
            { nom: "Chocolat de Noël 4", prix: 17 },
            { nom: "Chocolat de Noël 5", prix: 19 },
            { nom: "Chocolat de Noël 6", prix: 15 },
            { nom: "Chocolat de Pâques 4", prix: 12 },
            { nom: "Chocolat de Pâques 5", prix: 13 },
            { nom: "Chocolat de Pâques 6", prix: 14 },
            { nom: "Chocolat de Saint-Valentin 4", prix: 20 },
            { nom: "Chocolat de Saint-Valentin 5", prix: 19 },
            { nom: "Chocolat de Saint-Valentin 6", prix: 18 },
            { nom: "Chocolat de Noël 7", prix: 17 },
            { nom: "Chocolat de Noël 8", prix: 16 },
            { nom: "Chocolat de Noël 9", prix: 14 },
            { nom: "Chocolat de Pâques 7", prix: 11 },
            { nom: "Chocolat de Pâques 8", prix: 13 },
            { nom: "Chocolat de Pâques 9", prix: 12 },
            { nom: "Chocolat de Saint-Valentin 7", prix: 21 },
            { nom: "Chocolat de Saint-Valentin 8", prix: 22 },
            { nom: "Chocolat de Saint-Valentin 9", prix: 23 },
            { nom: "Chocolat de Noël 10", prix: 18 },
            { nom: "Chocolat de Noël 11", prix: 17 },
            { nom: "Chocolat de Noël 12", prix: 19 },
            { nom: "Chocolat de Pâques 10", prix: 12 },
            { nom: "Chocolat de Pâques 11", prix: 14 },
            { nom: "Chocolat de Pâques 12", prix: 13 },
            { nom: "Chocolat de Saint-Valentin 10", prix: 25 },
            { nom: "Chocolat de Saint-Valentin 11", prix: 24 },
            { nom: "Chocolat de Saint-Valentin 12", prix: 26 },
            { nom: "Chocolat de Noël 13", prix: 15 },
            { nom: "Chocolat de Noël 14", prix: 16 },
            { nom: "Chocolat de Noël 15", prix: 18 },
            { nom: "Chocolat de Pâques 13", prix: 11 },
            { nom: "Chocolat de Pâques 14", prix: 12 },
            { nom: "Chocolat de Pâques 15", prix: 14 },
            { nom: "Chocolat de Saint-Valentin 13", prix: 22 },
            { nom: "Chocolat de Saint-Valentin 14", prix: 21 },
            { nom: "Chocolat de Saint-Valentin 15", prix: 23 },
            { nom: "Chocolat de Noël 16", prix: 20 },
            { nom: "Chocolat de Noël 17", prix: 21 },
            { nom: "Chocolat de Noël 18", prix: 22 },
            { nom: "Chocolat de Pâques 16", prix: 13 },
            { nom: "Chocolat de Pâques 17", prix: 12 },
            { nom: "Chocolat de Pâques 18", prix: 14 },
            { nom: "Chocolat de Saint-Valentin 16", prix: 20 },
            { nom: "Chocolat de Saint-Valentin 17", prix: 22 },
            { nom: "Chocolat de Saint-Valentin 18", prix: 21 },
        ];

        // Initialisation du panier
        let panier = [];
        let total = 0;

        // Afficher les produits sur la page
        function afficherProduits() {
            let productsContainer = document.getElementById('products-container');
            produits.forEach((produit, index) => {
                let productDiv = document.createElement('div');
                productDiv.className = 'product';

                productDiv.innerHTML = `
                    <img src="https://via.placeholder.com/300x200?text=${produit.nom}" alt="${produit.nom}">
                    <h3>${produit.nom}</h3>
                    <p>Prix: ${produit.prix}€</p>
                    <button class="btn" onclick="ajouterAuPanier('${produit.nom}', ${produit.prix})">Ajouter au panier</button>
                `;
                productsContainer.appendChild(productDiv);
            });
        }

        // Fonction pour ajouter un produit au panier
        function ajouterAuPanier(nom, prix) {
            panier.push({ nom: nom, prix: prix });
            total += prix;
            afficherPanier();
        }

        // Fonction pour afficher les produits du panier
        function afficherPanier() {
            let cartItems = document.getElementById('cart-items');
            let totalElement = document.getElementById('total');
            cartItems.innerHTML = ''; // Vide le panier avant de le mettre à jour

            // Ajoute les articles du panier à l'interface
            panier.forEach(item => {
                let li = document.createElement('li');
                li.textContent = `${item.nom} - ${item.prix}€`;
                cartItems.appendChild(li);
            });

            // Affiche le total
            totalElement.textContent = `${total}€`;
        }

        // Appeler la fonction pour afficher les produits
        afficherProduits();
    </script>

</body>
</html>

