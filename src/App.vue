<template>
  <v-app>
    <!--app-bar를 시작합니다-->
    <v-app-bar
      app
      color="deep-purple accent-3"
      dense
      dark
    ><!--app을 선언해 주어야 알맞은 영역에 붙게된다-->
      <v-app-bar-nav-icon @click="drawer = !drawer" />
      <!--title시작-->
      <site-title :title="site.title"><v-icon>mdi-check</v-icon></site-title>
      <!--title 끝-->
      <v-spacer/>
      <!--app-bar 영역 종료-->
    </v-app-bar><!--e//v-app-bar-->
    <!--네비게이션 시작-->
     <v-navigation-drawer app v-model="drawer" width="400">
      <site-nav :items="site.menu"></site-nav> <!--여기에서 서브메뉴 컴포넌트로 선언됨-->
    </v-navigation-drawer>
    <!--네이게이션 영역 종료-->
     <!--content 시작 -->
    <v-content>
      <router-view/> <!--컴포넌트를 렌더링하여 라우터를 사용-->
    </v-content>
     <!--content 영역 종료 -->
<!--Footer를 시작합니다-->
   <site-footer :footer="site.footer"></site-footer>
<!--Footer 영역 종료-->
  </v-app><!--e//v-app-->
</template>

<script>
import SiteTitle from '@/views/site/title.vue'
import SiteFooter from '@/views/site/footer.vue'
import SiteNav from '@/views/site/nav.vue'

export default {
  components: { SiteTitle, SiteFooter, SiteNav },
  name: 'App',
  data () {
    return {
      drawer: false,
      site: {
        menu: [
          {
            title: 'home',
            icon: 'mdi-home',
            subItems: [
              {
                title: 'Dashboard',
                to: '/'
              },
              {
                title: 'About',
                to: '/about'
              }
            ]
          },
          {
            title: 'about',
            active: true,
            icon: 'mdi-account',
            subItems: [
              {
                title: 'Sub',
                to: '/sub'
              }
            ]
          }
        ],
        title: 'community site created by vue.js code',
        footer: 'Have a good one '
      }
    }
  },
  created () {
    this.subscribe()
  },
  methods: {
    subscribe () {
      this.$firebase.database().ref().child('site').on('value', (sn) => {
        const v = sn.val()
        if (!v) {
          this.$firebase.database().ref().child('site').set(this.site)
          return
        }
        this.site = v
      }, (e) => {
        console.log(e.message)
      })
    }
  }
}
</script>
