<template>
  <div class="container mt-4">
    <div class="row">

      <form  method="post">
        <div class="row">
          <div class="col-4">
            <div class="form-group">
              <label for="gorevad" class="form-label mt-4">Görev Adı</label>
              <input type="text" class="form-control" id="gorevad"  placeholder="Görev Adı" v-model="gorevData.gorevad">
            </div>
          </div>
          <div class="col-4">
            <div class="form-group">
              <label for="görevacikla" class="form-label mt-4">Görev Açıklması</label>
              <input type="text" class="form-control" id="görevacikla"  placeholder="Görev Açıklması" v-model="gorevData.gorevacikla">
            </div>
          </div>
          <div class="col-4 mt-6">
            <div class="d-grid gap-2">
              <button class="btn  btn-info" type="button" @click="onSave">+EKLE</button>
            </div>
          </div>
        </div>
      </form>
    </div>

  </div>




  <div class="container">
    <div class="row mt-5">
      <div class="col-4">
        <div class="card border-primary mb-3" style="max-width: 20rem;">
          <div class="card-header bg-primary text-center">YAPILACAKLAR</div>
          <div class="card-body">



            <div class="card bg-light mb-3" style="max-width: 20rem;" v-for="item in gorevList" v-bind:key="item.id">

              <div class="row">
                <div class="col-6">
                  <div class="card-header">{{ item.gorevad}}</div>
                </div>
                <div class="col-6 mt-1 float-end">
                  <button type="button" class="btn btn-danger btn-sm me-2" @click="deleteGorev(item.id)">
                    Sil
                  </button>
                  <button type="button" class="btn btn-info btn-sm ">
                    Başla
                  </button>
                </div>
              </div>
              <div class="card-body">
                <p class="card-text" >{{ item.gorevacikla}}</p>
              </div>
            </div>


          </div>
        </div>
      </div>
      <div class="col-4">
        <div class="card border-primary mb-3" style="max-width: 20rem;">
          <div class="card-header bg-success text-center">YAPILAN</div>
          <div class="card-body">


          </div>
        </div>
      </div>
      <div class="col-4">
        <div class="card border-primary mb-3" style="max-width: 20rem;">
          <div class="card-header bg-warning text-center">YAPILANLAR</div>
          <div class="card-body">


          </div>
        </div>
      </div>

    </div>

  </div>


</template>

<script>
import {appAxios} from "@/utils/appAxios";
export default {


  data(){
    return{
      gorevData : {
        gorevad : null,
        gorevacikla : null,
      },
      gorevDataYap:{
        gorevadyap:null,
        gorevaciklayap:null ,
      },

      gorevList : undefined,
      gorevListYap :undefined,
    }
  },
  methods:{
    onSave(){
      appAxios.post("/gorevs",this.gorevData).then(kayit_response => {
        console.log("kayit_response :>> ",kayit_response);
      })
      console.log(this.gorevData)
    },


    getGorevs(){
      appAxios.get("/gorevs")
      .then((getir_response) => {
        this.gorevList=getir_response.data
        console.log(getir_response.data)
      })
      .catch((error) =>{
        console.log(error)
      })
    },
    deleteGorev(id){
      appAxios.delete("/gorevs/"+id).then(() => {
        this.getGorevs();
      })
    }
  },

  mounted() {
    this.getGorevs()
  }


}
</script>

<style>

</style>
