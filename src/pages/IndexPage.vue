<template>
  <q-page>
    <div class="q-pa-md" style="max-width: 400px">
      <h6>Customer Form</h6>
      <q-form @submit.prevent="onSubmit" @reset="onReset" class="q-gutter-md" ref="myfrm">
        <q-input
          filled
          v-model="name"
          label="Your name *"
          hint="Name and surname"
          lazy-rules
          :rules="[(val) => (val && val.length > 0) || 'Please type something']"
        />

        <q-input
          filled
          type="number"
          v-model="age"
          label="Your age *"
          hint="Allow only number"
          lazy-rules
          :rules="[
            (val) => (val !== null && val !== '') || 'Please type your age',
            (val) => (val > 0 && val < 81) || 'Please type a real age between 1-80',
          ]"
        />

        <div>
          <q-btn label="ADD" type="submit" color="primary" />
          <q-btn
            label="Reset"
            type="reset"
            color="primary"
            flat
            class="q-ml-sm"
          />
        </div>
      </q-form>
      <br>
      <q-table
        title="Customer Details"
        :rows="rows"
        :columns="columns"
        row-key="name"
      />
    </div>
   
  </q-page>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
    name: "IndexPage",
    data() {
        return {
            name: null,
            age: null,
            columns: [
                { name: "id", label: "ID", field: "id", align: "center" },
                { name: "name", label: "Name", field: "name", align: "left" },
                { name: "age", label: "Age", field: "age", align: "right" }
            ],
            rows: [],
            id: 0
        };
    },
    methods: {
        onSubmit() {
            this.id++;
            this.rows.push({
                id: this.id,
                name: this.name,
                age: this.age
            });
            this.$refs.myfrm.reset();
        },
        onReset() {
            this.name = null;
            this.age = null;
        }
    },

});
</script>
