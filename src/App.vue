<template>
  <div>
    <div class="relative">
      <button class="fixed" @click="scrollToBottom()">Bottom</button>
    </div>
    <header class="mb-4 sticky-top">
      <nav class="position-relative">
        <img src="./assets/download.jpeg" alt="" width="70" />
        <h3
          class="position-absolute top-50 start-50 translate-middle text-center"
        >
          TECHBODIA Web Developer Coding Assignment
        </h3>
      </nav>
      <div class="pt-2 bg-white container">
        <div class="input-group mb-2">
          <span class="input-group-text" id="basic-addon2">Search</span>
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
              @click="sortData(true)"
              checked
            />
            <label class="form-check-label" for="az"> A-Z </label>
          </div>
          <div class="form-check">
            <input
              class="form-check-input"
              type="radio"
              name="flexRadioDefault"
              id="za"
              @click="sortData(false)"
            />
            <label class="form-check-label" for="za"> Z-A </label>
          </div>
        </div>
      </div>
    </header>
    <main class="container">
      <CatalogItems :data="data" id="results" />
    </main>
    <div
      id="pagination"
      class="d-flex justify-content-center gap-1 w-50 mx-auto my-4"
    >
      <a
        v-for="page in totalPages"
        :key="page"
        :class="{ active: page === currentPage }"
        @click="changePage(page)"
        class="d-flex justify-content-center align-items-center pointer hover-bg-info text-[#ff007a]"
      >
        {{ page }}
      </a>
    </div>
    <div ref="bottomElement"></div>
  </div>
</template>
<script>
import CatalogItems from "./components/CatalogItems.vue";
export default {
  components: {
    CatalogItems,
  },
  data() {
    return {
      API: "https://restcountries.com/v3.1/all",
      data: [],
      allData: [],
      checked: true,
      search: "",
      dataPerPage: 25,
      currentPage: 1,
      totalPages: 0,
    };
  },
  methods: {
    sortData(checked) {
      this.checked = checked;
      if (checked) {
        // Sort in ascending order
        this.data = this.data.sort((a, b) =>
          a.name.official.localeCompare(b.name.official)
        );
      } else {
        // Sort in desc
        this.data = this.data.sort((a, b) =>
          b.name.official.localeCompare(a.name.official)
        );
      }
    },
    SearchByCountryName(query) {
      if (query) {
        this.data = [
          ...this.allData.filter((item) =>
            item.name.official.toLowerCase().includes(query.toLowerCase())
          ),
        ];
      } else {
        this.listFlagsHandler();
      }
    },

    // Function to show data for the current page
    dataCurrentPages() {
      const start = (this.currentPage - 1) * this.dataPerPage;
      const end = start + this.dataPerPage;
      this.data = [...this.allData.slice(start, end)];
      this.sortData(this.checked);
    },

    listFlagsHandler() {
      fetch(this.API)
        .then((res) => res.json())
        .then((data) => {
          this.allData = [...data];
          // this.data = [...this.allData];
          this.sortData(this.checked);
          this.getTotalPage();
          this.dataCurrentPages();
        });
    },
    changePage(page) {
      this.currentPage = page;
      this.dataCurrentPages();
    },
    getTotalPage() {
      this.totalPages = Math.ceil(this.allData.length / this.dataPerPage);
    },
    scrollToBottom() {
      const bottomElement = this.$refs.bottomElement;
      bottomElement.scrollIntoView({ behavior: "smooth" });
    },
  },
  mounted() {
    this.listFlagsHandler();
  },
};
</script>
<style scoped>
nav {
  background: #282828;
}
h3 {
  color: #ff007a;
}
.vertical-line {
  border-left: 2px solid black;
  height: 100px; /* Adjust the height as needed */
}
#pagination a {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  cursor: pointer;
  color: #282828;
  text-decoration: none;
}
#pagination a:hover:not(.active) {
  background: #ff007b9d;
  color: #fff;
}
#pagination .active {
  background: #ff007a;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  color: #fff;
}
.relative {
  position: relative;
}
.relative .fixed {
  position: fixed;
  bottom: 0;
  right: 0;
  margin: 10px;
  background: #ff007a;
  border: none;
  outline: none;
  color: #fff;
  border-radius: 5px;
}
</style>
