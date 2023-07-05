<script setup>
import { ref } from "vue";
import { onMounted } from "vue";
import axios from "axios";

const nume = ref("");
const prenume = ref("");
const dataDeNastere = ref("");
const comentariu = ref("");

onMounted(() => {
  console.log("Component mounted.");
});

async function formSubmit() {

  let currentObj = this;

  axios
    .post("http://laravel.test/forms", {
      nume: nume.value,
      prenume: prenume.value,
      data_de_nastere: dataDeNastere.value,
      comentariu: comentariu.value,
    })
    .then(function (response) {
      currentObj.output = response.data;
    })
    .catch(function (error) {
      currentObj.output = error;
    });

    console.log("in functia de trimitere");
}
</script>

<template>
  <div class="container-fluid">
    <div class="row justify-content-center">
      <div class="col-md-8 mt-3">
        <div class="card">
          <div class="card-header">Formular</div>

          <div class="card-body">
            <div>
              <strong>Nume:</strong>
              <input type="text" class="form-control" v-model="nume" />
              <br>
              <strong>Prenume:</strong>
              <input type="text" class="form-control" v-model="prenume" />
              <br>
              <strong>Data de naștere:</strong>
              <input type="date" class="form-control" v-model="dataDeNastere" />
              <br>
              <strong>Comentariu:</strong>
              <input type="text" class="form-control" v-model="comentariu" />
              <br>

              <button class="btn btn-success" @click="formSubmit()">Trimite</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
