<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Enhanced Ecommerce Website</title>
  <style>
    /* General Styles */
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    header {
      background-color: #333;
      padding: 10px;
    }

    header nav ul {
      list-style: none;
      display: flex;
      justify-content: space-around;
    }

    header nav ul li {
      display: inline;
    }

    header nav ul li a {
      color: white;
      text-decoration: none;
      padding: 10px;
    }

    .products {
      display: flex;
      justify-content: space-around;
      margin: 20px;
    }

    .product {
      border: 1px solid #ccc;
      padding: 20px;
      width: 30%;
      text-align: center;
    }

    .product img {
      width: 100%;
      height: auto;
    }

    .product button {
      background-color: #28a745;
      color: white;
      border: none;
      padding: 10px;
      cursor: pointer;
    }

    .cart-section {
      padding: 20px;
      margin-top: 40px;
      border-top: 1px solid #ccc;
    }

    .remove-btn {
      background-color: #dc3545;
      color: white;
      border: none;
      padding: 5px;
      cursor: pointer;
      margin-left: 10px;
    }

    footer {
      text-align: center;
      background-color: #333;
      color: white;
      padding: 10px;
    }

    /* Responsive Design */
    @media screen and (max-width: 768px) {
      .products {
        flex-direction: column;
        align-items: center;
      }

      .product {
        width: 80%;
        margin-bottom: 20px;
      }
    }
  </style>
</head>
<body>

  <header>
    <nav>
      <ul>
        <li><a href="#">Home</a></li>
        <li><a href="#">Shop</a></li>
        <li><a href="#">Cart <span id="cart-count">(0)</span></a></li>
      </ul>
    </nav>
  </header>

  <main>
    <section class="products">
      <div class="product">
        <img src="product1.jpg" alt="Product 1">
        <h3>Product 1</h3>
        <p>$10.00</p>
        <label for="quantity1">Quantity:</label>
        <input type="number" id="quantity1" min="1" value="1">
        <button onclick="addToCart('Product 1', 10, 'quantity1')">Add to Cart</button>
      </div>
      <div class="product">
        <img src="product2.jpg" alt="Product 2">
        <h3>Product 2</h3>
        <p>$20.00</p>
        <label for="quantity2">Quantity:</label>
        <input type="number" id="quantity2" min="1" value="1">
        <button onclick="addToCart('Product 2', 20, 'quantity2')">Add to Cart</button>
      </div>
      <div class="product">
        <img src="product3.jpg" alt="Product 3">
        <h3>Product 3</h3>
        <p>$30.00</p>
        <label for="quantity3">Quantity:</label>
        <input type="number" id="quantity3" min="1" value="1">
        <button onclick="addToCart('Product 3', 30, 'quantity3')">Add to Cart</button>
      </div>
    </section>

    <section id="cart" class="cart-section">
      <h2>Your Cart</h2>
      <ul id="cart-items"></ul>
      <p>Total: $<span id="cart-total">0</span></p>
    </section>
  </main>

  <footer>
    <p>&copy; 2025 Enhanced Ecommerce</p>
  </footer>

  <script>
    let cart = JSON.parse(localStorage.getItem("cart")) || [];
    let cartCount = cart.length;

    function addToCart(productName, price, quantityId) {
      const quantity = document.getElementById(quantityId).value;
      for (let i = 0; i < quantity; i++) {
        cart.push({ name: productName, price: price });
      }
      cartCount += Number(quantity);
      
      localStorage.setItem("cart", JSON.stringify(cart));
      updateCart();
    }

    function updateCart() {
      const cartItemsContainer = document.getElementById("cart-items");
      cartItemsContainer.innerHTML = "";
      
      let total = 0;
      cart.forEach((item, index) => {
        const li = document.createElement("li");
        li.textContent = `${item.name} - $${item.price}`;
        
        const removeBtn = document.createElement("button");
        removeBtn.textContent = "Remove";
        removeBtn.classList.add("remove-btn");
        removeBtn.onclick = () => removeFromCart(index);
        
        li.appendChild(removeBtn);
        cartItemsContainer.appendChild(li);
        total += item.price;
      });

      document.getElementById("cart-total").textContent = total.toFixed(2);
      document.getElementById("cart-count").textContent = `(${cart.length})`;
    }

    function removeFromCart(index) {
      cart.splice(index, 1);
      localStorage.setItem("cart", JSON.stringify(cart));
      updateCart();
    }

    updateCart();
  </script>

</body>
</html>

