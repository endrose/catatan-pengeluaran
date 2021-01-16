<template>
  <Title title="Catatan Pengeluaran" />
  <FormPengeluaran @entry-pengeluaran="entryPengeluaran($event)" />
  <h2>Total Pengeluaran : {{ totalPengeluaran }}</h2>
  <h2 v-if="warning" class="warning">Pengeluaran Anda Terlalu Banyak</h2>
  <ListPengeluaran v-if="showList" :dataPengeluaran="dataPengeluaran" />
  <div v-else>Bagus kamu menghemat uang! untuk pengeluaran lain.</div>
</template>

<script>
import Title from "./components/Title.vue";
import ListPengeluaran from "./components/ListPengeluaran.vue";
import FormPengeluaran from "./components/FormPengeluaran.vue";

export default {
  name: "App",
  components: {
    Title,
    ListPengeluaran,
    FormPengeluaran,
  },
  data() {
    return {
      warning:true,
      dataPengeluaran: [
        {
          nominal: 20000,
          keterangan: "Makan Siang",
        },
        {
          nominal: 25000,
          keterangan: "Beli Pulsa",
        },
        {
          nominal: 15000,
          keterangan: "Beli Bensin",
        },
      ],
    };
  },

  methods: {
   entryPengeluaran(event){

     this.dataPengeluaran.push(event);
   }
  },
  computed: {
    showList: function() {
      return this.dataPengeluaran.length > 0;
    },
    totalPengeluaran:function(){
      return this.dataPengeluaran.reduce((acc, item) => acc + parseInt(item.nominal),0);
    }
  },
  watch:{
    totalPengeluaran:function(val){
      if(val > 100000){
          this.warning= true
      }
    }
  }
};
</script>

<style scoped></style>
