<template>
  <div>
    <header class="position-relative p-1 mb-4 position-sticky z-1 top-0">
      <img src="./assets/download.jpeg" alt="" width="70" />
      <h3
        class="position-absolute top-50 start-50 translate-middle text-center"
      >
        TECHBODIA Web Developer Coding Assignment
      </h3>
    </header>
    <main class="container">
      <SearchFlagItems />

      <div class="mb-2">
        <div class="col-4">
          <input
            class="form-control"
            type="search"
            v-model="search"
            @keyup="SearchByCountryName(search)"
            placeholder="Search For Country Name..."
            aria-label="Recipient's username"
            aria-describedby="basic-addon2"
          />
        </div>
        <div class="sort">
          Sorting by:
          <div class="form-check">
            <input
              class="form-check-input"
              type="radio"
              name="flexRadioDefault"
              id="az"
              v-model="checked"
              @click="sortData(checked)"
              :value="checked"
            />
            <label class="form-check-label" for="az"> A-Z </label>
          </div>
          <div class="form-check">
            <input
              class="form-check-input"
              type="radio"
              name="flexRadioDefault"
              id="za"
              :value="false"
              @click="sortData(false)"
            />
            <label class="form-check-label" for="za"> Z-A </label>
          </div>
        </div>
      </div>
      <CatalogItems :data="data" />
    </main>
  </div>
</template>
<script>
import SearchFlagItems from "./components/SearchFlagItems.vue";
import CatalogItems from "./components/CatalogItems.vue";
export default {
  components: {
    CatalogItems,
    SearchFlagItems,
  },
  data() {
    return {
      API: "https://restcountries.com/v3.1/all",
      data: [],
      checked: true,
      search: "",
    };
  },
  methods: {
    sortData(checked) {
      if (checked) {
        // Sort in ascending order
        this.data = this.data.sort((a, b) =>
          a.name.official.localeCompare(b.name.official)
        );
      } else {
        this.data = this.data.sort((a, b) =>
          b.name.official.localeCompare(a.name.official)
        );
      }
    },
    SearchByCountryName(query) {
      if (query) {
        this.data  = this.data.filter((item) =>
          item.name.official.toLowerCase().includes(query.toLowerCase())
        );
      } else {
        this.listFlagsHandler();

      }
    },
    listFlagsHandler() {
      fetch(this.API)
        .then((res) => res.json())
        .then((data) => {
          this.data = data;
          this.sortData(this.checked);
        });
    },
  },
  mounted() {
    this.listFlagsHandler();
  },
};
</script>
<style scoped>
header {
  background: #282828;
}
h3 {
  color: #ff007a;
}
.vertical-line {
  border-left: 2px solid black;
  height: 100px; /* Adjust the height as needed */
}
</style>
