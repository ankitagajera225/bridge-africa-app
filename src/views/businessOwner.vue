<template>
  <div class="" style="overflow-y: hidden; padding:0px">
    <navbar />

    <div class="container-fluid">
      <ly-tab
        v-model="selectedId"
        :items="items"
        :options="options"
        class="center-ly"
      >
      </ly-tab>

      <hr width="100%" class="d-none" d-md-block />
    </div>

    <div class="mt-3" v-if="selectedId == '0'">
      <Business />
    </div>

    <div class="mt-3" v-if="selectedId == '1'">
      <Inbox />
    </div>

    <div class="mt-3" v-if="selectedId == '2'">
      <Settings v-bind:currenttab="selectedId" />
    </div>

    <div class="mt-3" v-if="selectedId == '3'">
      <Settings v-bind:currenttab="selectedId" />
    </div>

    <div class="mt-3" v-if="selectedId == '4'">
      <Settings v-bind:currenttab="selectedId" />
    </div>

    <div class="mt-3" v-if="selectedId == '5'">
      <Settings v-bind:currenttab="selectedId" />
    </div>

    <Footer />
  </div>
</template>

<script>
import navbar from "@/components/navbar";
import Business from "../components/businessOwner/business";
//import Pending from "../components/businessOwner/pending";
//import Insight from "../components/businessOwner/insight";
//import Notification from "../components/businessOwner/notification";
import Settings from "../components/businessOwner/settings";

import Inbox from "../components/businessOwner/inbox";

import LyTab from "@/tab/src/index.vue";

import axios from "axios";

import Footer from "../components/footer";
export default {
  name: "Home",
  components: {
    navbar,
    Business,
    //Pending,
    LyTab,
    Settings,
    //  Insight,
    Inbox,
    // Notification,
    Footer
  },
  data() {
    return {
      selectedId: 0,
      bottomSelectedId: 0,
      url_data: null,
      items: [
        { label: "Home ", icon: "" },

        { label: "Inbox", icon: "" },
        { label: "Notification", icon: "" },
        { label: "Pending Post", icon: "" },
        { label: "Insight", icon: "" },

        { label: "Settings", icon: "" }
      ],
      options: {
        activeColor: "#1d98bd"
      }
    };
  },

  methods: {
    businessInfo() {
      this.$store
        .dispatch("businessOwner/businessInfo", this.url_data)
        .then(() => {
          console.log("hey yeah");
        })
        .catch(err => {
          console.log({ err: err });
        });
    },

    CommunityBusiness() {
      this.$store
        .dispatch("businessOwner/CommunityBusiness", this.url_data)
        .then(() => {
          console.log("hey yeah");
        })
        .catch(err => {
          console.log({ err: err });
        });
    },

    CommunityPeople() {
      this.$store
        .dispatch("businessOwner/CommunityPeople", this.url_data)
        .then(() => {
          console.log("hey yeah");
        })
        .catch(err => {
          console.log({ err: err });
        });
    },

    businessCommunityTotal() {
      this.$store
        .dispatch("businessOwner/businessCommunityTotal", this.url_data)
        .then(() => {
          console.log("hey yeah");
        })
        .catch(err => {
          console.log({ err: err });
        });
    },

    ownerPost() {
      this.$store
        .dispatch("businessOwner/ownerPost", this.url_data)
        .then(() => {
          console.log("hey yeah");
        })
        .catch(err => {
          console.log({ err: err });
        });
    }
  },
  computed: {},

  mounted() {
    this.url_data = this.$route.params.id;

    console.log(this.url_data);

    this.businessInfo();

    this.CommunityBusiness();

    this.CommunityPeople();

    this.businessCommunityTotal();
    this.ownerPost();
  }
};
</script>

<style scoped>
.mar-left {
  margin-left: 25px;
}
.tabs {
  width: 100%;
}
.settings {
  margin-left: 90%;
  position: relative;
  top: 40px;
}

.a-left {
  align-content: left;
}

.nav-text {
  cursor: pointer;
}

.tab-title-class {
  color: #ffffff !important;
}

@media only screen and (max-width: 768px) {
  .settings {
    top: -5px;
    left: -20px;
  }
}
</style>

<style>
.business-owner-tab .nav-link {
  display: block;
  padding: 0.5rem 1rem;
  padding-top: 1px;

  padding-bottom: 1px;
  padding: 1px;
  padding-right: 1px;
  padding-left: 1px;
  text-align: center;
  padding-left: 10px;
  padding-right: 20px;
  border: 1px solid gray;
}

@media only screen and (max-width: 768px) {
  .business-owner-tab .nav-pills .nav-link {
    border-radius: 0.25rem;
    font-size: 10px;
    margin-left: -8px;
    padding-left: 0px;
    padding-right: 0px;
  }
}

.nav-pills .nav-link.active,
.nav-pills .show > .nav-link {
  background-color: #e6e6e6;
}

.center-ly {
  margin-top: -25px;
}

.hrr {
  margin-top: 0px;
}
</style>
