<template>
  <div class=" p-0 mt-3">
    <div class="container-fluid border">
      <b-tabs pills content-class="mt-3  f-left">
        <b-tab title="People" active>
          <People />
        </b-tab>

        <b-tab title="Businesses">
          <Business />
        </b-tab>

        <b-tab title="Netwoks">
          <Network />
        </b-tab>
      </b-tabs>
    </div>
  </div>
</template>

<script>
import Business from "./businesses/businesses";
import People from "./people/people";
import Network from "./network/network";

export default {
  name: "SidebarCommunity",
  components: {
    Business,
    People,
    Network
  },

  data() {
    return {
      perPage: 3,
      currentPage: 1,
      items: [
        { id: 1, first_name: "Fred", last_name: "Flintstone" },
        { id: 2, first_name: "Wilma", last_name: "Flintstone" },
        { id: 3, first_name: "Barney", last_name: "Rubble" },
        { id: 4, first_name: "Betty", last_name: "Rubble" },
        { id: 5, first_name: "Pebbles", last_name: "Flintstone" },
        { id: 6, first_name: "Bamm Bamm", last_name: "Rubble" },
        { id: 7, first_name: "The Great", last_name: "Gazzoo" },
        { id: 8, first_name: "Rockhead", last_name: "Slate" },
        { id: 9, first_name: "Pearl", last_name: "Slaghoople" }
      ]
    };
  },
  computed: {
    rows() {
      return this.items.length;
    }
  }
};
</script>

<style scoped>
hr {
  border: solid 1px dimgray;
}

.btn {
  background-color: #fff;
  color: #e75c18;
  border: solid 1px #e75c18;
}

.btn:hover {
  color: #fff;
  border: none;
  background-color: #e75c18;
}

f-right {
  text-align: right;
  align-content: right;
}

.f-left {
  text-align: left;
  align-content: left;
}
@media only screen and (max-width: 768px) {
  .options {
    position: relative;
    left: -75px;
  }
}

.detail {
  position: relative;
  left: 92px;
  top: -30px;
}
.name {
  position: relative;
  top: -10px;
  left: 10px;
}

.b-background {
  background-color: red;
  color: white;
}

.people-style {
  border-top-left-radius: 40px;

  border-bottom-left-radius: 40px;

  border-top-right-radius: 15px;

  border-bottom-right-radius: 15px;

  height: 78px;

  background: white;

  background-color: #fff;
  background-clip: border-box;
  border: 1px solid rgba(0, 0, 0, 0.125);

  margin-bottom: 10px;
  margin-right: -30px;
  margin-left: -30px;
}

.p-buttons {
  margin-right: 1px;

  margin-left: -5px;
  margin-bottom: 2.5px;
  margin-top: 2.5px;

  padding-right: 5px;
}

.e-name {
  margin-right: -12px;
  margin-left: -25px;
}
.p-avater {
  margin-right: -10px;
}
.a-text {
  margin-top: 2px;
}
</style>
