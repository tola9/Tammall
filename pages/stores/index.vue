<template>
  <div class="content">
    <nav aria-label="breadcrumb">
      <ol class="breadcrumb">
        <li class="breadcrumb-item active" aria-current="page">Store</li>
      </ol>
    </nav>
    <!-- End  breadcrumb-->
    <div class="kv-card">
      <div class="kv-card-header">
        <div class="row">
          <div class="col-12 col-sm-6">
            <form>
              <div class="form-group mb-0">
                <label for="exampleInputEmail1">Search Store name</label>
                <input type="text" class="form-control" id="search" />
              </div>
            </form>
          </div>
          <div class="col-12 col-sm-6 text-right align-self-end">
            <nuxt-link to="/stores/add" class="btn btn-primary">
              <i class="fal fa-plus-circle"></i>
              Add New Store
            </nuxt-link>
          </div>
        </div>
      </div>
      <!--  -->
      <!--  -->
      <div class="table-responsive">
        <table class="table kv-table">
          <thead>
          <tr>
            <th scope="col">#</th>
            <th scope="col">Profile</th>
            <th scope="col">Banner</th>
            <th scope="col" class="m-w-150">Store Name</th>
            <th scope="col">Status</th>
            <th scope="col" class="m-w-150">Create Date</th>
            <th scope="col"></th>
          </tr>
          </thead>
          <tbody>
          <tr v-for="(store, index) in stores" :key="index">
            <th scope="row">{{ index + 1 }}</th>
            <td>
              <a :href="getImage(store.profile.path,'1080x1080')" target="_blank">
                <img
                  class="p-image rounded"
                  :src="getImage(store.profile.path,'1080x1080')"
                  alt="pro-image"
                />
              </a>
            </td>
            <td>
              <a :href="getImage(store.banner.path,'1080x1080')" target="_blank">
                <img
                  class="p-image rounded"
                  :src="getImage(store.banner.path,'1080x1080')"
                  alt="pro-image"
                />
              </a>
            </td>
            <td>{{ store.name }}</td>
            <td>
              <div class="custom-control custom-switch">
                <input
                  :checked="store.status"
                  type="checkbox"
                  class="custom-control-input"
                  :id="'customSwitch' + index"
                />
                <label
                  @click="toggle(store.id, store.status)"
                  class="custom-control-label"
                  :for="'customSwitch' + index"
                ></label>
              </div>
            </td>
            <td>{{ $dateFormat(store.created_at) }}</td>
            <td>
              <!-- Split dropleft button -->
              <div class="dropleft">
                <i
                  class="fas fa-ellipsis-v"
                  role="button"
                  id="dropdownMenuLink"
                  data-toggle="dropdown"
                  aria-haspopup="true"
                  aria-expanded="false"
                ></i>
                <div
                  class="dropdown-menu mr-3"
                  aria-labelledby="dropdownMenuLink"
                >
                  <div class="drop-wrap">
                    <nuxt-link
                      class="dropdown-item"
                      :to="'/stores/add?id=' + store.id"
                    >
                      <i class="fal fa-edit"></i> Edit
                    </nuxt-link>
                    <button
                      @click="del(store.id)"
                      class="dropdown-item"
                      href="#"
                    >
                      <i class="fal fa-times-circle"></i> Delete
                    </button>
                  </div>
                </div>
              </div>
            </td>
          </tr>
          </tbody>
        </table>
      </div>
      <!-- End Table -->
      <div
        class="kv-pagination d-flex flex-column flex-sm-row justify-content-sm-between align-items-center"
      >
        <div class="info">show from 1 to 10 of 85</div>
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
      <!-- End Pagination -->
    </div>
    <!-- End Card -->
  </div>
</template>
<script>
  import retrieveStores from "~/mixins/retrieveStores";

  export default {
    mixins: [retrieveStores],
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
