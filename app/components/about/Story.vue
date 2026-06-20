<template>
  <div class="wrapper-advantages">
    <div class="content-advantages">
      <div class="icons">
        <div class="icon-wrapper">
          <div class="icon">
            <img src="/icons_about/marks3.png" alt="medal" />
            <h2>20 лет</h2>
          </div>
          
          <div class="text">
            <p>Опыта работы в пенном бизнесе у собственника и команды</p>
          </div>
        </div>
        <div class="icon-wrapper">
          <div class="icon">
            <img src="/icons_about/marks4.png" alt="people" />
            <h2>&gt; 100</h2>
          </div>
          
          <div class="text">
            <p>Партнеров по всей России</p>
          </div>
        </div>
        <div class="icon-wrapper">
          <div class="icon">
            <img src="/icons_about/marks1.png" alt="heart" />
            <h2>&gt; 500</h2>
          </div>
          
          <div class="text">
            
            <p>Сортов пива представлено в ассортименте</p>
          </div>
        </div>
        <div class="icon-wrapper">
          <div class="icon">
            <img src="/icons_about/marks2.png" alt="up" />
            <h2>&gt; 15</h2>
          </div>
          
          <div class="text">        
            <p>Федеральных заводов по производству пива сотрудничают с нами</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup></script>

<style scoped>
.wrapper-advantages {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 350px;
}

.content-advantages {
  display: flex;
  gap: 2rem;
}

.icons {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
}

.icon-wrapper {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
  width: 100%;
  flex: 1;
}

.icon {
  width: 170px;
  height: 100px;
  border-radius: 50%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 1rem;
}

.icon img {
  width: 80px;
  height: 80px;
  margin-bottom: 1rem;
}

.text {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  gap: 1rem;
  width: 60%;
  flex: 1;
  margin-top: 1rem;
}

h2 {
  font-size: var(--text-4xl);
  font-family: var(--font-rubik);
  color: var(--color-amber-700);
  font-weight: var(--font-weight-medium);
}

p {
  font-size: var(--text-base);
  font-family: var(--font-nunito);
  color: var(--color-gray-600);
  font-weight: var(--font-weight-medium);
}

/* Адаптив */
@media (max-width: 1024px) {
  .content-advantages {
    gap: 1.5rem;
  }
}

@media (max-width: 768px) {
  .wrapper-advantages {
    height: auto;
    padding: 2rem 0;
    min-width: 360px;
  }

  .text {
    align-items: flex-start;
  }
  
  .icons {
    flex-direction: column;
    gap: 2rem;
  }
  
  .icon-wrapper {
    flex-direction: row;
    text-align: left;
    gap: 1.5rem;
  }
  
  h2 {
    font-size: var(--text-3xl);
  }


}
</style>
