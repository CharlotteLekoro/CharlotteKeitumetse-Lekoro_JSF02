<script>
  import { onMount } from 'svelte';
  let products = [];
  let isLoading = true;
  let items = [];
  let filteredItems = [];

  onMount(async () => {
    const response = await fetch('https://fakestoreapi.com/products');
    const data = await response.json();
    products = data;
    isLoading = false;
    items = data;
    filteredItems = items; // Display all items initially
  });

  function sortItems(category) {
    filteredItems = items.filter(item => item.category.toLowerCase() === category);
  }

</script>
<nav class="navbar">
  <div class="logo">
    <img src="./assets/" alt="Trendy Treasures Logo" />
    <span>Trendy Treasures</span>
  </div>
  <ul class="nav-links">
    <li>
      <a href="#" class="nav-link">Add to Cart</a>
    </li>
    <li>
      <a href="#" class="nav-link">Wishlist</a>
    </li>
  </ul>
</nav>

<div class="dropdown">
  <button class="dropbtn">Sort by Category</button>
  <div class="dropdown-content">
    <a href="#" on:click={(e) => { e.preventDefault(); sortItems('electronics'); }}>Electronics</a>
    <a href="#" on:click={(e) => { e.preventDefault(); sortItems("men's clothing"); }}>Men's Clothing</a>
    <a href="#" on:click={(e) => { e.preventDefault(); sortItems("women's clothing"); }}>Women's Clothing</a>
    <a href="#" on:click={(e) => { e.preventDefault(); sortItems('jewelery'); }}>Jewelry</a>
  </div>
</div>

{#if isLoading}
  <div class="loading-state">
    <p>Loading...</p>
  </div>
{:else}
  <div class="card-container">
    {#each filteredItems as product}
      <div class="card">
        <img src={product.image} alt={product.title} />
        <h2>{product.title}</h2>
        <p>Price: ${product.price}</p>
        <p>{product.category}</p>
      </div>
    {/each}
  </div>
{/if}

<style>
  
 .navbar {
    position: fixed; 
    top: 0;
    left: 0;
    width: 100%; 
    height: 60px; 
    background-color: #653b73;
    color: #fff;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0 20px; /* add some padding for the logo and links */
  }

 .logo {
    display: flex;
    align-items: center;
  }

 .logo img {
    width: 30px;
    height: 30px;
    margin-right: 10px;
  }

 .nav-links {
    display: flex;
    list-style: none;
    margin: 20px;
    padding: 0;
  }

 .nav-link {
    color: #fff;
    text-decoration: none;
    margin-right: 20px;
    margin-left: 20px;
  }

 .nav-link:hover {
    color: #25a327;
  }

  .dropdown {
  position: relative;
  display: inline-block;
  margin: 20px;
  margin-top: 35px; /* Add top margin */
  margin-left: -auto; /* Align to the left side */
  left: 20px;
}

  .dropdown-content {
    display: none;
    position: absolute;
    background-color: #d9c8dc;
    min-width: 5%;
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
    z-index: 1;
  }

  .dropdown-content a {
    color: rgb(108, 77, 135);
    padding: 12px 16px;
    text-decoration: none;
    display: block;
  }

  .dropdown-content a:hover {
    background-color: #f1f1f1;
  }

  .dropdown:hover .dropdown-content {
    display: block;
  }

  .card-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }

  .card {
    margin: 20px;
    width: calc(25% - 20px);
    background-color: #fff;
    border: 1px solid #ddd;
    border-radius: 10px;
    padding: 20px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    cursor: pointer;
  }

  .card img {
    width: 100%;
    height: 100px;
    object-fit: contain;
    overflow: hidden;
    border-radius: 10px 10px 10px 010px;
  }

  .card h2 {
    font-size: 16px;
    margin-top: 10px;
  }

  .card p {
    font-size: 12px;
    font-weight:bold;
    color: #666;
  }

  .card:hover {
    box-shadow: 0 8px 16px rgba(84, 42, 121, 0.549);
}

body {
    background-color: #f8f8f8d1; /* Off-white background for the page */
    font-family: 'Lobster', cursive; /* Applying the fancy font to the body */
}

.image-page {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 20px;
  }

  .image-page img {
    width: 100%;
    height: 300px;
    object-fit: cover;
    border-radius: 10px;
  }
</style>

