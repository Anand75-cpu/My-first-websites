# My-first-websites

<!DOCTYPE html>
<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Rishi E-Store | Online Shopping</title>

<style>
* { box-sizing: border-box; }
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #f5f6fa;
  color: #222;
}
header {
  background: #211b45;
  color: white;
  padding: 20px;
  text-align: center;
}
header h1 { margin: 0; font-size: 27px; }
header p { margin-bottom: 0; color: #ddd; }

.search {
  display: block;
  width: 90%;
  max-width: 550px;
  margin: 18px auto;
  padding: 14px;
  border: 1px solid #ddd;
  border-radius: 12px;
  font-size: 16px;
}
.categories {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 8px;
  padding: 5px 12px 18px;
}
.categories button {
  border: 0;
  padding: 10px 15px;
  border-radius: 20px;
  background: #e5e2f4;
  color: #211b45;
}
.categories button.active {
  background: #211b45;
  color: white;
}
h2 { text-align: center; }

.products {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 14px;
  padding: 12px;
  max-width: 900px;
  margin: auto;
}
.product {
  background: white;
  border-radius: 14px;
  padding: 12px;
  text-align: center;
  box-shadow: 0 2px 10px #00000012;
}
.photo {
  background: #eeeafa;
  border-radius: 12px;
  font-size: 55px;
  padding: 20px 5px;
}
.product h3 { font-size: 16px; }
.price {
  color: #16834a;
  font-weight: bold;
  font-size: 19px;
}
.product button, .checkout {
  background: #211b45;
  color: white;
  border: none;
  border-radius: 9px;
  padding: 11px;
  width: 100%;
  font-size: 14px;
}
.cart {
  background: white;
  margin: 20px 12px;
  padding: 18px;
  border-radius: 14px;
}
.cart p { border-bottom: 1px solid #eee; padding: 8px 0; }
footer {
  background: #211b45;
  color: white;
  padding: 20px;
  text-align: center;
  margin-top: 25px;
}
@media (min-width: 650px) {
  .products { grid-template-columns: repeat(3, 1fr); }
}
</style>
</head>

<body>

<header>
  <h1>🛍️ Rishi E-Store</h1>
  <p>आपकी पसंद, हमारी जिम्मेदारी!</p>
</header>

<input
  class="search"
  id="search"
  placeholder="🔍 Product खोजें..."
  oninput="showProducts()"
>

<div class="categories">
  <button class="active" onclick="filter('All',this)">All</button>
  <button onclick="filter('Electronics',this)">Electronics</button>
  <button onclick="filter('Fashion',this)">Fashion</button>
  <button onclick="filter('Home',this)">Home</button>
  <button onclick="filter('Beauty',this)">Beauty</button>
</div>

<h2>🔥 हमारे Products</h2>
<div class="products" id="products"></div>

<div class="cart">
  <h2>🛒 My Cart (<span id="count">0</span>)</h2>
  <div id="cartItems">अभी Cart खाली है।</div>
  <h3>कुल कीमत: ₹<span id="total">0</span></h3>
  <button class="checkout" onclick="checkout()">
    WhatsApp से Order करें
  </button>
</div>

<footer>
  <h3>Rishi E-Store</h3>
  <p>Thank you for shopping with us ❤️</p>
  <p>© 2026 Rishi E-Store</p>
</footer>

<script>
const products = [
 {id:1,name:"Wireless Earbuds",price:599,cat:"Electronics",emoji:"🎧"},
 {id:2,name:"Smart Watch",price:999,cat:"Electronics",emoji:"⌚"},
 {id:3,name:"Bluetooth Speaker",price:799,cat:"Electronics",emoji:"🔊"},
 {id:4,name:"Stylish T-Shirt",price:399,cat:"Fashion",emoji:"👕"},
 {id:5,name:"Home Lamp",price:499,cat:"Home",emoji:"💡"},
 {id:6,name:"Beauty Kit",price:699,cat:"Beauty",emoji:"💄"}
];

let selected = "All";
let cart = [];

function showProducts() {
 const search = document.getElementById("search").value.toLowerCase();
 const list = products.filter(p =>
  (selected === "All" || p.cat === selected) &&
  p.name.toLowerCase().includes(search)
 );

 document.getElementById("products").innerHTML =
 list.length ? list.map(p => `
  <div class="product">
   <div class="photo">${p.emoji}</div>
   <h3>${p.name}</h3>
   <p class="price">₹${p.price}</p>
   <button onclick="addCart(${p.id})">Add to Cart</button>
  </div>
 `).join("") : "<p>कोई Product नहीं मिला।</p>";
}

function filter(category,btn) {
 selected = category;
 document.querySelectorAll(".categories button")
 .forEach(b => b.classList.remove("active"));
 btn.classList.add("active");
 showProducts();
}

function addCart(id) {
 cart.push(products.find(p => p.id === id));
 updateCart();
}

function updateCart() {
 document.getElementById("count").innerText = cart.length;
 document.getElementById("total").innerText =
 cart.reduce((sum,p) => sum + p.price,0);

 document.getElementById("cartItems").innerHTML =
 cart.length ? cart.map((p,i) =>
 `<p>${p.emoji} ${p.name} - ₹${p.price}
 <button onclick="removeCart(${i})">Remove</button></p>`
 ).join("") : "अभी Cart खाली है।";
}

function removeCart(i) {
 cart.splice(i,1);
 updateCart();
}

function checkout() {
 if (!cart.length) {
  alert("पहले कोई Product Cart में जोड़ें।");
  return;
 }
 alert("अगले स्टेप में हम तुम्हारा WhatsApp नंबर जोड़कर Order सिस्टम चालू करेंगे।");
}

showProducts();
</script>

</body>
</html>

