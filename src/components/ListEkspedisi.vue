<template>
  <div class="card">
    <div class="card-header">
      Daftar Ekspedisi
    </div>
    <div class="card-body">
      <div class="mb-3 row">
        <div class="col-sm-10">
          <div class="row">
            <label for="inputPassword" class="col-sm-3 col-form-label">Pilih Tanggal</label>
            <div class="col-sm-9">
              <date-range-picker class="form-control form-control-sm mb-2" v-model="dateRange" :timePicker24Hour="false"
                ref="picker">
                <template v-slot:input="picker" style="min-width: 350px;">
                  {{ picker.startDate | date }} - {{ picker.endDate | date }}
                </template>
              </date-range-picker>
            </div>
            <label for="inputPassword" class="col-sm-3 col-form-label">Pilih Ekspedisi</label>
            <div class="col-sm-9">
              <select class="form-select mb-2 form-select-sm" aria-label="Default select example">
                <option selected value="">Silahkan Pilih Ekspedisi</option>
                <option :value="item" v-for='item in $store.state.ekspedisi' :key='item'>{{ item }}</option>
              </select>
            </div>
          </div>
        </div>
        <div class="col-sm-2">
          <div class="d-grid gap-2 mx-auto col-12">
            <button class="btn btn-primary" type="button">cari</button>
          </div>
        </div>
      </div>
      <div>
        <div class="table-responsive mt-2">
          <table class="table table-sm">
            <thead>
              <tr>
                <th scope="col">No</th>
                <th scope="col">Nama Ekspedisi</th>
                <th scope="col">Tanggal Ekspedisi</th>
                <th scope="col">#</th>
              </tr>
            </thead>
            <tbody v-if="!isLoadingList" class="mb-2">
              <tr v-for="(item, key) in data" :key="key">
                <th scope="row">{{ (page - 1) * perPage + 1 + key }}</th>
                <td>{{ item.ekspedisi }}</td>
                <td>{{ item.date }}</td>
                <td class="action-table">
                  <button class="btn btn-outline-primary btn-sm" data-bs-toggle="modal"
                    data-bs-target="#staticBackdrop">
                    Detail
                  </button>
                  <button class="btn btn-outline-success btn-sm">Excel</button>
                  <button class="btn btn-outline-danger btn-sm">PDF</button>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
      <nav aria-label="..." class="mt-2">
        <ul class="pagination">
          <li class="paginate_button page-item" :class="{disabled: page == 1}" v-if="page > 1">
            <a href="#" class="page-link" v-on:click="paginate('previous')">Sebelumnya</a>
          </li>
          <li class="page-item" :class='item == page ? "active" : ""' v-for="item in arrayPage()" :key="item">
            <a class="page-link" href="#" @click="pages(item)">{{ item }}</a>
          </li>
          <li class="paginate_button page-item" :class="{disabled: page >= total}" v-if="page != total">
            <a href="#" class="page-link" v-on:click="paginate('next')">Berikutnya</a>
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
  import DateRangePicker from 'vue2-daterange-picker'
  import moment from 'moment'
  import 'vue2-daterange-picker/dist/vue2-daterange-picker.css'
  export default {
    name: 'list-ekspedisi',
    components: {
      DateRangePicker
    },
    data() {
      return {
        data: [{
          id: 1,
          ekspedisi: 'JNE',
          date: this.$moment().format('DD MMMM YYYY'),
        }, ],
        page: 1,
        perPage: 5,
        total: 1,
        isLoadingList: false,
        filter: {
          startDate: null,
          endDate: null,
          ekspedisi: ''
        },
        dateRange: {
          startDate: moment(),
          endDate: moment(),
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
      },
      arrayPage: function () {
        let arr = [];
        let awal = 1;
        let akhir = this.total;

        if (akhir > 5) akhir = 5;

        if (this.page > 3) {
          awal = this.page - 2;
          akhir = this.page + 2;

          if ((this.total - this.page) === 1 || this.total === this.page) {
            akhir = this.total;
            awal = this.total - 4;

            if (awal === 0) {
              awal = 1;
            }
          }
        }

        let no = 0;
        for (let i = awal; i <= akhir; i++) {
          arr[no] = i;

          no += 1;
        }
        return arr;
      },
      paginate(direction) {
        if (direction === 'previous') {
          if (this.page > 1) {
            --this.page;
            this.loadingList();
          }
        } else if (direction === 'next') {
          if (Math.floor((this.total - 1) / this.perPage) !== (this.page - 1)) {
            ++this.page;
            this.loadingList();
          }
        } else if (direction === 'first') {
          this.page = 1;
          this.loadingList();
        } else if (direction === 'last') {
          this.page = Math.floor((this.total - 1) / this.perPage) + 1;
          this.loadingList();
        }
      },
    },
    filters: {
      date(val) {
        return val ? moment(val).format('YYYY/MM/DD') : ''
      }
    }
  }
</script>

<style scoped>
  .action-table button {
    margin-left: 5px;
  }
</style>