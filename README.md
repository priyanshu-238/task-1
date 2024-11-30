<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Image Gallery</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background-color: #f0f0f5;
      text-align: center;
    }
    h1 {
      margin: 20px 0;
      color: #333;
    }
    .gallery {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 10px;
      padding: 20px;
    }
    .gallery img {
      width: 150px;
      height: 100px;
      object-fit: cover;
      border-radius: 5px;
      cursor: pointer;
      transition: transform 0.3s, box-shadow 0.3s;
    }
    .gallery img:hover {
      transform: scale(1.1);
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    }
    #lightbox {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.9);
      justify-content: center;
      align-items: center;
      flex-direction: column;
      z-index: 1000;
    }
    #lightbox img {
      max-width: 90%;
      max-height: 80%;
      border-radius: 10px;
    }
    #lightbox .controls {
      display: flex;
      justify-content: center;
      align-items: center;
      margin-top: 10px;
    }
    #lightbox .nav {
      color: white;
      font-size: 2rem;
      cursor: pointer;
      margin: 0 20px;
      user-select: none;
    }
    #lightbox .close {
      position: absolute;
      top: 20px;
      right: 30px;
      font-size: 2rem;
      color: white;
      cursor: pointer;
    }
    #lightbox .slideshow {
      color: white;
      font-size: 1.2rem;
      margin-top: 10px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <h1>Image Gallery</h1>
  <div class="gallery">
    <img src="https://via.placeholder.com/150x100" alt="Image 1">
    <img src="https://via.placeholder.com/150x100" alt="Image 2">
    <img src="https://via.placeholder.com/150x100" alt="Image 3">
    <img src="https://via.placeholder.com/150x100" alt="Image 4">
    <img src="https://via.placeholder.com/150x100" alt="Image 5">
    <img src="https://via.placeholder.com/150x100" alt="Image 6">
  </div>

  <div id="lightbox">
    <span class="close" onclick="closeLightbox()">&#10006;</span>
    <img src="" alt="Lightbox Image">
    <div class="controls">
      <span class="nav" onclick="prevImage()">&#10094;</span>
      <span class="nav" onclick="nextImage()">&#10095;</span>
    </div>
    <button class="slideshow" onclick="toggleSlideshow()">Start Slideshow</button>
  </div>

  <script>
    const images = document.querySelectorAll('.gallery img');
    const lightbox = document.getElementById('lightbox');
    const lightboxImg = lightbox.querySelector('img');
    let currentIndex = 0;
    let slideshowInterval = null;

    images.forEach((img, index) => {
      img.addEventListener('click', () => {
        currentIndex = index;
        openLightbox(img.src);
      });
    });

    function openLightbox(src) {
      lightbox.style.display = 'flex';
      lightboxImg.src = src;
    }

    function closeLightbox() {
      lightbox.style.display = 'none';
      stopSlideshow();
    }

    function nextImage() {
      currentIndex = (currentIndex + 1) % images.length;
      lightboxImg.src = images[currentIndex].src;
    }

    // Previous Image
    function prevImage() {
      currentIndex = (currentIndex - 1 + images.length) % images.length;
      lightboxImg.src = images[currentIndex].src;
    }

    // Toggle Slideshow
    function toggleSlideshow() {
      if (slideshowInterval) {
        stopSlideshow();
      } else {
        startSlideshow();
      }
    }

    function startSlideshow() {
      document.querySelector('.slideshow').textContent = 'Stop Slideshow';
      slideshowInterval = setInterval(nextImage, 2000);
    }

    function stopSlideshow() {
      document.querySelector('.slideshow').textContent = 'Start Slideshow';
      clearInterval(slideshowInterval);
      slideshowInterval = null;
    }
  </script>
</body>
</html>
