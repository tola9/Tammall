<template>
  <div class="content">
    <nav aria-label="breadcrumb">
      <ol class="breadcrumb">
        <li class="breadcrumb-item active" aria-current="page">Brands</li>
      </ol>
    </nav>
    <div class="kv-card">
      <div class="kv-card-header">
        <div class="row justify-content-between">
          <div class="col-8">
            <form>
              <div class="row">
                <div class="col-3 text-right">
                  <label for="exampleInputEmail1">Search Brands</label>
                </div>
                <div class="col-4 text-right">
                  <div class="form-group mb-0">
                    <select class="form-control" v-model="addSubBrand" @change="changSub">
                      <option selected>Choose...</option>
                      <option
                        v-for="(brand, index) in brands"
                        :key="index"
                        :value="brand"
                      >{{ brand.name }}</option>
                    </select>
                  </div>
                </div>
                <div class="col-5">
                  <button v-if="addSubBrand" @click="addNew" type="submit" class="btn btn-primary">
                    <i class="fal fa-plus-circle"></i>
                    Add New Brands
                  </button>
                </div>
              </div>
            </form>
          </div>
        </div>
      </div>
      <div class="table-responsive">
        <table class="table kv-table">
          <thead>
            <tr>
              <th scope="col">#</th>
              <th scope="col">Brands Image</th>
              <th scope="col">Brands name</th>
              <th scope="col">Description</th>
              <th scope="col">Create Date</th>
              <th scope="col"></th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(subbrand, index) in subbrands" :key="index">
              <td scope="row">{{ index + 1 }}</td>
              <td><img
                class="p-image rounded"
                :src="getImage(subbrand.image.path,'1080x1080')"
                alt="pro-image"
              /></td>
              <td>{{ subbrand.name }}</td>
              <td>{{ subbrand.description }}</td>
              <td>{{ $dateFormat(subbrand.created_at) }}</td>
              <td>
                <button
                  class="dropdown-item"
                  @click="del(subbrand.id)"
                  href="#"
                >
                  <i class="fal fa-times-circle"></i> Delete
                </button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
      <!-- End Table -->
      <div
        class="kv-pagination d-flex flex-column flex-sm-row justify-content-sm-between align-items-center"
      >
        <div class="info">show from 1 to 10 of 25</div>
        <nav aria-label="Page navigation example">
          <ul class="pagination mb-0">
            <li class="page-item">
              <a class="page-link">Previous</a>
            </li>
            <li class="page-item">
              <a class="page-link">1</a>
            </li>
            <li class="page-item">
              <a class="page-link">2</a>
            </li>
            <li class="page-item">
              <a class="page-link">3</a>
            </li>
            <li class="page-item">
              <a class="page-link">Next</a>
            </li>
          </ul>
        </nav>
      </div>
    </div>
  </div>
</template>
<script>
import retrieveSubBrand from "~/mixins/stores/retrieveSubBrand";

export default {
  mixins: [retrieveSubBrand],
  methods: {
    getImage (url,size){
      if(url=="" || url==null){
        return null;
      }
      if(url!=null && url!=""){
        url = url.replaceAll("https://firebasestorage.googleapis.com/v0/b/tamneak-d40f1.appspot.com/o/", "http://cdn.tamneak.com/");
        url = url.replaceAll("https://firebasestorage.googleapis.com/v0/b/product-eaa84.appspot.com/o/", "http://34.120.98.30/");
      }
      // let resultraw = url.replaceAll(".jpg", '_' +size + '.jpg');
      url = url.replaceAll(".jpg", '_' +size + '.jpg');
      url = url.replaceAll(".png", '_' +size + '.png');
      return url;
    }
  }
};
</script>

<style lang="scss" scoped></style>
