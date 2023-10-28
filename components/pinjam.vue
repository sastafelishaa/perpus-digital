<!-- <template>
    <div class="pinjam">
        <div class="text-center">
            <h2>Silahkan Isi Data</h2>
        </div>
        <form @submit.prevent="pinjamBuku">
            <div class="form-group py-3">
                <label for="exampleFormControlImput1">
                    Nama
                </label>
                <input v-model='nama' type="nama" class="form-control" id="exampleFormControlImput1" />
            </div>
            <div class="form-group py-3">
                <label for="exampleFormControlImput1">
                    Kelas
                </label>
                <input v-model='kelas' type="nama" class="form-control" id="exampleFormControlImput1" />
            </div>
            <div class="form-group py-3">
                <label for="exampleFormControlImput1">
                    Judul Buku
                </label>
                <input v-model='judul' type="nama" class="form-control" id="exampleFormControlImput1" />
            </div>
            <button type="submit" class="btn btn-primary">Pinjam</button>
        </form>
    </div>
</template>

<script setup>
const supabase = useSupabaseClient()
const nama = ref("")
const kelas = ref("")
const judul = ref("")

async function pinjamBuku() {
    const {error} = await supabase
    .from('pinjam')
    .insert([
        {
            nama: nama.value,
            kelas: kelas.value,
            judul: judul.value
        }
    ])
    if (error) throw error
    else navigateTo()
}
</script> -->