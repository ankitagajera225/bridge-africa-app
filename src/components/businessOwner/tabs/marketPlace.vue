<template>
  <div>
    <div class="products ">
      <div class="col-md-6" v-for="(product, index) in products" :key="index">
        <Product :product="product" />
      </div>
      <b-col v-if="loader" class="load">
        <b-spinner
          style="width: 7rem; height: 7rem;"
          variant="primary"
        ></b-spinner>
      </b-col>
      <b-col v-if="products.lentgh < 1 && !loader" class="load">
        <p>No notifications to show !!</p>
      </b-col>
    </div>

    <b-modal hide-footer title="Add product" v-model="showModal">
      <b-form>
        <b-row>
          <b-col cols="12" md="6">
            <b-form-group
              id="input-group-1"
              label="Product Name"
              label-for="input-1"
              label-size="sm"
            >
              <b-form-input
                id="input-1"
                class="mt-1"
                type="text"
                v-model="newProduct.name"
                required
              ></b-form-input>
            </b-form-group>

            <b-form-group
              id="input-group-1"
              label="Product Description"
              label-for="input-1"
              label-size="sm"
            >
              <b-textarea
                id="input-1"
                class="mt-2"
                v-model="newProduct.description"
                type="text"
                required
              ></b-textarea>
            </b-form-group>
          </b-col>
          <b-col cols="12" md="6">
            <div class="image-upload-wrap" @click="picImage">
              <input
                type="file"
                name=""
                @change="getImage"
                accept="image/*"
                id="image"
                v-show="false"
              />
              <a href="#" data-toggle="modal" data-target="#createalbumModal">
                <div class="drag-text">
                  <i class="fa fa-plus"></i>
                  <h6>Product Image</h6>
                </div>
              </a>
              <div></div>
            </div>
          </b-col>
        </b-row>

        <b-form-group
          id="input-group-1"
          label="Product Description"
          label-for="input-1"
          label-size="sm"
        >
          <b-form-input
            v-model="newProduct.price"
            class="mt-1"
            id="price"
          ></b-form-input>
        </b-form-group>

        <b-form-checkbox
          value="1"
          v-model="newProduct.on_discount"
          unchecked-value="0"
        >
          <b-form-input class="mt-1" id="price"></b-form-input>
        </b-form-checkbox>

        <b-form-checkbox
          id="checkbox-1"
          name="checkbox-1"
          value="accepted"
          unchecked-value="not_accepted"
        >
          This Product Is On Discount
        </b-form-checkbox>

        <b-form-group
          id="conditions"
          label="Conditions"
          label-for="input-1"
          label-size="sm"
        >
          <b-form-input
            v-model="newProduct.condition"
            class="mt-1"
            id="conditions"
          ></b-form-input>
        </b-form-group>

        <b-form-checkbox
          value="1"
          v-model="newProduct.is_service"
          unchecked-value="0"
        >
          This Item Is A Service ?
        </b-form-checkbox>

        <b-form-checkbox
          value="1"
          v-model="newProduct.in_stock"
          unchecked-value="0"
        >
          In stock
        </b-form-checkbox>

        <b-form-checkbox value="1" unchecked-value="0">
          Published
        </b-form-checkbox>
        <b-alert v-if="success" :variant="val" show> {{ msg }} </b-alert>
        <b-button @click="addProduct" class="mt-2 btn-block" variant="primary">
          <b-spinner v-if="load" variant="white"></b-spinner>

          Add</b-button
        >
      </b-form>
    </b-modal>
  </div>
</template>

<script>
import Product from "../product";
import axios from "axios";
export default {
  data() {
    return {
      showModal: false,
      load: false,
      loader: false,
      newProduct: {
        name: "",
        description: "",
        picture: "",
        price: "",
        in_stock: "",
        on_discount: null,
        discount_price: "",
        condition: "",
        is_service: null,
      },
      products: [],
      val: "",
      msg: "",
      success: false,
    };
  },
  components: {
    Product,
  },
  beforeMount() {
    this.loader = true;
    axios.defaults.headers.common["Authorization"] =
      "Bearer " + localStorage.getItem("access_token");
    this.getProducts();
  },
  methods: {
    getProducts() {
      axios.get("/api/v1/market").then((res) => {
        this.products = res.data.data.data;
      });
    },
    addProduct() {
      this.load = true;
      let fd = new FormData();
      fd.append("name", this.newProduct.name);
      fd.append("description", this.newProduct.description);
      fd.append("picture", this.newProduct.picture);
      fd.append("price", this.newProduct.price);
      fd.append("in_stock", this.newProduct.in_stock);
      fd.append("on_discount", this.newProduct.on_discount);
      fd.append("discount_price", this.newProduct.discount_price);
      fd.append("condition", this.newProduct.condition);
      fd.append("is_service", this.newProduct.is_service);

      axios
        .post("market", fd)
        .then((res) => {
          this.load = false;
          (this.success = true), (this.val = "success");
          this.msg = "Operation was successful !!";
          this.getProducts();
        })
        .catch((err) => {
          this.load = false;
          (this.success = true), (this.val = "danger");
          this.msg = "Something wen't wrong !!";

          setTimeout(() => {
            this.success = false;
          }, 5000);
        });
    },
    picImage() {
      document.querySelector("#image").click();
    },
    getImage(e) {
      this.newProduct.picture = e.target.files[0];
    },
    createProduct() {
      this.showModal = !this.showModal;
    },
  },
};
</script>

<style scoped>
.load {
  display: flex;
  justify-content: center;
}
.products {
  display: flex;
  flex-wrap: wrap;
}

.product:hover .overlay {
  opacity: 0.5;
  color: #e75d29;
}
.text-hover {
  position: relative;
  top: 80px;
}

.text-static {
  position: relative;
  top: -220px;
  left: 100px;
  color: white;
  font-weight: 200;
}

.product:hover .text-static {
  display: none;
}

.btn-view {
  background-color: transparent;
  border: none;
  color: white;
}

.btn-view:focus {
  outline-color: transparent;
  border: none;
}

.product-name {
  color: #e75d29;
  text-align: center;
}

.pic-name {
  position: relative;
  left: -200px;
  color: white;
  font-weight: 200;
  opacity: 0;
}

.sp:hover .pic-name {
  opacity: 1;
}

.pic {
  cursor: pointer;
  background-color: transparent;
}
.pic:hover {
  box-shadow: 5px 10px 8px 2px #888888;
}

.create {
  position: relative;
  height: 210px;
  color: #fff;
  background-color: #bbb;
  padding: 20px;
  width: 14rem;
  top: 5px;
  left: 10px;
  border-radius: 5px;
  text-align: center;
  cursor: pointer;
  margin-bottom: 10px;
}

.text {
  margin-top: 50px;
}

.product {
  height: 190px;
  cursor: pointer;
}

@media only screen and (max-width: 768px) {
  .products {
    position: relative;
  }

  .product {
    margin-top: 20px;
  }

  .create {
    position: relative;
    height: 150px;
    left: 23px;
  }
  .text {
    margin-top: 30px;
  }
  .btn {
    font-size: 12px;
  }
}
</style>
