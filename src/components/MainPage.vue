<template>
  <v-app id="chewedfeed" dark>
    <v-navigation-drawer fixed>
      <v-toolbar flat class="transparent">
        <v-list class="pa-0">
          <v-list-tile avatar>
            <v-list-tile-avatar>
              <img src="//assets.chewedfeed.com/logo.png" >
            </v-list-tile-avatar>
            <v-list-tile-content>
              <v-list-tile-title>ChewedFeed</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
        </v-list>
      </v-toolbar>

      <v-list class="pt-0" dense>
        <v-divider></v-divider>

        <v-list-group v-for="feed in feeds" v-model="feed.active" :key="feed.title" no-action>
          <v-list-tile slot="activator">
            <v-list-tile-avatar size="25">
              <img :src="feed.icon">
            </v-list-tile-avatar>
            <v-list-tile-content>
              <v-list-tile-title v-text="feed.title"></v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
          <v-list-tile v-for="feedItem in feed.items" :key="feedItem.date" @click="reader = feedItem.link">
            <v-list-tile-content>
              <v-list-tile-title v-text="feedItem.title"></v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
        </v-list-group>

      </v-list>
    </v-navigation-drawer>

    <v-toolbar app fixed>
      <v-spacer></v-spacer>
      <v-toolbar-items>
        <v-btn flat to="/">Home</v-btn>
        <v-btn flat to="/feeds">Feeds List</v-btn>
        <v-btn flat to="/add">Add Feed</v-btn>
        <v-btn flat :loading="loading" :disabled="loading" @click="loader = 'loading'">Subscribe</v-btn>
      </v-toolbar-items>
    </v-toolbar>

    <v-content>
      <v-container fill-height>
        <v-flex offset-xs2 fill-height id="contentArea">
          <p>Bacon ipsum dolor amet flank cow burgdoggen shank. Boudin swine brisket burgdoggen ball tip. Beef pig rump, tri-tip fatback kielbasa jowl strip steak swine shankle drumstick. Ham shankle pancetta t-bone venison bresaola, meatball pig beef.</p>
          <p>Prosciutto shoulder cow frankfurter drumstick picanha corned beef hamburger rump spare ribs salami ribeye biltong. Tongue fatback short ribs andouille. Pastrami frankfurter beef ribs flank beef brisket kielbasa. Alcatra kevin frankfurter hamburger ball tip jowl. Biltong bacon meatloaf, porchetta brisket shankle sausage t-bone fatback doner strip steak cow short ribs flank.</p>
          <p>Meatball sirloin meatloaf, burgdoggen pastrami flank buffalo picanha. Turkey cupim corned beef jowl tail, brisket pork belly. Kevin leberkas cupim, t-bone corned beef pork chop ball tip andouille drumstick. Bresaola tri-tip shankle, kevin picanha biltong beef ribs beef brisket frankfurter venison ham hock pig pork chop tail.</p>
          <p>Ball tip sirloin venison landjaeger pig, pork chop meatloaf. Turkey capicola turducken boudin. Tongue leberkas biltong spare ribs filet mignon, kevin bacon bresaola pancetta. Shankle tail brisket sirloin shank hamburger andouille pork loin tongue pork belly landjaeger meatloaf ham. Drumstick leberkas porchetta tail, pork chop meatloaf brisket short loin ground round. Andouille short ribs leberkas beef ribs.</p>
          <p>Porchetta cupim andouille prosciutto ground round. Jerky sirloin beef ribs sausage t-bone. Ribeye tongue capicola buffalo. Frankfurter doner kevin ground round, t-bone pig pork belly chicken. Prosciutto shankle chuck bresaola flank short ribs. Strip steak turducken brisket sausage, pastrami cow tail kevin short loin shankle doner kielbasa bacon biltong. Meatloaf shoulder swine cow pork meatball picanha strip steak doner bacon ham hock sirloin tenderloin burgdoggen.</p>
          <p>Does your lorem ipsum text long for something a little meatier? Give our generator a try… it’s tasty!</p>
        </v-flex>
      </v-container>
    </v-content>
    <v-content id="preLoad"></v-content>
  </v-app>
</template>

<script>
export default {
  name: 'MainPage',
  data: () => {
    return {
      drawer: false,
      right: null,
      loader: null,
      reader: null,
      loading: false,
      feeds: [
        {
          title: '9to5Mac',
          icon: 'https://s2.wp.com/wp-content/themes/vip/9to5-2015/images/favicons/9to5mac/9to5mac-touch-icon-iphone.png',
          active: false,
          items: [
            {
              title: '100 Views of Silicon Valley\' project combines iPad creativity with traditional painting',
              link: 'https://9to5mac.com/2018/05/31/silicon-valley-ipad-painting/',
              date: 1
            },
            {
              title: 'Apple Watch: How to customize the Dock',
              link: 'https://9to5mac.com/2018/05/31/apple-watch-how-to-customize-dock/',
              date: 2
            }
          ]
        }
      ]
    }
  },
  watch: {
    loader: () => {
      const l = this.loader
      this[l] = !this[l]

      setTimeout(() => (this[l] = false), 3000)

      this.loader = null
    },
    reader: (link) => {
      const c = document.getElementById('contentArea')
      let cc = c.firstChild
      while (cc) {
        c.removeChild(cc)
        cc = c.firstChild
      }

      let i = document.createElement('iframe')
      i.width = '100%'
      i.height = window.innerHeight
      i.src = link
      c.appendChild(i)
    }
  }
}
</script>
