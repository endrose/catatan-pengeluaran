<template>
  <Title title="Catatan Pengeluaran" />
  <FormPengeluaran @entry-pengeluaran="entryPengeluaran($event)" />
  <h2 class="t-pengeluaran">Total Pengeluaran : {{ totalPengeluaran }}</h2>
  <h2 v-if="warning" class="warning">Pengeluaran Anda Terlalu Banyak</h2>
  <ListPengeluaran v-if="showList" :dataPengeluaran="dataPengeluaran" />
  <div v-else>Bagus kamu menghemat uang! untuk pengeluaran lain.</div>
</template>

<script>
import Title from "./components/Title.vue";
import ListPengeluaran from "./components/ListPengeluaran.vue";
import FormPengeluaran from "./components/FormPengeluaran.vue";
import {ref, computed, watch} from "vue";
export default {
  name: "App",
  components: {
    Title,
    ListPengeluaran,
    FormPengeluaran,
  },
  // COMPOSITON API
  setup(){
    const warning = ref(false);
    const dataPengeluaran = ref([]);
    const showList = computed(()=> dataPengeluaran.value.length > 0)
    const totalPengeluaran = computed(() => dataPengeluaran.value.reduce((acc,item) => acc+parseInt(item.nominal),0))


    function entryPengeluaran(event){
      dataPengeluaran.value.push(event)
    }


    watch(totalPengeluaran, (newValue)=> {
      if(newValue > 100000){
        warning.value = true
      }
    });


    return {
      dataPengeluaran,
      showList,
      totalPengeluaran,
      entryPengeluaran,
      warning
    }
  }

  // OPTION API
  // data() {
  //   return {
  //     warning:true,
  //     dataPengeluaran: [
  //       // {
  //       //   nominal: 20000,
  //       //   keterangan: "Makan Siang",
  //       // },
  //       // {
  //       //   nominal: 25000,
  //       //   keterangan: "Beli Pulsa",
  //       // },
  //       // {
  //       //   nominal: 15000,
  //       //   keterangan: "Beli Bensin",
  //       // },
  //     ],
  //   };
  // },

  // methods: {
  //  entryPengeluaran(event){

  //    this.dataPengeluaran.push(event);
  //  }
  // },
  // computed: {
  //   // showList: function() {
  //   //   return this.dataPengeluaran.length > 0;
  //   // },
  //   // totalPengeluaran:function(){
  //   //   return this.dataPengeluaran.reduce((acc, item) => acc + parseInt(item.nominal),0);
  //   // }
  // },
  // watch:{
  //   totalPengeluaran:function(val){
  //     if(val > 100000){
  //         this.warning= true
  //     }
  //   }
  // }
};
</script>

<style scoped>
  .t-pengeluaran{
    text-align: center;
  }
</style>
