<template>
  <form class="form-pengeluaran" @submit.prevent="catat">
    <div>
      <label for="pengeluaran">Pengeluaran</label>
      <input v-model="state.pengeluaran" type="number" id="pengeluaran" />
    </div>
    <div>
      <label for="keterangan">Keterangan</label>
      <input v-model="state.keterangan" type="text" id="keterangan" />
    </div>
    <div>
      <button>Catat!</button>
    </div>
  </form>
</template>

<script>
// COMPOSITOION API
import { reactive } from "vue";
export default {
  name: "FormPengeluaran",
  setup(props, context) {
    const state = reactive({
      pengeluaran: null,
      keterangan: null,
    });

    function catat() {
      context.emit("entry-pengeluaran", {
        nominal: state.pengeluaran,
        keterangan: state.keterangan,
      });
      state.pengeluaran = null;
      state.keterangan = null;
      document.getElementById("pengeluaran").focus();
    }

    return {
      state,
      catat,
    };
  },
  // OPTION API

  // data(){
  //  return{
  //     pengeluaran: null,
  //     keterangan: null
  //  }
  // },

  // methods:{
  //   catat(){
  //     // emit child to parent
  //     this.$emit('entry-pengeluaran', {
  //       nominal: this.pengeluaran,
  //       keterangan: this.keterangan
  //     });

  //     this.pengeluaran=null
  //     this.keterangan=null

  //     document.getElementById("pengeluaran").focus()

  //   }
  // }
};
</script>

<style scoped>
.form-pengeluaran {
  padding: 20px;
  display: flex;
  flex-flow: nowrap;
  align-items: center;
  justify-content: center;
}

.form-pengeluaran label {
  margin: 5px 10px 5px 0;
}

.form-pengeluaran input {
  vertical-align: middle;
  margin: 5px 10px 5px 0;
  padding: 10px;
  background-color: #ffff;
  border: 1px solid #ddd;
}

.form-pengeluaran button:hover {
  background-color: white;
  color: blueviolet;
  outline: none;
  border: 1px solid blueviolet;
}

.form-pengeluaran button {
  padding: 10px 20px;
  background-color: blueviolet;
  border-radius: 10px;
  color: white;
  border: 1px solid blueviolet;
  cursor: pointer;
}
</style>
