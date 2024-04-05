<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
import Navbar from './components/Navbar.vue';
import ImageList from './components/ImageList.vue';
import { ref } from 'vue';
const imageList = ref([
      {
        id:1,
        link: 'https://www.gstatic.com/webp/gallery/1.jpg',
        name: 'Seasandiego.jpg',
        imageSize: '2000x2000',
        physicalSize: '763.3kb',
        photo_by: 'John Doe'
      },
      {
        id:2,
        link: 'https://www.gstatic.com/webp/gallery/2.jpg',
        name: 'iMactwin.jpg',
        imageSize: '2500x1500',
        physicalSize: '845.1kb',
        photo_by: 'admin'
      },
      {
        id:3,
        link: 'https://www.gstatic.com/webp/gallery/3.jpg',
        name: 'hutslecup.jpg',
        imageSize: '1800x2200',
        physicalSize: '632.8kb',
        photo_by: 'Michael Johnson'
      },
      {
        id:4,
        link: 'https://www.gstatic.com/webp/gallery/4.jpg',
        name: 'MSsurface.jpg',
        imageSize: '2100x1800',
        physicalSize: '712.5kb',
        photo_by: 'Sarah Wilson'
      },
    //   {
    //     link: 'https://www.gstatic.com/webp/gallery/5.jpg',
    //     name: 'beach5.jpg',
    //     imageSize: '1900x1700',
    //     physicalSize: '694.2kb',
    //     photo_by: 'Chris Brown'
    //   },
    //   {
    //     link: 'https://www.gstatic.com/webp/gallery/6.jpg',
    //     name: 'beach6.jpg',
    //     imageSize: '2200x1600',
    //     physicalSize: '778.9kb',
    //     photo_by: 'Emily Miller'
    //   },
    //   {
    //     link: 'https://www.gstatic.com/webp/gallery/7.jpg',
    //     name: 'beach7.jpg',
    //     imageSize: '2400x1900',
    //     physicalSize: '803.6kb',
    //     photo_by: 'David Lee'
    //   },
    //   {
    //     link: 'https://www.gstatic.com/webp/gallery/8.jpg',
    //     name: 'beach8.jpg',
    //     imageSize: '2300x2100',
    //     physicalSize: '865.3kb',
    //     photo_by: 'Sophia Garcia'
    //   },
    ]);

const searchImage = (value) => {
  const searchKeyword = value.trim().toLowerCase();
  const filteredImages = imageList.value.filter((image) => {
    const imageName = image.name.toLowerCase();
    return imageName.includes(searchKeyword);
  });

  imageList.value = filteredImages;
};

const filterByPhotoBy = (value) => {
  const photoBy =value;
  if(photoBy=='admin'){
    imageList.value = imageList.value.filter(record => record.photo_by === 'admin');
  }
  //Nếu là all thì sẽ call api lấy lại tất cả bản ghi
};

</script>

<template>
  <header>
    <div class="wrapper">
      <Navbar :imageList="imageList" @search="searchImage" @photoby="filterByPhotoBy"></Navbar>
      <ImageList :imageList="imageList"></ImageList>
    </div>
  </header>

</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
