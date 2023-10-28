<template>
    <div>

        <div class="search mt-3 col-lg my-3">
        <form @submit.prevent="getData">
            <input 
            v-model="keyword"
            class="form-control form-control-lg rounded-pill" 
            placeholder="Cari buku teks paling komprehensif." 
            type="search">
        </form>
        </div> 

        <div class="row">
            <div v-for="book in books" :key="book.id" class="col-3"> 
                <br>
                <div class="card">
                    <div class="card-header">
                        <img :src="book.cover" alt="cover" class="cover">
                        <div v-for="item in items" :key="item.id">
                            {{ item }}
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- table -->
    <!-- <div class="container">
      <table class="table table-striped table-light mt-4">
        <thead>
          <tr>
            <td>COVER</td>
            <td>JUDUL</td>
            <td>PENULIS</td>
            <td>PENERBIT</td>
            <td>KATEGORI</td>
            <td>RAK</td>
          </tr>
        </thead>
        <tbody>
          <tr v-for="book in books" :key="book.id">
            <td><img :src="book.cover" alt=""></td>
            <td>{{ book.judul }}</td>
            <td>{{ book.penulis }}</td>
            <td>{{ book.penerbit }}</td>
            <td>{{ book.kategori.nama }}</td>
            <td>{{ book.rak.kode }}</td>
          </tr>
        </tbody>
      </table>
    </div> -->


    </div>
</template>

<script setup>
const supabase = useSupabaseClient()
const books = ref([])
const keyword = ref("")

onMounted(() => getData())

async function getData() {
    let { data, error } = await supabase
        .from('buku')
        .select(`
            id, judul, penulis, penerbit,
            kategori(nama), rak(kode), cover
        `)
        .ilike('judul', `%${keyword.value}%`)
    if(data) books.value = data
    if(error) throw error
}
</script>


<style scoped>
.cover {
    width: 100%;
}
</style>