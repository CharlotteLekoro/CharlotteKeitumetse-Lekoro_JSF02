// Navbar.svelte
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

<style>
 .navbar {
    position: fixed; /* fix the navbar to the top of the page */
    top: 0;
    left: 0;
    width: 100%; /* stretch across the whole page */
    height: 60px; /* adjust the height to your liking */
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
</style>