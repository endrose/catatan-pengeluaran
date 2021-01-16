<template>
  <form class="form-pengeluaran" @submit.prevent="catat" >
    <div>
      <label for="pengeluaran">Pengeluaran</label>
      <input v-model="pengeluaran" type="number" id="pengeluaran">
    </div>
    <div>
        <label for="keterangan">Keterangan</label>
        <input v-model="keterangan" type="text" id="keterangan">
    </div>
    <div>
      <button>Catat!</button>
    </div>
  </form>
</template>

<script>
export default {
  name:"FormPengeluaran",
  data(){
   return{
      pengeluaran: null,
      keterangan: null
   }
  },
  mounted(){

  },
  methods:{
    catat(){
      // emit child to parent
      this.$emit('entry-pengeluaran', {
        nominal: this.pengeluaran,
        keterangan: this.keterangan
      });

     
      this.pengeluaran=null
      this.keterangan=null

      document.getElementById("pengeluaran").focus()

    }
  }
}
</script>

<style scoped>
  .form-pengeluaran{
      padding: 20px;
      display: flex;
      flex-flow: nowrap;
      align-items: center;
      justify-content: center;
  }

  .form-pengeluaran label{
    margin: 5px 10px 5px 0;
  }

  .form-pengeluaran input{
    vertical-align: middle;
    margin: 5px 10px 5px 0;
    padding: 10px;
    background-color: #ffff;
    border: 1px solid #ddd;
  }

  .form-pengeluaran button:hover{
    background-color: white;
    color: blueviolet;
    outline: none;
    border: 1px solid blueviolet;
  }

  .form-pengeluaran button{
    padding: 10px 20px;
    background-color: blueviolet;
    border-radius: 10px;
    color: white;
    border: 1px solid blueviolet;
    cursor: pointer;
  }
</style>