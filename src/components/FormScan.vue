<template>
    <div class="card mb-3">
        <div class="card-header">
            Scan Ekspedisi
        </div>
        <div class="card-body">
            <h6>Tanggal : {{ today }}</h6>
            <h6>Pilih Ekspedisi : </h6>
            <select class="form-select mb-2 form-select-sm" aria-label="Default select example"
                v-model="form.ekspedisi">
                <option selected value="">Silahkan Pilih Ekspedisi</option>
                <option :value="item" v-for='item in $store.state.ekspedisi' :key='item'>{{ item }}</option>
            </select>
            <h6>Jumlah Kode Seri : <span class="badge bg-primary rounded-pill">{{ form.data.length }}</span></h6>
            <table class="table table-sm">
                <thead>
                    <tr>
                        <th scope="col">No</th>
                        <th scope="col">Kode Resi</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(item, key) in form.data" :key="key">
                        <th scope="row">{{ key + 1 }}</th>
                        <td>{{ item }}</td>
                    </tr>
                </tbody>
            </table>
            <div class="d-grid gap-2 d-md-flex justify-content-md-end mb-2">
                <button class="btn btn-primary btn-sm me-md-2" type="button" id="liveToastBtn">Simpan</button>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'form-scan',
        data() {
            return {
                today: this.$moment().format('YYYY-MMMM-DD'),
                form: {
                    ekspedisi: "",
                    date: new Date().toISOString(),
                    data: [
                        "1243243521",
                    ]
                },
            }
        },
    }
</script>