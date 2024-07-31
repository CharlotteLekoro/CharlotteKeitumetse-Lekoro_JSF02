<script>
  import { onMount } from 'svelte';
  let products = [];

  onMount(async () => {
    const response = await fetch('https://fakestoreapi.com/products');
    const data = await response.json();
    products = data;
  });

  function navigateToImagePage(product) {
    // Navigate to the image page with the product details
    window.location.href = `/image/${product.id}`;
  }

</script>
<nav class="navbar">
  <div class="logo">
    <img src="logo.png" alt="Trendy Treasures Logo" />
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
<div class="card-container">
  {#each products as product}
    <div class="card">
      <img src={product.image} alt={product.title} />
      <h2>{product.title}</h2>
      <p>Price: ${product.price}</p>
      <p>{product.category}</p>
    </div>
  {/each}
</div>
<div class="card-container">
  {#each products as product}
    <div class="card" on:click={() => navigateToImagePage(product)}>
      <img src={product.image} alt={product.title} />
      <h2>{product.title}</h2>
      <p>{product.description}</p>
      <p>Price: ${product.price}</p>
    </div>
  {/each}
</div>
<!--<div class="image-page">
  <img src={product.image} alt={product.title} />
  <h2>{product.title}</h2>
  <p>Price: ${product.price}</p>
</div>-->

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

