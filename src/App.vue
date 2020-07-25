<template>
  <div>

    <div class="row">
      <div class="logo">
        <embed src="../img/Samsung_Electronics_logo.png" id="logo">
      </div>
      <div class="searchForm">
        <span class="icon-search"></span>
        <input type="search"/>
        <input type="button" value="ПОИСК"/>
      </div>
    </div>

    <div class="row">
      <nav>
        <span class="toggle" @click="menuHidd = !menuHidd">☰</span>
        <ul class="menu" v-show="menuHidd">
          <li v-for="menuItem in menuList">
            <a href="#">
            {{ menuItem.name }}
            <i class="icon-down-open-big"></i>
           </a></li>
       </ul>
      </nav>
    </div>

    <div class="row">
      <span><u>Главная</u> / Корзина</span>
    </div>

    <div class="row">
      <cart></cart>
    </div>

  </div>
</template>

<script>
import cart from './Cart.vue';

export default {
  name: 'app',
  data () {
    return {
      menuHidd: true,
      menuList: [
        {
          name: 'каталог продукции'
        },
        {
          name: 'все бренды'
        },
        {
          name: 'подарки на 14 февраля'
        },
        {
          name: 'подарки на 23 февраля'
        },
        {
          name: 'подарки на 8 марта'
        }
      ]
    }
  },
   components:{
      cart
    }
}
</script>
