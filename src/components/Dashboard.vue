<template>
  <div id="dashboard">
    <h3>dashboard </h3>
    <ul class="collection with-header">
      <li class="collection-header">
        <h4>Avengers</h4>
      </li>
      <li v-for="employee in employees" v-bind:key="employee.id" class="collection-item">
        {{employee.employee_id}}{{employee.name}}
        <div class="chip">{{employee.position}}</div>
        <router-link class="secondary-content" v-bind:to="{name:'view-employee',params:{employee_id:employee.employee_id}}">
            <i class="fa fa-eye">view</i>
        </router-link>
      </li>
    </ul>
    <div class="fixed-action-btn">
      <router-link to="/new" class="btn-floating btn-large red">
        <i class="fa fa-plus">+</i>
      </router-link>
    </div>
  </div>
</template>
<script>
  import db from "./firebaseInit";
  // import { QuerySnapshot } from '@firebase/firestore-types';
  export default {
    name: "dashboard",
    data() {
      return {
        employees: []
      };
    },

    created() {
      db
        .collection("employees")
        .orderBy("name")
        .get()
        .then(querySnapshot => {
          querySnapshot.forEach(doc => {
            console.log(doc.data());
            const data = {
              id: doc.id,
              name: doc.data().name,
              power: doc.data().power,
              employee_id: doc.data().employee_id,
              position: doc.data().position
            };
            this.employees.push(data);
            //   console.log(this.employees)
          });
        });
    }
  };

</script>
<style>


</style>