<template>
  <v-app dark>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
    >
      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar
      :clipped-left="clipped"
      fixed
      app
    >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-btn
        icon
        @click.stop="miniVariant = !miniVariant"
      >
        <v-icon>mdi-{{ `chevron-${miniVariant ? 'right' : 'left'}` }}</v-icon>
      </v-btn>
      <v-toolbar-title>
        <nuxt-link class="toolbarLink" to="/">{{$t('HongKongAutonomyAction')}}</nuxt-link>
      </v-toolbar-title>
      <v-spacer />
      <v-btn
        icon
        @click.stop="goToFacebook"
      >
        <v-icon>mdi-facebook</v-icon>
      </v-btn>
      <v-btn
        icon
        @click.stop="goToTwitter"
      >
        <v-icon>mdi-twitter</v-icon>
      </v-btn>
      <v-btn
        icon
        @click.stop="goToTelegram"
      >
        <v-icon>mdi-telegram</v-icon>
      </v-btn>
      <v-btn
        icon
        @click.stop="changeLanguage"
      >
        {{$t('CurrentLanguage')}}
      </v-btn>
    </v-app-bar>
    <v-content>
      <v-container>
        <nuxt />
      </v-container>
    </v-content>
    <v-footer
      :fixed="fixed"
      app
    >
      <span>&copy; {{ new Date().getFullYear() }} {{$t('HongKongAutonomyAction')}}{{$t('.')}} {{$t('AllRightsReserved')}}{{$t('.')}}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      clipped: false,
      drawer: false,
      fixed: true,
      miniVariant: false,
      right: true,
      title: 'HongKongAutonomyAction'
    }
  },
  computed: {
    items: function() {
      return [
        {
          icon: 'mdi-home',
          title: this.$t('Home'),
          to: '/'
        },
        {
          icon: 'mdi-chart-bubble',
          title: this.$t('AboutUs'),
          to: '/about-us',
          items: [
            {
              title: this.$t('Founder'),
              to: '/founder'
            }
          ]
        }
      ]
    }
  },
  head() {
    return {
      title: this.$t('HongKongAutonomyAction')
    }
  },
  methods: {
    changeLanguage() {
      const locale = this.$i18n.locale === 'zh-HK' ? 'en-US' : 'zh-HK';
      this.$i18n.setLocale(locale);
    },
    goToFacebook() {
      window.open('https://www.facebook.com/HKAA2019/', '_blank');
    },
    goToTwitter() {
      window.open('https://twitter.com/HKAA2019', '_blank');
    },
    goToTelegram() {
      window.open('https://t.me/HKAA2019', '_blank');
    }
  }
}
</script>

<style scoped>
.toolbarLink {
  text-decoration: none;
  color: inherit;
}
</style>
