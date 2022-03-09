<template>
  <div id="app">
    <TheHeader />
    <div class="container">
      <h1 class="main_title">Airlines</h1>
      <div class="filter">
        <p>Filter by Alliances</p>
        <div class="checkboxes">
          <label :for="filter.id" v-for="filter in filters" :key="filter.name">
            <input
              type="checkbox"
              :id="filter.id"
              :value="filter.id"
              v-model="selectFilter"
            />
            {{ filter.name }}
          </label>
        </div>
      </div>
      <div class="row">
        <TheCard
          v-for="company in filterCompany"
          :key="company.id"
          :name="company.name"
          :img="company.logoURL"
          :alliance="company.alliance"
          :phone="company.phone"
          :website="company.site"
        />
      </div>
    </div>
  </div>
</template>

<script>
import TheHeader from "./components/TheHeader.vue";
import TheCard from "./components/TheCard.vue";
import jsonp from "jsonp";

export default {
  name: "App",
  data() {
    return {
      companies: [],
      selectFilter: [],
      filters: [
        {
          id: "OW",
          name: "Oneworld",
        },
        {
          id: "ST",
          name: "Sky Team",
        },
        {
          id: "SA",
          name: "Star Alliance",
        },
      ],
    };
  },
  components: {
    TheHeader,
    TheCard,
  },
  methods: {
    filterAlliance(value) {
      this.selectFilter = value;
    },
  },
  computed: {
    filterCompany() {
      if (this.selectFilter.length === 0) {
        return this.companies;
      } else {
        let filterCompany = this.companies.filter((company) => {
          return this.selectFilter.includes(company.alliance);
        });
        return filterCompany;
      }
    },
  },
  mounted() {
    jsonp(
      "https://www.kayak.com/h/mobileapis/directory/airlines/homework",
      { param: "jsonp" },
      (err, data) => {
        if (err) {
          console.error(err.message);
        } else {
          this.companies = data;
        }
      }
    );
  },
};
</script>

<style lang="scss">
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #192024;
  background-color: #f9fafb;
  .container {
    width: 90%;
    margin: auto;
    .main_title {
      font-size: 44px;
      color: black;
      margin: 70px 0;
    }
    .filter {
      p {
        font-size: 16px;
        font-weight: bold;
        margin-bottom: 22px;
      }
      .checkboxes {
        display: flex;
        margin-bottom: 56px;
        label {
          display: flex;
          align-items: center;
          font-size: 14px;
          margin-right: 24px;
          input {
            width: 20px;
            height: 20px;
            margin-right: 10px;
          }
        }
      }
    }
    .row {
      display: flex;
      flex-wrap: wrap;
      column-gap: 16px;
    }
  }
}
</style>
