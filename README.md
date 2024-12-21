<!DOCTYPE html>
<html lang="en" data-theme="dark">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Shopify-Powered GitHub Page</title>

  <!-- Tailwind CSS and DaisyUI -->
  <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
  <link href="https://cdn.jsdelivr.net/npm/daisyui@2.14.3/dist/full.css" rel="stylesheet">

  <!-- Font Awesome -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.1.1/css/all.min.css">

  <!-- GSAP -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.10.4/gsap.min.js"></script>

  <!-- ScrollReveal -->
  <script src="https://cdn.jsdelivr.net/npm/scrollreveal@4.0.9/dist/scrollreveal.min.js"></script>

  <!-- Swiper -->
  <link rel="stylesheet" href="https://unpkg.com/swiper/swiper-bundle.min.css" />
  <script src="https://unpkg.com/swiper/swiper-bundle.min.js"></script>

  <!-- Firebase -->
  <script src="https://www.gstatic.com/firebasejs/8.6.8/firebase-app.js"></script>
  <script src="https://www.gstatic.com/firebasejs/8.6.8/firebase-firestore.js"></script>

  <style>
    body {
      background-color: #121212;
      color: #eaeaea;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }

    .hero {
       background-image: linear-gradient(135deg, #121212 50%, #ff6b6b 100%);
      position: relative;
      overflow: hidden;
    }

    .hero-content {
      z-index: 10;
      position: relative;
    }

    .particle {
      position: absolute;
      border-radius: 50%;
      opacity: 0.4;
      animation: float 6s linear infinite;
    }

    @keyframes float {
      0% {
        transform: translateY(0);
      }
      50% {
        transform: translateY(-20px);
      }
      100% {
        transform: translateY(0);
      }
    }

    #particle-1 {
      width: 80px;
      height: 80px;
      background-image: linear-gradient(135deg, #6b73ff 0%, #000dff 100%);
      top: 10%;
      left: 10%;
    }

    #particle-2 {
      width: 50px;
      height: 50px;
      background-image: linear-gradient(135deg, #ff6b6b 0%, #ff0000 100%);
      bottom: 20%;
      right: 15%;
    }

    .swiper-container {
      width: 100%;
      height: 500px;
    }

    .swiper-slide {
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 22px;
      background: #181818;
      color: #fff;
      border-radius: 12px;
      position: relative;
      overflow: hidden;
    }

    .swiper-slide img {
      display: block;
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

    .swiper-slide-content {
      position: absolute;
      bottom: 0;
      left: 0;
      width: 100%;
      padding: 20px;
      background-color: rgba(0, 0, 0, 0.6);
      color: #fff;
      text-align: left;
      transform: translateY(100%);
      transition: transform 0.4s ease-in-out;
    }

    .swiper-slide-content h4 {
      font-size: 24px;
      margin-bottom: 10px;
    }

    .swiper-slide:hover .swiper-slide-content {
      transform: translateY(0);
    }

    #shopify-section {
      position: relative;
      background-color: #181818;
      padding: 50px 0;
    }

    .shopify-section-bg {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-image: url(./background.jpg);
      background-size: cover;
      background-position: center;
      filter: blur(10px) brightness(50%);
      z-index: 1;
    }

    .shopify-section-title {
      text-align: center;
      font-size: 36px;
      color: #fff;
      margin-bottom: 30px;
      z-index: 2;
      position: relative;
    }
  </style>
</head>
<body>
  <section class="hero min-h-screen py-20">
    <div id="particle-1" class="particle"></div>
    <div id="particle-2" class="particle"></div>

    <div class="hero-content text-center">
      <h1 class="text-6xl font-bold mb-6">Welcome to My Shopify Store</h1>
      <p class="text-2xl mb-10">Discover the latest and greatest products.</p>
      <a href="#shopify-section" class="btn btn-primary text-lg px-8 py-3 rounded-full hover:bg-purple-700 transition-colors">Shop Now</a>
    </div>
  </section>

  <section id="shopify-section">
    <div class="shopify-section-bg"></div>
    <h2 class="shopify-section-title">Featured Products</h2>
    <div class="container mx-auto">
      <div class="swiper-container">
        <div class="swiper-wrapper" id="product-list">
        </div>
      </div>
    </div>
  </section>

  <footer class="footer p-10 bg-base-200 text-base-content mt-12">
    <div>
      <span class="footer-title">Shopify Store</span>
      <a class="link link-hover">Branding</a>
      <a class="link link-hover">Design</a>
      <a class="link link-hover">Marketing</a>
      <a class="link link-hover">Advertisement</a>
    </div>
    <div>
      <span class="footer-title">GitHub</span>
      <a class="link link-hover">About us</a>
      <a class="link link-hover">Contact</a>
      <a class="link link-hover">Jobs</a>
      <a class="link link-hover">Press kit</a>
    </div>
    <div>
      <span class="footer-title">Legal</span>
      <a class="link link-hover">Terms of use</a>
      <a class="link link-hover">Privacy policy</a>
      <a class="link link-hover">Cookie policy</a>
    </div>
  </footer>

  <script>
  // Initialize Firebase
const firebaseConfig = {
  apiKey: "AIzaSyCu7R0Nxxxxxxxxxxxxxxxxxxxxxxxxxxx",
  authDomain: "your-project.firebaseapp.com",
  databaseURL: "https://your-project.firebaseio.com",
  projectId: "your-project",
  storageBucket: "your-project.appspot.com",
  messagingSenderId: "00000000000",
  appId: "1:000000000:web:xxxxxxxxxxxxxxxxxxx"
};

  firebase.initializeApp(firebaseConfig);
  const db = firebase.firestore();

  // Initialize Swiper
  var swiper = new Swiper('.swiper-container', {
    effect: 'coverflow',
    grabCursor: true,
    centeredSlides: true,
    slidesPerView: 'auto',
    coverflowEffect: {
      rotate: 50,
      stretch: 0,
      depth: 100,
      modifier: 1,
      slideShadows: true,
    },
    pagination: {
      el: '.swiper-pagination',
      clickable: true,
    },
    navigation: {
      nextEl: '.swiper-button-next',
      prevEl: '.swiper-button-prev',
    },
  });

  // Fetch products from Shopify via Firebase
  function fetchProducts() {
    db.collection('products').onSnapshot((snapshot) => {
      const products = snapshot.docs.map(doc => ({ id: doc.id, ...doc.data() }));
      updateProductList(products);
    });
  }

  // Update product list on the page
  function updateProductList(products) {
    const productList = document.getElementById('product-list');
    productList.innerHTML = '';

    products.forEach(product => {
      const slide = document.createElement('div');
      slide.classList.add('swiper-slide');
      slide.innerHTML = `
        <img src="${product.imageUrl}" alt="${product.name}">
        <div class="swiper-slide-content">
          <h4>${product.name}</h4>
          <p>${product.description}</p>
          <button class="btn btn-primary mt-4 buy-button" data-product-id="${product.id}">Buy Now</button>
        </div>
      `;
      productList.appendChild(slide);
    });

    swiper.update(); // Update Swiper after adding slides

    // Add event listeners to buy buttons
    const buyButtons = document.querySelectorAll('.buy-button');
    buyButtons.forEach(button => {
      button.addEventListener('click', () => {
        const productId = button.dataset.productId;
        window.location.href = `https://your-shopify-store.myshopify.com/cart/add?id=${productId}`;
      });
    });
  }

  // Initialize animations with GSAP and ScrollReveal
  function initAnimations() {
    gsap.from('.hero-content h1', { duration: 1, y: -50, opacity: 0, ease: 'power3.out' });
    gsap.from('.hero-content p', { duration: 1, y: -50, opacity: 0, delay: 0.5, ease: 'power3.out' });
    gsap.from('.hero-content .btn', { duration: 1, x: -50, opacity: 0, delay: 1, ease: 'power3.out' });

    ScrollReveal().reveal('.shopify-section-title', {
      duration: 1000,
      origin: 'top',
      distance: '50px',
      easing: 'ease-in-out',
      reset: true
    });

    ScrollReveal().reveal('.swiper-slide', {
      duration: 1000,
      origin: 'bottom',
      distance: '50px',
      easing: 'ease-in-out',
      reset: true,
      interval: 200
    });
  }

  // Call functions on window load
  window.addEventListener('load', () => {
    fetchProducts();
    initAnimations();
  });

  </script>
</body>
</html>
