<script setup>
import Navbar from '@/components/Navbar.vue'
</script>

<template>
  <body>
    <Navbar />
    <main>
      <div class="space-info">
        <div class="space-text">
          <h2>SO, YOU WANT TO TRAVEL TO</h2>
          <h1>SPACE</h1>
          <P>Let’s face it; if you want to go to space, you might as well genuinely go to outer space and not hover kind
            of on the edge of it. Well sit back, and relax because we’ll give you a truly out of this world experience!
          </P>
        </div>
        <div class="space-button">
          <button>
            <p>EXPLORE</p>
          </button>
        </div>
      </div>
    </main>
  </body>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Bellefair&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Barlow:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap');

body {
  margin: 0;
  padding: 0;
  font-family: 'Roboto', sans-serif;
  background-color: black;
  background-image: url('@/assets/image/background-home-desktop.png');
}

main {
  padding: 1rem;
}

.space-info {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  padding: 2rem;
  padding-top: 10rem;
  padding-bottom: 10rem;
}

.space-text {
  display: flex;
  flex-direction: column;
  padding: 2rem;
  padding-left: 5rem;
  padding-right: 5rem;
  width: 50%;
}

.space-text h2 {
  color: #D0D6F9;
  font-size: 1.5rem;
  font-family: 'Barlow Condensed', sans-serif;
  letter-spacing: 3px;
}

.space-text h1 {
  color: white;
  font-size: 8rem;
  font-family: 'Bellefair', serif;
  margin: 0;
}

.space-text p {
  width: 70%;
  color: #D0D6F9;
  font-size: 1.3rem;
  margin-bottom: 1rem;
  font-family: 'Barlow', sans-serif;
}

.space-button {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 2rem;
  padding-left: 5rem;
  padding-right: 5rem;
  width: 50%;
}

.space-button button {
  width: 274px;
  height: 274px;
  border-radius: 50%;
  background-color: white;
  border: none;
}

.space-button button p {
  color: #0B0D17;
  font-size: 2rem;
  font-family: 'Bellefair', serif;
  margin: 0;
}

.space-button button:hover {
  outline: 80px solid rgba(255, 255, 255, 0.1);
  transition: 0.4s;
}

@media (max-width: 767.98px) {

  body {
    background-image: url('@/assets/image/background-mobile-home.png');
  }

  .space-info {
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding-top: 5rem;
    padding-bottom: 5rem;
  }

  .space-text {
    display: flex;
    align-items: center;
    width: 100%;
    padding: 0;
    padding-bottom: 2rem;
  }

  .space-text h2 {
    font-size: 1.2rem;
    letter-spacing: 2px;
  }

  .space-text h1 {
    font-size: 5rem;
  }

  .space-text p {
    width: 115%;
    font-size: 1rem;
    text-align: center;
  }

  .space-button {
    width: 100%;
    padding: 0;
    padding-top: 2rem;
    padding-bottom: 2rem;
  }

  .space-button button {
    width: 200px;
    height: 200px;
  }

  .space-button button p {
    font-size: 1.5rem;
  }

  .space-button button:hover {
    outline: 50px solid rgba(255, 255, 255, 0.1);
  }
}

@media (min-width: 768px) and (max-width: 1024px) {
  
    .space-info {
      flex-direction: column;
      align-items: center;
      justify-content: center;
      padding-top: 5rem;
      padding-bottom: 5rem;
    }
  
    .space-text {
      display: flex;
      align-items: center;
      width: 100%;
      padding: 0;
      padding-bottom: 2rem;
    }
  
    .space-text h2 {
      font-size: 1.5rem;
      letter-spacing: 3px;
    }
  
    .space-text h1 {
      font-size: 10rem;
    }
  
    .space-text p {
      width: 60%;
      font-size: 1.2rem;
      text-align: center;
      margin-bottom: 5rem;
    }
  
    .space-button {
      width: 100%;
      padding: 0;
      padding-top: 2rem;
      padding-bottom: 2rem;
    }
  
    .space-button button {
      width: 200px;
      height: 200px;
    }
  
    .space-button button p {
      font-size: 1.5rem;
    }
  
    .space-button button:hover {
      outline: 50px solid rgba(255, 255, 255, 0.1);
    }
}
</style>
