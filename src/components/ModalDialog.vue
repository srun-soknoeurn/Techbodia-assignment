<template>
  <!-- Button trigger modal -->
  <button
    type="button"
    class="btn btn-primary"
    data-bs-toggle="modal"
    data-bs-target="#dialog"
    ref="showDialog"
    v-show="false"
  ></button>
  <!-- Modal -->
  <div
    class="modal fade"
    id="dialog"
    data-bs-backdrop="static"
    data-bs-keyboard="false"
    tabindex="-1"
    aria-labelledby="staticBackdropLabel"
    aria-hidden="true"
  >
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="staticBackdropLabel">
            {{ dataDetails.name ? dataDetails.name.official : "" }}
          </h5>
          <button
            type="button"
            class="btn-close"
            data-bs-dismiss="modal"
            aria-label="Close"
          ></button>
        </div>
        <div class="modal-body">
          <div class="card mb-3">
            <img
              :src="dataDetails.flags ? dataDetails.flags.png : ''"
              class="card-img-top"
              width="200"
              alt="..."
            />
            <div class="card-body">
              <ul>
                <li>
                  Country name:
                  {{ dataDetails.name ? dataDetails.name.official : "" }}
                </li>
                <li>Population: {{ dataDetails.population }}</li>
                <li>Area: {{ dataDetails.area }}</li>
                <li>Area: {{ dataDetails.area }}</li>
                <li>Region: {{ dataDetails.region }}</li>
                <li>Subregion: {{ dataDetails.subregion }}</li>
                <li>Languages: {{ dataDetails.languages }}</li>
                <li>CCA2: {{ dataDetails.cca2 }}</li>
                <li>CCN3: {{ dataDetails.ccn3 }}</li>
                <li>CCA3: {{ dataDetails.cca3 }}</li>
                <li>Status: {{ dataDetails.status }}</li>
                <li><a :href="dataDetails.maps?dataDetails.maps.openStreetMaps: ''" target="_blank">View map</a></li>
              </ul>
                
            </div>
          </div>
        </div>
        <div class="modal-footer">
          <button
            type="button"
            class="btn btn-secondary"
            data-bs-dismiss="modal"
          >
            Close
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {};
  },
  props: ["title", "dataDetails"],
  methods: {
    openModalDialog() {
      this.$refs.showDialog.click();
    },
  },
};
</script>
<style></style>
