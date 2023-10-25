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
                        <div>{{ book.judul }}</div>
                </div>
                </div>
            </div>
        </div>

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
    width: 100px;
}
</style>