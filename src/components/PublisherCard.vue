<template>
    <q-card class="my-card q-ma-sm my-box cursor-pointer q-hoverable" v-ripple style="width: 400px; height: 350px;">
        <div class="full-height full-width card">
            <div class="row justify-center">
                <img :src="image" class="q-mt-sm" fit="contain" style="max-width: 170px; height: 200px;">
            </div>
            <q-card-section class="full-width">
                <div class="text-h6">{{ name }}</div>
                <div class="text-subtitle-2">Địa chỉ: {{ address }}</div>
                <div class="row justify-center q-mt-md">
                    <q-btn label="Cập nhật" color="primary" @click="updatePublisher" />
                    <q-btn label="Xóa" color="negative" @click="deletePublisher" class="q-ml-md" />
                </div>
            </q-card-section>
        </div>
    </q-card>
</template>

<script>
import axios from 'axios';
import router from '../router';
export default {
    props: {
        _id: String,
        name: String,
        address: String,
        // Add image prop
        image: String
    },
    methods: {
        updatePublisher() {
            // Chuyển đến trang cập nhật thông tin nhà xuất bản
            router.push('/publishers/update/' + this._id + '?name=' + this.name + '&address=' + this.address + '&image=' + this.image);
        },
        deletePublisher() {
            // Xóa nhà xuất bản
            const token = localStorage.getItem('token');
            axios.delete('http://localhost:3333/api/publisher/' + this._id, {
                headers: {
                    token: `Bearer ${token}`
                }
            })
                .then(response => {
                    location.reload();
                    // Thông báo xóa nhà xuất bản thành công và cập nhật danh sách
                    this.$emit('publisher-deleted', this._id);
                })
                .catch(error => {
                    // Xử lý lỗi
                    console.error(error);
                });
        }
    }
};
</script>

<style scoped>
.full-height {
    height: 100%;
}

.full-width {
    width: 100%;
}

.card {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
}

.row {
    display: flex;
    justify-content: center;
}
</style>
