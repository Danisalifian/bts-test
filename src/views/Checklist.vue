<template>
  <section>
    <div class="container ">
      <b-field label="Checklist Name">
        <b-input v-model="data.name"></b-input>
      </b-field>
      <b-button type="is-primary" @click="saveChecklist"
        >Save Checklist</b-button
      >
      <hr />
      <h1 class="title is-3">Checklist</h1>

      <div class="card" v-for="checklist in checklistArray" :key="checklist.id">
        <header class="card-header">
          <p class="card-header-title">
            {{ checklist.name }}
          </p>
          <a href="#" class="card-header-icon" aria-label="more options">
            <span class="icon">
              <i class="fas fa-angle-down" aria-hidden="true"></i>
            </span>
          </a>
        </header>
        <div class="card-content">
          <b-field label="Item">
            <b-input v-model="itemName"></b-input>
          </b-field>
          <b-button type="is-primary" @click="saveItem(checklist.id)"
            >Save Item</b-button
          >
          <div class="content">
            <li
              v-for="item in checklist.items"
              :key="item.id"
              style="text-align:left"
            >
              {{ item.name }}
              <span>
                <b-button
                  type="is-danger"
                  icon-right="delete"
                  @click="deleteItem(item.id)"
                />
              </span>
            </li>
          </div>
        </div>
        <footer class="card-footer">
          <a
            href="#"
            class="card-footer-item is-danger"
            @click="deleteChecklist(checklist.id)"
            >Delete</a
          >
        </footer>
      </div>
      <hr />
    </div>
  </section>
</template>

<script>
import Axios from "axios";
const config = {
  headers: {
    Authorization: `Bearer ${$cookies.get("user_session")}`,
  },
};
export default {
  name: "Checklist",
  data() {
    return {
      data: {
        name: "",
      },
      checklistArray: [],
      itemName: "",
    };
  },
  methods: {
    getChecklist() {
      Axios.get("http://18.139.50.74:8080/checklist", config).then((res) => {
        this.checklistArray = res.data.data;
      });
    },

    saveChecklist() {
      Axios.post("http://18.139.50.74:8080/checklist", this.data, config).then(
        (res) => {
          this.$buefy.toast.open({
            message: res.data.message,
            type: "is-success",
          });
        }
      );
    },

    deleteChecklist(id) {
      Axios.delete(`http://18.139.50.74:8080/checklist/${id}`, config).then(
        (res) => {
          this.$buefy.toast.open({
            message: res.data.message,
            type: "is-success",
          });
        }
      );
    },

    saveItem(id) {
      let data = {
        checklistId: id,
        itemName: this.itemName,
      };
      Axios.post("http://18.139.50.74:8080/item", data, config).then((res) => {
        this.$buefy.toast.open({
          message: res.data.message,
          type: "is-success",
        });
      });
    },

    deleteItem(id) {
      Axios.delete(`http://18.139.50.74:8080/item/${id}`, config).then(
        (res) => {
          this.$buefy.toast.open({
            message: res.data.message,
            type: "is-success",
          });
        }
      );
    },
  },
  mounted() {
    this.getChecklist();
  },
};
</script>

<style>
.is-danger {
  font-weight: bolder;
  background: red;
  color: white;
}
.card {
  border: 1px solid black;
  margin: 10px 0;
}
.card-header {
  border-bottom: 1px solid black;
}
</style>
