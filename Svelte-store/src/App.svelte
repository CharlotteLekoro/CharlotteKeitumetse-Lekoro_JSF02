/**
 * Import onMount from Svelte
 */
<script>
  import { onMount } from 'svelte';
  /**
 * Initialize variables
 */
  let products = [];
  let isLoading = true;
  let items = [];
  let filteredItems = [];
  let dropdownOpen = false;
  let activeSort = 'default'; 
  let activeCategory = ''; 
/**
 * On mount, fetch products from API and set up initial state
 */
  onMount(async () => {
    const response = await fetch('https://fakestoreapi.com/products');
    const data = await response.json();
    products = data;
    isLoading = false;
    items = data;
    filteredItems = [...items]; // Display all items initially
  });
/**
 * Sort items based on option and sortBy
 * @param {string} option - sorting option (default, category, price)
 * @param {string} sortBy - category or price sorting option
 */
  function sortItems(option, sortBy) {
    if (option === 'default') {
      filteredItems = [...items];
    } else if (option === 'category') {
      filteredItems = items.filter(item => item.category.toLowerCase() === sortBy.toLowerCase());
    } else if (option === 'price') {
      if (sortBy === 'highToLow') {
        filteredItems = [...items].sort((a, b) => b.price - a.price);
      } else if (sortBy === 'lowToHigh') {
        filteredItems = [...items].sort((a, b) => a.price - b.price);
      }
    }
    activeSort = option; // Update the active sort option
    activeCategory = sortBy; // Update the active category or price sorting
    dropdownOpen = false; // Close the dropdown after selection
  }
/**
 * Toggle dropdown open state
 */
  function toggleDropdown() {
    dropdownOpen = !dropdownOpen;
  }
</script>


<nav class="navbar">
  <div class="logo">
    <img src="./assets/" alt="Trendy Treasures Logo" />
    <span>Trendy Treasures</span>
  </div>
  <ul class="nav-links">
    <li><a href="#" class="nav-link">Add to Cart</a></li>
    <li><a href="#" class="nav-link">Wishlist</a></li>
  </ul>
</nav>

<div class="sort-dropdown">
  <button class={`sort-btn ${dropdownOpen ? 'active' : ''}`} on:click={toggleDropdown}>
    Sort By {activeSort === 'default' ? '🔽' : activeSort === 'price' ? (activeCategory === 'highToLow' ? '🔼' : '🔽') : activeCategory}
  </button>
  {#if dropdownOpen}
    <div class="sort-dropdown-content">
      <a href="#" class={activeSort === 'default' ? 'active' : ''} on:click={(e) => { e.preventDefault(); sortItems('default'); }}>Default</a>
      <a href="#" class={activeSort === 'category' && activeCategory === 'electronics' ? 'active' : ''} on:click={(e) => { e.preventDefault(); sortItems('category', 'electronics'); }}>Electronics</a>
      <a href="#" class={activeSort === 'category' && activeCategory === 'mens clothing' ? 'active' : ''} on:click={(e) => { e.preventDefault(); sortItems('category', 'mens clothing'); }}>Men's Clothing</a>
      <a href="#" class={activeSort === 'category' && activeCategory === 'womens clothing' ? 'active' : ''} on:click={(e) => { e.preventDefault(); sortItems('category', 'womens clothing'); }}>Women's Clothing</a>
      <a href="#" class={activeSort === 'category' && activeCategory === 'jewelery' ? 'active' : ''} on:click={(e) => { e.preventDefault(); sortItems('category', 'jewelery'); }}>Jewelery</a>
      <a href="#" class={activeSort === 'price' && activeCategory === 'highToLow' ? 'active' : ''} on:click={(e) => { e.preventDefault(); sortItems('price', 'highToLow'); }}>Price: High to Low</a>
      <a href="#" class={activeSort === 'price' && activeCategory === 'lowToHigh' ? 'active' : ''} on:click={(e) => { e.preventDefault(); sortItems('price', 'lowToHigh'); }}>Price: Low to High</a>
    </div>
  {/if}
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
   
   .body{
    background-color: #666;
   }

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

 /* CSS styles for the sort button and dropdown */

.sort-dropdown {
  position: relative;
  display: inline-block;
}

.sort-btn {
  background-color: #653b73;
  color: white;
  padding: 10px 20px;
  font-size: 16px;
  border: none;
  cursor: pointer;
  border-radius: 5px;
  transition: background-color 0.3s, box-shadow 0.3s;
  margin-top: 35px;
}

.sort-btn.active {
  background-color: #6845a0; /* Darker shade when active */
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.sort-dropdown-content {
  display: none;
  position: absolute;
  background-color: #f9f9f9;
  min-width: 160px;
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
  z-index: 1;
}

.sort-dropdown-content a {
  color: black;
  padding: 12px 16px;
  text-decoration: none;
  display: block;
}

.sort-dropdown-content a:hover {
  background-color: #f1f1f1;
}

.sort-dropdown-content a.active {
  background-color: #ddd; /* Highlight active option */
  font-weight: bold;
}

.sort-dropdown:hover .sort-dropdown-content {
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

