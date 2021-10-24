<template>
  <div class="food-detail">
    <Navbar />
    <div class="container">
      <BreadCrumb title="Food Detail" />
      <div class="row mt-2">
        <div class="col-md-6 mt-4">
          <img
            :src="'../assets/images/' + product.gambar"
            class="img-fluid shadow"
            alt="..."
          />
        </div>
        <div class="col-md-6">
          <h2>
            <strong>{{ product.nama }}</strong>
          </h2>
          <hr />
          <h4>
            Harga : <strong>Rp. {{ product.harga }}</strong>
          </h4>
          <form class="mt-4" @submit.prevent>
            <div class="form-group">
              <label for="jumlah_pesanan">Jumlah Pesanan</label>
              <input
                type="number"
                class="form-control"
                v-model="pesan.jumlah_pemesanan"
              />
            </div>

            <div class="form-group">
              <label for="keterangan">Keterangan</label>
              <textarea
                v-model="pesan.keterangan"
                class="form-control"
                placeholder="Keterangan : pedes, nasi setengah dll.."
              ></textarea>
            </div>

            <button type="submit" class="btn btn-success" @click="pemesanan">
              <b-icon-cart></b-icon-cart> Pesan
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import BreadCrumb from "@/components/BreadCrumb.vue";
import axios from "axios";

export default {
  name: "FoodDetail",
  components: {
    Navbar,
    BreadCrumb,
  },
  data() {
    return {
      product: [],
      pesan: {},
    };
  },
  methods: {
    setProduct(data) {
      this.product = data;
    },
    pemesanan() {
      if ( this.pesan.jumlah_pemesanan ) {
        this.pesan.products = this.product;
        axios
          .post("http://localhost:3000/keranjangs", this.pesan)
          .then(() => {
            this.$router.push({ path: "/keranjang" }),
              this.$toast.success("Pesanan Sukses masuk keranjang.", {
                type: "success",
                position: "top",
                duration: 1000,
                dismissible: true,
              });
          })
          .catch((err) => console.log(err));
      } else {
        this.$toast.error("Jumlah Pesanan Wajib di isi.", {
          type: "error",
          position: "top",
          duration: 1000,
          dismissible: true,
        });
      }
    },
  },
  mounted() {
    console.log(this.$route.params.id);
    axios
      .get("http://localhost:3000/products/" + this.$route.params.id)
      .then((response) => this.setProduct(response.data))
      .catch((error) => console.log(error));
  },
};
</script>

<style>
</style>