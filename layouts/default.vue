<template>
  <v-app dark>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      width="375"
      fixed
      app
    >
      <v-list>
        <template
          v-for="item in items"
        >
          <v-list-group
            v-if="item.items"
            :key="item.title"
            :prepend-icon="item.icon"
            no-action
          >
            <template v-slot:activator>
              <v-list-item-content>
                <v-list-item-title v-text="item.title"></v-list-item-title>
              </v-list-item-content>
            </template>

            <v-list-item
              v-for="subItem in item.items"
              :key="subItem.title"
              :to="subItem.to"
              router
              exact
            >
              <v-list-item-content>
                <v-list-item-title v-text="subItem.title"></v-list-item-title>
              </v-list-item-content>
            </v-list-item>
          </v-list-group>

          <v-list-item
            v-else
            :key="item.title"
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
        </template>

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
              to: '/about-us/founder'
            },
            {
              title: this.$t('History'),
              to: '/about-us/history'
            },
            {
              title: this.$t('Philosophy'),
              to: '/about-us/philosophy'
            },
            {
              title: this.$t('ContactUs'),
              to: '/about-us/contact-us'
            }
          ]
        },
        {
          icon: 'mdi-sign-caution',
          title: this.$t('Demonstration'),
          to: '/demonstration'
        },
        {
          icon: 'mdi-run',
          title: this.$t('Action'),
          to: '/action',
          items: [
            {
              title: this.$t('CreatePetitionTheWhiteHouse'),
              to: '/action/create-petition-the-white-house'
            },
            {
              title: this.$t('RescueAsylumSeekersOversea'),
              to: '/action/rescue-asylum-seekers-oversea'
            },
            {
              title: this.$t('HangBannerFromLionRock'),
              to: '/action/hang-banner-from-lion-rock'
            },
            {
              title: this.$t('MeetSenatorAtTheAirport'),
              to: '/action/meet-senator-at-the-airport'
            },
            {
              title: this.$t('SendChristmasCard'),
              to: '/action/send-christmas-card'
            },
            {
              title: this.$t('ShootVideoShow'),
              to: '/action/shoot-video-show'
            },
            {
              title: this.$t('ResearchForHongKongCulturalProspect'),
              to: '/action/research-for-hong-kong-cultural-prospect'
            }
          ]
        },
        {
          icon: 'mdi-share-variant',
          title: this.$t('Propaganda'),
          to: '/propaganda',
          items: [
            {
              title: this.$t('AmericanFlag'),
              to: '/propaganda/american-flag'
            },
            {
              title: this.$t('AmericanNationalAnthem'),
              to: '/propaganda/american-national-anthem'
            },
            {
              title: this.$t('Banner'),
              to: '/propaganda/banner'
            },
            {
              title: this.$t('Placard'),
              to: '/propaganda/placard'
            },
            {
              title: this.$t('Foamboard'),
              to: '/propaganda/foamboard'
            },
            {
              title: this.$t('Couplet'),
              to: '/propaganda/couplet'
            },
            {
              title: this.$t('OpenLetter'),
              to: '/propaganda/open-letter'
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
