<template>
    <div class="user-form">
        <div class="photo-preview" :style="{ backgroundImage: user.photo ? 'url(' + user.photo + ')' : '' }"></div>
        <input type="file" id="photo" @change="onFileChange" accept="image/*" style="display: none;" />
        <button class="photo-btn" @click="triggerFileInput">ADICIONAR FOTO</button>
        <div class="fields">
            <label>Nome</label>
            <input type="text" v-model="user.name" />
            <label>Sobrenome</label>
            <input type="text" v-model="user.surname" />
        </div>
    </div>
</template>

<script>
export default {
    name: 'UserForm',
    data() {
        return {
            user: {
                photo: '',
                name: '',
                surname: '',
                cardColor: '#ECB117'
            }
        }
    },
    watch: {
        user: {
            handler() {
                this.$emit('updateUser', this.user);
            },
            deep: true
        }
    },
    methods: {
        triggerFileInput() {
            this.$el.querySelector('#photo').click();
        },
        onFileChange(e) {
            const file = e.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = e => {
                    this.user.photo = e.target.result;
                };
                reader.readAsDataURL(file);
            }
        }
    }
}
</script>

<style>
.user-form {
    display: flex;
    flex-direction: column;
    align-items: center;
    border: 3px solid #e0e4e8;
    border-radius: 4px;
    background: #fff;
    width: 340px;
    padding: 28px 18px 24px 18px;
    margin: 32px auto;
    box-sizing: border-box;
}
.photo-preview {
    width: 150px;
    height: 150px;
    border: 2px solid #444;
    background: #fff center/cover no-repeat;
    margin-bottom: 18px;
}
.photo-btn {
    background: #FF9900;
    color: #fff;
    border: none;
    padding: 10px 0;
    border-radius: 2px;
    cursor: pointer;
    font-weight: bold;
    width: 100%;
    margin-bottom: 18px;
    font-size: 16px;
    transition: background 0.2s;
}
.photo-btn:hover {
    background: #ecb117;
}
.fields {
    display: flex;
    flex-direction: column;
    gap: 12px;
    width: 100%;
}
.fields label {
    font-size: 14px;
    margin-bottom: 2px;
    text-align: left;
}
.fields input {
    padding: 8px;
    border: 1px solid #ccc;
    border-radius: 2px;
    font-size: 15px;
    width: 100%;
    box-sizing: border-box;
}
</style>