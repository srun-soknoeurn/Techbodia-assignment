<template>
  <div class="row row-cols-4 row-cols-md-3 g-4">
    <div class="col" v-for="flag in data" :key="flag">
      <div class="card h-100">
        <img :src="flag.flags.png" class="card-img-top h-75" alt="..." />
        <div class="card-body">
          <h5 class="card-title">{{ flag.name.official }}</h5>
          <ul>
            <li>{{ flag.cca2 }}</li>
            <li>{{ flag.cca3 }}</li>
            <li>{{ flag.name.nativeName }}</li>
            <li>{{ flag.altSpellings }}</li>
            <li class="p-0 m-0">
              <span>{{ flag.idd.root }}</span> 
              <span v-for="item in flag.idd.suffixes" :key="item">
                {{ item }}</span
              >
            </li>
          </ul>
        </div>
      </div>
    </div>
    <!-- <div class="col">
      <div class="card">
        <img src="..." class="card-img-top" alt="..." />
        <div class="card-body">
          <h5 class="card-title">Card title</h5>
          <p class="card-text">
            This is a longer card with supporting text below as a natural
            lead-in to additional content. This content is a little bit longer.
          </p>
        </div>
      </div>
    </div>
    <div class="col">
      <div class="card">
        <img src="..." class="card-img-top" alt="..." />
        <div class="card-body">
          <h5 class="card-title">Card title</h5>
          <p class="card-text">
            This is a longer card with supporting text below as a natural
            lead-in to additional content.
          </p>
        </div>
      </div>
    </div>
    <div class="col">
      <div class="card">
        <img src="..." class="card-img-top" alt="..." />
        <div class="card-body">
          <h5 class="card-title">Card title</h5>
          <p class="card-text">
            This is a longer card with supporting text below as a natural
            lead-in to additional content. This content is a little bit longer.
          </p>
        </div>
      </div>
    </div> -->
  </div>
</template>

<script>
export default {
  data() {
    return {
      API: "https://restcountries.com/v3.1/all",
      data: [],
    };
  },
  methods: {
    listFlagsHandler() {
      fetch(this.API)
        .then((res) => res.json())
        .then((data) => {
          this.data = data;
        });
    },
  },
  mounted() {
    this.listFlagsHandler();
  },
};
</script>

<style scoped></style>
