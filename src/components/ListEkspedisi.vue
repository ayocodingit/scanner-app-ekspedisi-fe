<template>
  <div class="card">
    <div class="card-header">
      Daftar Ekspedisi
    </div>
    <div class="card-body">
      <div class="mb-3 row">
        <label for="inputPassword" class="col-sm-2 col-form-label">Pilih Tanggal</label>
        <div class="col-sm-10">
          <input type="text" class="form-control form-control-sm mb-2" id="inputPassword">
        </div>
      </div>
      <div class="mb-3 row">
        <label for="inputPassword" class="col-sm-2 col-form-label">Pilih Ekspedisi</label>
        <div class="col-sm-10">
          <select class="form-select mb-2 form-select-sm" aria-label="Default select example">
            <option selected value="">Silahkan Pilih Ekspedisi</option>
            <option :value="item" v-for='item in $store.state.ekspedisi' :key='item'>{{ item }}</option>
          </select>
        </div>
      </div>
      <div class="mb-3 row">
        <div class="col-sm-12">
          <div class="d-grid gap-2">
            <button class="btn btn-primary btn-sm" type="button">cari</button>
          </div>
        </div>
      </div>
      <div>
        <table class="table table-responsive table-sm">
          <thead>
            <tr>
              <th scope="col">No</th>
              <th scope="col">Nama Ekspedisi</th>
              <th scope="col">Tanggal Ekspedisi</th>
              <th scope="col">#</th>
            </tr>
          </thead>
          <tbody v-if="!isLoadingList">
            <tr v-for="(item, key) in data" :key="key">
              <th scope="row">{{ (page - 1) * perPage + 1 + key }}</th>
              <td>{{ item.ekspedisi }}</td>
              <td>{{ item.date }}</td>
              <td>
                <a href="#" class="btn btn-outline-primary btn-sm" data-bs-toggle="modal"
                  data-bs-target="#staticBackdrop">
                  Lihat Resi
                </a>
                <button class="btn btn-outline-success btn-sm">Excel</button>
                <button class="btn btn-outline-danger btn-sm">PDF</button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
      <nav aria-label="...">
        <ul class="pagination pagination-sm">
          <li class="page-item" :class='item == page ? "active" : ""' v-for="item in (1, totalPages)" :key="item">
            <a class="page-link" href="#" v-if="item < totalPages + 1" @click="pages(item)">{{ item }}</a>
          </li>
        </ul>
      </nav>
    </div>

    <!-- Modal -->
    <div class="modal fade" id="staticBackdrop" data-bs-backdrop="static" data-bs-keyboard="false" tabindex="-1"
      aria-labelledby="staticBackdropLabel" aria-hidden="true">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="staticBackdropLabel">Daftar Resi</h5>
            <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
          </div>
          <div class="modal-body">
            <button type="button" class="btn btn-sm btn-outline-primary text-dark">74329432</button>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-sm btn-primary" data-bs-dismiss="modal">Tutup</button>
          </div>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
  export default {
    name: 'list-ekspedisi',
    data() {
      return {
        data: [{
            id: 1,
            ekspedisi: 'JNE',
            date: new Date().toISOString(),
          },
          {
            id: 1,
            ekspedisi: 'JNE',
            date: new Date().toISOString(),
          },
          {
            id: 1,
            ekspedisi: 'JNE',
            date: new Date().toISOString(),
          },
          {
            id: 1,
            ekspedisi: 'JNE',
            date: new Date().toISOString(),
          },
          {
            id: 1,
            ekspedisi: 'JNE',
            date: new Date().toISOString(),
          },
          {
            id: 1,
            ekspedisi: 'JNE',
            date: new Date().toISOString(),
          },
          {
            id: 1,
            ekspedisi: 'JNE',
            date: new Date().toISOString(),
          },
          {
            id: 1,
            ekspedisi: 'JNE',
            date: new Date().toISOString(),
          },
          {
            id: 1,
            ekspedisi: 'JNE',
            date: new Date().toISOString(),
          },
        ],
        page: 1,
        perPage: 10,
        totalPages: 10,
        isLoadingList: false,
        filter: {
          date: null,
          ekspedisi: ''
        },
      }
    },
    methods: {
      pages(page) {
        this.loadingList()
        this.page = page
      },
      loadingList() {
        this.isLoadingList = true
        setTimeout(() => {
          this.isLoadingList = false
        }, 1000);
      }
    },
  }
</script>