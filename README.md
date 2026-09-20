# my-web-site
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Alex & Alish Furniture Showroom</title>
  <style>
    :root {
      --primary: #2c3e50;
      --secondary: #1a252f;
      --accent: #27ae60;
      --btn-blue: #2980b9;
      --btn-hover: #3498db;
      --bg-light: #f4f4f9;
    }

    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background-color: var(--bg-light);
      color: #333;
    }

    .top-bar-container {
      background-color: var(--secondary);
      color: #ecf0f1;
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 0.5rem 2rem;
      font-size: 0.9rem;
      font-weight: bold;
      flex-wrap: wrap;
    }

    .cart-btn {
      background-color: var(--accent);
      color: white;
      border: none;
      padding: 0.4rem 1rem;
      border-radius: 4px;
      cursor: pointer;
      font-size: 0.9rem;
      font-weight: bold;
    }

    .cart-btn:hover {
      background-color: #219653;
    }

    header {
      background-color: var(--primary);
      color: #fff;
      text-align: center;
      padding: 2rem 1rem;
    }

    header h1 {
      margin: 0;
      font-size: 2.5rem;
    }

    header p {
      margin-top: 0.5rem;
      color: #ecf0f1;
    }

    .container {
      max-width: 1100px;
      margin: 2rem auto;
      padding: 0 1rem;
    }

    .product-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 2rem;
    }

    .product-card {
      background-color: #fff;
      border-radius: 8px;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
      overflow: hidden;
      display: flex;
      flex-direction: column;
    }

    .product-card img {
      width: 100%;
      height: 200px;
      object-fit: cover;
    }

    .product-details {
      padding: 1.5rem;
      display: flex;
      flex-direction: column;
      flex-grow: 1;
    }

    .product-title {
      font-size: 1.25rem;
      margin: 0 0 0.5rem 0;
    }

    .product-price {
      font-size: 1.1rem;
      font-weight: bold;
      color: var(--accent);
      margin-bottom: 1rem;
    }

    .buy-btn {
      margin-top: auto;
      background-color: var(--btn-blue);
      color: #fff;
      border: none;
      padding: 0.75rem;
      border-radius: 4px;
      cursor: pointer;
      font-size: 1rem;
      transition: background 0.2s;
    }

    .buy-btn:hover {
      background-color: var(--btn-hover);
    }

    /* Cart Modal / Sidebar */
    .cart-modal {
      display: none;
      position: fixed;
      top: 0;
      right: 0;
      width: 350px;
      height: 100%;
      background: white;
      box-shadow: -4px 0 10px rgba(0,0,0,0.2);
      z-index: 1000;
      padding: 1.5rem;
      box-sizing: border-box;
      flex-direction: column;
    }

    .cart-overlay {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0,0,0,0.5);
      z-index: 999;
    }

    .cart-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      border-bottom: 2px solid #eee;
      padding-bottom: 1rem;
    }

    .close-cart {
      background: none;
      border: none;
      font-size: 1.5rem;
      cursor: pointer;
    }

    .cart-items {
      flex-grow: 1;
      overflow-y: auto;
      margin: 1rem 0;
    }

    .cart-item {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 1rem;
      border-bottom: 1px solid #f0f0f0;
      padding-bottom: 0.5rem;
      font-size: 0.95rem;
    }

    .cart-item button {
      background: #e74c3c;
      color: white;
      border: none;
      padding: 0.25rem 0.5rem;
      border-radius: 3px;
      cursor: pointer;
    }

    .cart-total {
      font-size: 1.2rem;
      font-weight: bold;
      margin-bottom: 1rem;
      text-align: right;
    }

    .checkout-btn {
      background-color: var(--accent);
      color: white;
      border: none;
      padding: 0.75rem;
      font-size: 1rem;
      border-radius: 4px;
      cursor: pointer;
      width: 100%;
    }

    footer {
      text-align: center;
      padding: 1.5rem;
      background-color: var(--primary);
      color: #fff;
      margin-top: 3rem;
    }

    .hidden {
      display: none !important;
    }
  </style>
</head>
<body>

  <!-- Top Bar for Contact Info & Cart -->
  <div class="top-bar-container">
    <div>
      <span>Pro: Ram Karan Chaudhary</span> | 
      <span>📞 WhatsApp: 9841587624</span> | 
      <span>📞 Contact: 9716757776</span>
    </div>
    <div>
      <button class="cart-btn" onclick="toggleCart()">🛒 Cart (<span id="cart-count">0</span>)</button>
    </div>
  </div>

  <header>
    <h1>Alex & Alish Furniture Showroom</h1>
    <p>Quality furniture designed for comfort and modern homes.</p>
  </header>

  <div class="container">
    <div class="product-grid" id="product-grid">
      <!-- Products will be loaded dynamically via JavaScript -->
    </div>
  </div>

  <!-- Cart Drawer Overlay -->
  <div class="cart-overlay" id="cart-overlay" onclick="toggleCart()"></div>

  <!-- Cart Sidebar Drawer -->
  <div class="cart-modal hidden" id="cart-modal">
    <div class="cart-header">
      <h2>Your Shopping Cart</h2>
      <button class="close-cart" onclick="toggleCart()">&times;</button>
    </div>
    <div class="cart-items" id="cart-items-container">
      <p>Your cart is currently empty.</p>
    </div>
    <div class="cart-total">
      Total: Rs. <span id="cart-total-price">0</span>
    </div>
    <button class="checkout-btn" onclick="checkout()">Proceed to Checkout</button>
  </div>

  <footer>
    <p>&copy; 2026 Alex & Alish Furniture Showroom. All rights reserved.</p>
  </footer>

  <script>
    // Product Database (Expanded to 58 items)
    const products = [
      { id: 1, title: "Modern Minimalist Sofa", price: 65000, image: "https://images.unsplash.com/photo-1555041469-a586c61ea9bc?auto=format&fit=crop&w=600&q=80" },
      { id: 2, title: "Solid Oak Dining Table", price: 45000, image: "https://images.unsplash.com/photo-1530018607912-eff2daa1bac4?auto=format&fit=crop&w=600&q=80" },
      { id: 3, title: "Cozy Reading Armchair", price: 24000, image: "https://images.unsplash.com/photo-1580481072645-022f9a6d8310?auto=format&fit=crop&w=600&q=80" },
      { id: 4, title: "Queen Size Bed Frame", price: 68000, image: "https://images.unsplash.com/photo-1505693416388-ac5ce068fe85?auto=format&fit=crop&w=600&q=80" },
      { id: 5, title: "Rustic Wooden Coffee Table", price: 18500, image: "https://images.unsplash.com/photo-1532372320572-cda25653a26d?auto=format&fit=crop&w=600&q=80" },
      { id: 6, title: "5-Tier Industrial Bookshelf", price: 28000, image: "https://images.unsplash.com/photo-1595428774223-ef52624120d2?auto=format&fit=crop&w=600&q=80" },
      { id: 7, title: "Ergonomic Wooden Study Desk", price: 32000, image: "https://images.unsplash.com/photo-1518455027359-f3f8164ba6bd?auto=format&fit=crop&w=600&q=80" },
      { id: 8, title: "Scandinavian Accent Chair", price: 16000, image: "https://images.unsplash.com/photo-1598300042247-d088f8ab3a91?auto=format&fit=crop&w=600&q=80" },
      { id: 9, title: "Velvet Tufted Ottoman", price: 9500, image: "https://images.unsplash.com/photo-1586023492125-27b2c045efd7?auto=format&fit=crop&w=600&q=80" },
      { id: 10, title: "Glass Top Coffee Table", price: 21000, image: "https://images.unsplash.com/photo-1567016432779-094069958ea5?auto=format&fit=crop&w=600&q=80" },
      { id: 11, title: "Leather Recliner Chair", price: 42000, image: "https://images.unsplash.com/photo-1586023492125-27b2c045efd7?auto=format&fit=crop&w=600&q=80" },
      { id: 12, title: "King Size Luxury Bed", price: 85000, image: "https://images.unsplash.com/photo-1540518614846-7ede433c4ef0?auto=format&fit=crop&w=600&q=80" },
      { id: 13, title: "Minimalist Bedside Table", price: 7500, image: "https://images.unsplash.com/photo-1532372320572-cda25653a26d?auto=format&fit=crop&w=600&q=80" },
      { id: 14, title: "6-Seater Glass Dining Set", price: 72000, image: "https://images.unsplash.com/photo-1617806118233-18e1c0c1ae2d?auto=format&fit=crop&w=600&q=80" },
      { id: 15, title: "Upholstered Dining Chair", price: 6500, image: "https://images.unsplash.com/photo-1503602642458-232111445657?auto=format&fit=crop&w=600&q=80" },
      { id: 16, title: "Executive Office Desk", price: 48000, image: "https://images.unsplash.com/photo-1524758631624-e2822e304c36?auto=format&fit=crop&w=600&q=80" },
      { id: 17, title: "Mesh Ergonomic Office Chair", price: 18000, image: "https://images.unsplash.com/photo-1580481072645-022f9a6d8310?auto=format&fit=crop&w=600&q=80" },
      { id: 18, title: "Wooden TV Media Console", price: 34000, image: "https://images.unsplash.com/photo-1595428774223-ef52624120d2?auto=format&fit=crop&w=600&q=80" },
      { id: 19, title: "Floating Wall Shelf Unit", price: 5500, image: "https://images.unsplash.com/photo-1594552072238-b8a3da72ae8a?auto=format&fit=crop&w=600&q=80" },
      { id: 20, title: "L-Shaped Sectional Sofa", price: 95000, image: "https://images.unsplash.com/photo-1493663284031-b7e3aefcae8e?auto=format&fit=crop&w=600&q=80" },
      { id: 21, title: "Vintage Wooden Wardrobe", price: 78000, image: "https://images.unsplash.com/photo-1595515106967-1ce29566ff1c?auto=format&fit=crop&w=600&q=80" },
      { id: 22, title: "Modern Sliding Door Wardrobe", price: 89000, image: "https://images.unsplash.com/photo-1558997519-83ea9252dfac?auto=format&fit=crop&w=600&q=80" },
      { id: 23, title: "Dressing Table with Mirror", price: 29000, image: "https://images.unsplash.com/photo-1616046229478-9901c5536a45?auto=format&fit=crop&w=600&q=80" },
      { id: 24, title: "Padded Bedroom Bench", price: 12000, image: "https://images.unsplash.com/photo-1586023492125-27b2c045efd7?auto=format&fit=crop&w=600&q=80" },
      { id: 25, title: "Outdoor Rattan Patio Chair", price: 14000, image: "https://images.unsplash.com/photo-1519947486511-46149fa0a254?auto=format&fit=crop&w=600&q=80" },
      { id: 26, title: "Balcony Tea Table Set", price: 22000, image: "https://images.unsplash.com/photo-1533090161767-e6ffed986c88?auto=format&fit=crop&w=600&q=80" },
      { id: 27, title: "Children Bunk Bed", price: 55000, image: "https://images.unsplash.com/photo-1505693416388-ac5ce068fe85?auto=format&fit=crop&w=600&q=80" },
      { id: 28, title: "Kids Study Table & Chair Set", price: 15000, image: "https://images.unsplash.com/photo-1518455027359-f3f8164ba6bd?auto=format&fit=crop&w=600&q=80" },
      { id: 29, title: "Tall Metal Shoe Rack", price: 8500, image: "https://images.unsplash.com/photo-1595428774223-ef52624120d2?auto=format&fit=crop&w=600&q=80" },
      { id: 30, title: "Wooden Shoe Bench", price: 11000, image: "https://images.unsplash.com/photo-1532372320572-cda25653a26d?auto=format&fit=crop&w=600&q=80" },
      { id: 31, title: "Corner Display Cabinet", price: 31000, image: "https://images.unsplash.com/photo-1594552072238-b8a3da72ae8a?auto=format&fit=crop&w=600&q=80" },
      { id: 32, title: "Glass Crockery Unit", price: 46000, image: "https://images.unsplash.com/photo-1595515106967-1ce29566ff1c?auto=format&fit=crop&w=600&q=80" },
      { id: 33, title: "Nested Coffee Tables (Set of 2)", price: 16500, image: "https://images.unsplash.com/photo-1532372320572-cda25653a26d?auto=format&fit=crop&w=600&q=80" },
      { id: 34, title: "Foldable Laptop Table", price: 4500, image: "https://images.unsplash.com/photo-1518455027359-f3f8164ba6bd?auto=format&fit=crop&w=600&q=80" },
      { id: 35, title: "High Bar Stool", price: 7000, image: "https://images.unsplash.com/photo-1503602642458-232111445657?auto=format&fit=crop&w=600&q=80" },
      { id: 36, title: "Counter Height Dining Table", price: 38000, image: "https://images.unsplash.com/photo-1530018607912-eff2daa1bac4?auto=format&fit=crop&w=600&q=80" },
      { id: 37, title: "Velvet 3-Seater Sofa", price: 58000, image: "https://images.unsplash.com/photo-1555041469-a586c61ea9bc?auto=format&fit=crop&w=600&q=80" },
      { id: 38, title: "Chesterfield Leather Sofa", price: 82000, image: "https://images.unsplash.com/photo-1493663284031-b7e3aefcae8e?auto=format&fit=crop&w=600&q=80" },
      { id: 39, title: "Single Wooden Diwan Bed", price: 25000, image: "https://images.unsplash.com/photo-1505693416388-ac5ce068fe85?auto=format&fit=crop&w=600&q=80" },
      { id: 40, title: "Hydraulic Storage King Bed", price: 92000, image: "https://images.unsplash.com/photo-1540518614846-7ede433c4ef0?auto=format&fit=crop&w=600&q=80" },
      { id: 41, title: "Metal Wire Accent Chair", price: 13500, image: "https://images.unsplash.com/photo-1598300042247-d088f8ab3a91?auto=format&fit=crop&w=600&q=80" },
      { id: 42, title: "Boho Rattan Lounge Chair", price: 19000, image: "https://images.unsplash.com/photo-1580481072645-022f9a6d8310?auto=format&fit=crop&w=600&q=80" },
      { id: 43, title: "Industrial Style Bookshelf", price: 24000, image: "https://images.unsplash.com/photo-1595428774223-ef52624120d2?auto=format&fit=crop&w=600&q=80" },
      { id: 44, title: "Low Profile TV Unit", price: 21000, image: "https://images.unsplash.com/photo-1595428774223-ef52624120d2?auto=format&fit=crop&w=600&q=80" },
      { id: 45, title: "Wall-Mounted Computer Desk", price: 14500, image: "https://images.unsplash.com/photo-1518455027359-f3f8164ba6bd?auto=format&fit=crop&w=600&q=80" },
      { id: 46, title: "Conference Room Meeting Table", price: 110000, image: "https://images.unsplash.com/photo-1530018607912-eff2daa1bac4?auto=format&fit=crop&w=600&q=80" },
      { id: 47, title: "Visitor Office Chair", price: 9000, image: "https://images.unsplash.com/photo-1503602642458-232111445657?auto=format&fit=crop&w=600&q=80" },
      { id: 48, title: "Office Filing Cabinet", price: 26000, image: "https://images.unsplash.com/photo-1595515106967-1ce29566ff1c?auto=format&fit=crop&w=600&q=80" },
      { id: 49, title: "Round Marble Coffee Table", price: 29500, image: "https://images.unsplash.com/photo-1532372320572-cda25653a26d?auto=format&fit=crop&w=600&q=80" },
      { id: 50, title: "Solid Teak Wood Rocking Chair", price: 27000, image: "https://images.unsplash.com/photo-1580481072645-022f9a6d8310?auto=format&fit=crop&w=600&q=80" },
      { id: 51, title: "Upholstered Storage Ottoman", price: 13000, image: "https://images.unsplash.com/photo-1586023492125-27b2c045efd7?auto=format&fit=crop&w=600&q=80" },
      { id: 52, title: "Compact 4-Seater Dining Set", price: 35000, image: "https://images.unsplash.com/photo-1530018607912-eff2daa1bac4?auto=format&fit=crop&w=600&q=80" },
      { id: 53, title: "Marble Top Dining Table", price: 85000, image: "https://images.unsplash.com/photo-1617806118233-18e1c0c1ae2d?auto=format&fit=crop&w=600&q=80" },
      { id: 54, title: "Folding Garden Lounger", price: 16000, image: "https://images.unsplash.com/photo-1519947486511-46149fa0a254?auto=format&fit=crop&w=600&q=80" },
      { id: 55, title: "Wooden Room Divider Screen", price: 14000, image: "https://images.unsplash.com/photo-1594552072238-b8a3da72ae8a?auto=format&fit=crop&w=600&q=80" },
      { id: 56, title: "Multi-Purpose Utility Rack", price: 12500, image: "https://images.unsplash.com/photo-1595428774223-ef52624120d2?auto=format&fit=crop&w=600&q=80" },
      { id: 57, title: "Padded Vanity Stool", price: 5000, image: "https://images.unsplash.com/photo-1586023492125-27b2c045efd7?auto=format&fit=crop&w=600&q=80" },
      { id: 58, title: "Luxury Accent Bench", price: 17500, image: "https://images.unsplash.com/photo-1586023492125-27b2c045efd7?auto=format&fit=crop&w=600&q=80" }
    ];

    let cart = [];

    // Render Products on Page Load
    function renderProducts() {
      const grid = document.getElementById('product-grid');
      grid.innerHTML = products.map(product => `
        <div class="product-card">
          <img src="${product.image}" alt="${product.title}">
          <div class="product-details">
            <h2 class="product-title">${product.title}</h2>
            <div class="product-price">Rs. ${product.price.toLocaleString()}</div>
            <button class="buy-btn" onclick="addToCart(${product.id})">Add to Cart</button>
          </div>
        </div>
      `).join('');
    }

    // Add Item to Cart
    function addToCart(productId) {
      const product = products.find(p => p.id === productId);
      const existingItem = cart.find(item => item.id === productId);

      if (existingItem) {
        existingItem.quantity += 1;
      } else {
        cart.push({ ...product, quantity: 1 });
      }

      updateCartUI();
      alert(`${product.title} has been added to your cart!`);
    }

    // Remove Item from Cart
    function removeFromCart(productId) {
      cart = cart.filter(item => item.id !== productId);
      updateCartUI();
    }

    // Update Cart Counter, Items List, and Total Price
    function updateCartUI() {
      const cartCount = document.getElementById('cart-count');
      const cartItemsContainer = document.getElementById('cart-items-container');
      const cartTotalPrice = document.getElementById('cart-total-price');

      const totalCount = cart.reduce((sum, item) => sum + item.quantity, 0);
      cartCount.innerText = totalCount;

      if (cart.length === 0) {
        cartItemsContainer.innerHTML = '<p>Your cart is currently empty.</p>';
        cartTotalPrice.innerText = '0';
        return;
      }

      cartItemsContainer.innerHTML = cart.map(item => `
        <div class="cart-item">
          <div>
            <strong>${item.title}</strong><br>
            <small>Qty: ${item.quantity} x Rs. ${item.price.toLocaleString()}</small>
          </div>
          <button onclick="removeFromCart(${item.id})">X</button>
        </div>
      `).join('');

      const totalPrice = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
      cartTotalPrice.innerText = totalPrice.toLocaleString();
    }

    // Toggle Cart Drawer Visibility
    function toggleCart() {
      const modal = document.getElementById('cart-modal');
      const overlay = document.getElementById('cart-overlay');
      
      if (modal.classList.contains('hidden')) {
        modal.classList.remove('hidden');
        overlay.style.display = 'block';
      } else {
        modal.classList.add('hidden');
        overlay.style.display = 'none';
      }
    }

    // Checkout Simulation
    function checkout() {
      if (cart.length === 0) {
        alert("Your cart is empty!");
        return;
      }
      alert("Thank you for shopping with Alex & Alish Furniture Showroom! Order placed successfully. We will contact you via WhatsApp/Phone to confirm delivery.");
      cart = [];
      updateCartUI();
      toggleCart();
    }

    // Initialize the app
    renderProducts();
  </script>
</body>
</html>

























