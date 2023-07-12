<script lang="ts">
export default {
  methods: {
    onAuth(user: any) {
      console.log(user);
    }
  },
  async mounted() {
    await gapi.client.setApiKey("AIzaSyB6VnlDU-bcMARarsyuhovRokiStqPiBIk");
    await gapi.client.load("https://www.googleapis.com/discovery/v1/apis/youtube/v3/rest")
      .then(() => console.log("GAPI Loaded Successfully"))
      .catch(() => console.log("Error Loading GAPI"));

    google.accounts.id.initialize({
      client_id: "281401900182-udhm7ek5gmvl1he0q9b4e7m8v02840kq.apps.googleusercontent.com",
      callback: this.onAuth,
      context: "signin",
      ux_mode: "popup"
    });

    google.accounts.id.renderButton(document.querySelector('#signin'), {});
    
    gapi.client.youtube.channels.list({
      part: ["snippet,statistics"],
      id: ["UC_x5XG1OV2P6uZZ5FSM9Ttw"],
      maxResults: 1
    }).then((res: any) => {
      console.log(res.result.items[0])
    });
  }
};
</script>

<template>
  <div id="signin"></div>
</template>
