<template lang ="html">
  <div  class="container">
    <div  class="row">
      <div class="col text-left">
        <h2>Editar Artículo</h2>
      </div>
    </div>
    <div class="row">
        <div class="col">
          <div class="card">
              <div class="card-body">

                <form @submit="onSubmit">
                   <div class="form-group row">
                     <label for="title" class="col-sm-2 col-form-label">
                      Título
                     </label>
                       <div class="col-sm-5">
                          <input type="text" placeholder="Título" name="title" class="form-control" v-model.trim="form.title"> </input>
                       </div>
                   </div>
                   <div class="form-group row">
                     <label for="title" class="col-sm-2 col-form-label">
                      Autor
                     </label>
                       <div class="col-sm-5">
                          <input type="text" placeholder="Autor" name="author" class="form-control" v-model.trim="form.author"> </input>
                       </div>
                   </div>
                   <div class="form-group row">
                     <label for="title" class="col-sm-2 col-form-label">
                      Descripción
                     </label>
                       <div class="col-sm-6">
                          <textarea name="description" class="form-control" placeholder="Descripción" rows="4" v-model.trim="form.description"> </textarea>
                       </div>
                   </div>

                   <div class="rows">
                      <div class="col text-left">
                        <b-button type="submit" variant="primary"> Editar </b-button>
                        <b-button type="submit" class="btn-large-space" :to="{name: 'listArticulo' }"> Cancelar </b-button>
                      </div>

                   </div>

                </form>

              </div>

          </div>

        </div>
     </div>
  </div>
</template>

<script>
import axios from 'axios'
import swal from 'sweetalert'
export default {
  data (){
    return {
      articuloId: this.$route.params.articuloId,
        form: {
          title: '',
          author: '',
          description:''
        }
    }
  },
  methods :{
    onSubmit(evt){
      evt.preventDefault()
      const path = `http://127.0.0.1:8000/api/v1.0/articulos/${this.articuloId}/`
      axios.put(path, this.form).then((response) => {

        this.form.title= response.data.title
        this.form.author= response.data.author
        this.form.description= response.data.description
        swal("Artículo actualizado correctamente", "", "exito")
      })
      .catch ((error) =>{
        console.log(error)
      })



    },

    getArticulo (){
      const path = `http://127.0.0.1:8000/api/v1.0/articulos/${this.articuloId}/`
      axios.get(path).then((response) => {

        this.form.title= response.data.title
        this.form.author= response.data.author
        this.form.description= response.data.description

      })
      .catch ((error) =>{
        console.log(error)
      })

    }

  },
  created (){
    this.getArticulo()
  }

}
</script>

<style lang="css" scoped>

</style>
