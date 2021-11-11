<template>
  <div>
    <v-container
    >
      <v-menu offset-y>
        <template v-slot:activator="{ on, attrs }">
          <img src="@/assets/img/search/Google-icon.svg"
               v-bind="attrs"
               v-on="on"
               width="20px" height="36px"/>
        </template>
        <v-list>
          <v-list-item
              v-for="(item, index) in searchItems" link :key="index">
            <v-list-item-title v-text="item"></v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
      <!-- Google -->
      <form
          action="https://www.google.com/search"
          target="_blank"
          v-bind:class="{searchbar_form_active: isSearch}"
          v-if="searchEngine == 'google'"
          class="searchbar_form"
      >
        <v-text-field
            v-on:click="toSearch"
            v-bind:class="{searchbar_input_active: isSearch}"
            type="text"
            name="q"
            autocomplete="off"
            placeholder="Search"
        ></v-text-field>

      </form>

      <!-- Bing -->
      <form
          action="https://www.bing.com/search"
          v-bind:class="{searchbar_form_active: isSearch}"
          v-if="searchEngine == 'bing'"
          class="searchbar_form"
      >
        <input
            v-on:click="toSearch"
            v-bind:class="{searchbar_input_active: isSearch}"
            class="mdui-textfield-input searchbar_input"
            type="text"
            name="q"
            autocomplete="off"
            placeholder="Search"
        >
      </form>

      <!-- Baidu -->
      <form
          action="https://www.baidu.com/s"
          v-bind:class="{searchbar_form_active: isSearch}"
          v-if="searchEngine == 'baidu'"
          class="searchbar_form"
      >
        <input
            v-on:click="toSearch"
            v-bind:class="{searchbar_input_active: isSearch}"
            class="mdui-textfield-input searchbar_input"
            type="text"
            name="wd"
            autocomplete="off"
            placeholder="Search"
        >
      </form>

      <!-- Search button -->
      <div class="search-button">
        <img src="@/assets/img/search/search.svg" width="36px" height="36px"/>
      </div>
    </v-container>
<!--    <v-container>-->


<!--      <v-divider></v-divider>-->
<!--      <v-row no-gutters>-->
<!--        <v-col-->
<!--            cols="12"-->
<!--            sm="6"-->
<!--            md="8"-->
<!--        >-->
<!--          <v-card-->
<!--              class="pa-2"-->
<!--              outlined-->
<!--              tile-->
<!--          >-->
<!--            .col-12 .col-sm-6 .col-md-8-->
<!--          </v-card>-->
<!--        </v-col>-->
<!--        <v-col-->
<!--            cols="6"-->
<!--            md="4"-->
<!--        >-->
<!--          <v-card-->
<!--              class="pa-2"-->
<!--              outlined-->
<!--              tile-->
<!--          >-->
<!--            .col-6 .col-md-4-->
<!--          </v-card>-->
<!--        </v-col>-->
<!--      </v-row>-->
<!--      &lt;!&ndash; Footer &ndash;&gt;-->
<!--      <div class="footer mdui-card mdui-col-xs-12">-->
<!--        <ul class="social-buttons">-->
<!--          <li><a href="https://github.com/appdev/opage" target="_blank"><img src="@/assets/img/footer/github.svg" alt=""-->
<!--                                                                             width="24px" height="24px;"></a></li>-->
<!--          <li><a href="https://www.apkdv.com/" target="_blank"><img src="@/assets/img/footer/about.svg" alt=""-->
<!--                                                                    width="24px" height="24px;"></a></li>-->
<!--        </ul>-->

<!--        <p class="copyright">-->
<!--          © 2017 <a href="https://www.apkdv.com/" target="_blank">APKDV</a>-->
<!--        </p>-->
<!--      </div>-->

<!--    </v-container>-->
  </div>
</template>

<script>
import Store from '@/store'

Store.setCookie("se", "google", 365);
export default {
  name: 'HelloWorld',

  data: () => ({
    ecosystem: [
      {
        text: 'vuetify-loader',
        href: 'https://github.com/vuetifyjs/vuetify-loader',
      },
      {
        text: 'github',
        href: 'https://github.com/vuetifyjs/vuetify',
      },
      {
        text: 'awesome-vuetify',
        href: 'https://github.com/vuetifyjs/awesome-vuetify',
      },
    ],
    importantLinks: [
      {
        text: 'Documentation',
        href: 'https://vuetifyjs.com',
      },
      {
        text: 'Chat',
        href: 'https://community.vuetifyjs.com',
      },
      {
        text: 'Made with Vuetify',
        href: 'https://madewithvuejs.com/vuetify',
      },
      {
        text: 'Twitter',
        href: 'https://twitter.com/vuetifyjs',
      },
      {
        text: 'Articles',
        href: 'https://medium.com/vuetify',
      },
    ],
    whatsNext: [
      {
        text: 'Explore components',
        href: 'https://vuetifyjs.com/components/api-explorer',
      },
      {
        text: 'Select a layout',
        href: 'https://vuetifyjs.com/getting-started/pre-made-layouts',
      },
      {
        text: 'Frequently Asked Questions',
        href: 'https://vuetifyjs.com/getting-started/frequently-asked-questions',
      },
    ],
    searchItems: ["Google", "Baidu", "Bing"],
    searchEngine: Store.getCookie('se'),
  }), methods: {
    useGoogle: function () {
      this.searchEngine = 'google';
      Store.setCookie("se", "google", 30);
    },
    useBing: function () {
      this.searchEngine = 'bing';
      Store.setCookie("se", "bing", 30);
    },
    useBaidu: function () {
      this.searchEngine = 'baidu';
      Store.setCookie("se", "baidu", 30);
    }
  }
}
</script>
<style lang="scss">

.search_switch {
  margin: 0;
  text-align: center;
  width: 40px;
  height: 36px;
  background-color: #fff;
  color: rgba(0, 0, 0, .87);
  text-overflow: clip;
  overflow: hidden;
  cursor: pointer;
}

.search_switch_active {
  width: 0;
  height: 56px;
}

#search_engine {
  width: 100px;
}

.searchbar {
  margin-bottom: 10px;
  transition: .7s;
}

.searchbar_active {
  padding: 0;
  margin-top: -56px;
  transition: .7s;
  z-index: 2000;
}

.searchbar_form {
  width: calc(100% - 40px);
  margin: 0;
}

.searchbar_form_active {
  width: 100%;
}

.searchbar_input {
  padding: 0;
  height: 36px;
  /*background-color: #e9f3fc;*/
  background-color: #fff;
  color: #000;
  border: 0;
}

.searchbar_input_active {
  padding: 0 16px;
  height: 56px;
}

.search-button {
  display: none;
}
</style>

