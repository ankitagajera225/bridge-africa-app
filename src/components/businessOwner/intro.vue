<template>
  <div>
    <b-card title="" header-tag="header" footer-tag="footer">
      <div style="float:right" class="edit" @click="editContact">
        <b-icon icon="pencil-fill" variant="primary"></b-icon>
      </div>
      <h6 class="mb-2"><b>Intro</b></h6>

      <b-card-text>
        <p>
          <b-icon icon="briefcase-fill" class="primary icon-size"></b-icon>
          {{ business_intro.category }}
        </p>
        <p>
          <b-icon icon="search" class="primary icon-size"></b-icon>
          {{ business_intro.keywords }}
        </p>
        <p>
          <b-icon icon="geo-alt-fill" class="primary icon-size"></b-icon>
          Mokolo, Yaounde, Cameroon
        </p>
        <p>
          <b-icon icon="link" class="primary icon-size"></b-icon>
          www.business.com
        </p>
        <p>
          <b-icon icon="people-fill" class="primary icon-size"></b-icon>
          {{ business_intro.community }} Community
        </p>
        <p>
          <b-icon icon="telephone-fill" class="primary icon-size"></b-icon>
          {{ business_intro.phone }}
        </p>
        <p>
          <b-icon icon="envelope-fill" class="primary icon-size"></b-icon>
          {{ business_intro.email }}
        </p>
        <p>
          <b-icon icon="clock" class="primary icon-size"></b-icon>
          <b-link> Open now</b-link>
          <br />
          <b-dropdown size="sm" variant="transperent">
            <template #button-content>
              10:00AM - 7:00PM
            </template>
            <b-dropdown-item> 10:00AM - 7:00PM</b-dropdown-item>
          </b-dropdown>
        </p>
      </b-card-text>

      <GmapMap
        :center="position"
        :zoom="12"
        style="width:100%;  height: 250px;"
      >
        <GmapMarker :position="position" />
      </GmapMap>
    </b-card>

    <b-modal
      id="bv-modal-example2"
      hide-footer
      title="Edit Address"
      v-model="edit2"
      size="lg"
    >
      <b-form>
        {{ blec }}
        <b-row>
          <div class="form-group col-md-6">
            <label for="username">Busness Name:</label><br />
            <input
              type="text"
              name="name"
              id="name"
              placeholder="Busness Name"
              class="form-control"
              :state="validateState('name')"
              v-model="form.name"
            />
          </div>

          <div class="form-group col-md-6">
            <label for="alias">Category:</label><br />

            <b-form-select
              :options="categories"
              class="mb-3"
              value-field="item"
              v-model="form.category"
              text-field="name"
            ></b-form-select>
          </div>
        </b-row>

        <b-row>
          <b-form-group
            id="input-group-2"
            label="Phone Contact"
            label-for="input-2"
            label-size="sm"
            class="col-md-6"
          >
            <b-form-input
              id="input-1"
              class="mt-1"
              v-model="form.phone"
              type="tel"
              required
            ></b-form-input>
          </b-form-group>

          <b-form-group
            class="col-md-6"
            id="input-group-2"
            label="Business Email"
            label-for="input-2"
            label-size="sm"
          >
            <b-form-input
              id="input-1"
              class="mt-1"
              v-model="form.email"
              type="email"
              required
            ></b-form-input>
          </b-form-group>
        </b-row>

        <b-row>
          <div class="form-group col-md-6">
            <label for="username">Keywords</label><br />
            <div class="col-md-12 pl-0 pr-0">
              {{ form.keywords }}

              <input
                type="text"
                name="alias"
                id="alias"
                placeholder="Enter your Keywords"
                class="form-control"
                v-model="form.keywords"
              />
            </div>
          </div>

          <div class="form-group col-md-6">
            <label for="country" class="username"> Country :</label><br />

            <country-select
              v-model="form.country"
              :country="country"
              topCountry="CM"
              class="form-control text"
            />
          </div>
        </b-row>

        <b-row>
          <div class="form-group col-md-6">
            <label for="country" class="username"> Region :</label><br />

            <region-select
              v-model="form.region"
              :country="country"
              :region="region"
              class="form-control text"
            />
          </div>

          <b-form-group
            id="input-group-2"
            label="City"
            label-for="input-2"
            label-size="sm"
            class="col-md-6"
          >
            <b-form-input
              id="input-1"
              class="mt-1"
              v-model="form.city"
              type="text"
              required
            ></b-form-input>
          </b-form-group>
        </b-row>
        <!--
        <b-form-group
          id="input-group-2"
          label="Neigbourhood"
          label-for="input-2"
          label-size="sm"
          class="col-md-6"
        >



         <b-form-input
            id="input-1"
            class="mt-1"
            v-model="form.Neigbourhood"
            type="text"
            required
          ></b-form-input>
         
        </b-form-group>

-->

        <b-button class="mt-3 btn-block" variant="primary" @click="validate">
          Modify
        </b-button>
      </b-form>
    </b-modal>
  </div>
</template>

<script>
import axios from "axios";

import { validationMixin } from "vuelidate";

import { required, email, minLength } from "vuelidate/lib/validators";

export default {
  mixins: [validationMixin],
  data() {
    return {
      form: this.$store.state.businessOwner.businessInfo,
      blec: this.business_intro,
      center: null,

      country: null,
      region: null,
      url: null,

      markers: [],

      position: {
        lat: 0,
        lng: 0,
      },

      currentPlace: null,

      places: [],

      category: "",
      categories: [
        { item: "Professional_and_home_service", name: "Professionals" },
        { item: "Agriculture ", name: "Agriculture " },
        { item: "Restaurant ", name: " Restaurant " },
        { item: "Electronics ", name: "Electronics " },
        { item: "Handicrafts", name: "Handicrafts" },
        { item: "clothing", name: "clothing" },
        { item: "Mechanics", name: "Mechanics" },
        { item: "Health_unit ", name: "Health unit " },
        { item: "Bars", name: "Bars" },
        { item: "Hair_and_beauty ", name: "Hair and beauty " },
        { item: "Real_estate ", name: "Real_estate " },
        { item: "Travelling ", name: "Travelling " },
        { item: "Hotels", name: "Hotels" },
        { item: "station", name: " station  " },
        { item: "Mayor_concils", name: "Mayor_concils" },
        { item: "Taxis service", name: "Taxis service" },
      ],

      edit1: false,
      edit2: false,
      leftTitle: "About Mapoure Agrobusiness",
      textToo:
        "Lorem ipsum dolor sit amet consectetur adipisicing elit.\n" +
        "              Asperiores temporibus, rerum iste id obcaecati quae odit accusamus\n" +
        "              reprehenderit, ipsa nam laudantium pariatur. Harum, soluta. Nam\n" +
        "              accusantium hic numquam architecto debitis. Lorem ipsum dolor sit\n" +
        "              amet consectetur adipisicing elit. Asperiores temporibus, rerum\n" +
        "              iste id obcaecati quae odit accusamus reprehenderit, ipsa nam\n" +
        "              laudantium pariatur. Harum, soluta. Nam accusantium hic numquam\n" +
        "              architecto debitis. Asperiores temporibus, rerum iste id obcaecati\n" +
        "              quae odit accusamus reprehenderit, ipsa nam laudantium pariatur.\n" +
        "              Harum, soluta. Nam accusantium hic numquam architecto debitis.",
      workedAt: "Current or Last Organization",
      lastEducation: "Last Education",
      homeTown: "Dummy",
      cityName: "Dummy",
      followed: "525",
      telephone: "+1 (234) 567-8974",
      email: "info@businessname.com",
    };
  },

  validations: {
    form: {
      name: {
        required,
      },

      category: {
        required,
      },
    },
  },

  methods: {
    /**
     * Used to edit biography
     * @return void
     */


    getValidationClass(fieldName) {
      const field = this.$v.form[fieldName];
      if (field) {
        return {
          red: field.$invalid && field.$dirty,
        };
      }
    },

    validate() {
      this.$v.form.$touch();
      if (this.$v.form.$anyError) {
        console.log("error error");
        return false;
      } else {
        console.log("no error error");

        this.UpdateBusiness();
        return true;
      }
    },

    UpdateBusiness() {
      let formData2 = new FormData();

      formData2.append("region", this.form.region);
      formData2.append("city", this.form.city);
      formData2.append("country", this.form.country);

      formData2.append("address", this.form.adress);

      formData2.append("lat", this.form.lat);
      formData2.append("lng", this.form.lng);

      formData2.append("neighbor", this.form.neighbor);

      formData2.append("name", this.form.name);
      formData2.append("category", this.form.category);
      formData2.append("keywords", this.form.keywords);
      formData2.append("phone", this.form.phone);
      formData2.append("email", this.form.email);
      formData2.append("about_business", this.about);

      this.axios
        .post("business/update/" + this.url, formData2, {
          headers: {
            "Content-Type": "multipart/form-data",
          },
        })
        .then((response) => {
          console.log(response);

          this.flashMessage.show({
            status: "success",
            blockClass: "custom-block-class",
            message: "Business Profile updated",
          });
        })
        .catch((err) => {
          console.log({ err: err });

          this.sendingB = false;

          if (err.response.status == 422) {
            console.log({ err: err });
            console.log(err.response.data.message);

            this.flashMessage.show({
              status: "error",

              message: err.response.data.message,
              blockClass: "custom-block-class",
            });
          } else {
            this.flashMessage.show({
              status: "error",

              message: "Unable to update Your Business",
              blockClass: "custom-block-class",
            });
            console.log({ err: err });
          }
        });
    },

    setcoordintes() {
      //  this.position.lat = this.$store.state.businessOwner.businessInfo.lat;
      this.position.lng = 10;

      // this.center={ lat:10, lng: 20 }
    },

    editBio() {
      this.edit1 = !this.edit1;
    },
    /**
     * Used to edit contact info
     * @return void
     */
    editContact() {
      (this.form = this.business_intro), (this.edit2 = !this.edit2);
    },

    /**
     *
     * @param idForm
     */
 //   validate(idForm) {
 //     this.$bvModal.hide(idForm);
 //   }, 
  },

  computed: {
    business_intro() {
      return this.$store.state.businessOwner.businessInfo;
    },
  },

  mounted() {
    this.setcoordintes();
    this.url = this.$route.params.id;
  },
};
</script>

<style scoped>
@media (max-width: 768px) {
  .primary {
    margin-right: 6px;
    font-size: 12px !important;
  }

  .card-text {
    font-size: 14px !important;
  }
}

@media (min-width: 768px) {
  .primary {
    margin-right: 8px;
    font-size: 14px !important;
  }

  .card-text {
    font-size: 14px !important;
  }
}
</style>

<style>
.icon-size {
  width: 24px;
  height: 24px;
}
</style>
