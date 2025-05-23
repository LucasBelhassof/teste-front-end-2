<template>
    <div class="user-form">
        <div class="photo-section">
            <div class="photo-preview" :style="{ backgroundImage: user.photo ? 'url(' + user.photo + ')' : '' }"></div>
            <input type="file" id="photo" @change="onFileChange" accept="image/*" style="display: none;" />
            <button class="photo-btn" @click="triggerFileInput">ADICIONAR FOTO</button>
        </div>
        <div class="fields">
            <label>Nome</label>
            <input type="text" v-model="user.name" />
            <label>Sobrenome</label>
            <input type="text" v-model="user.surname" />
            <div class="color-buttons">
                <span>Cor do card:</span>
                <button
                    class="color-btn"
                    :class="{ selected: user.cardColor === '#ECB117' }"
                    @click="setColor('#ECB117')"
                    style="background: linear-gradient(90deg, #ECB117 50%, #000 50%);"
                    aria-label="Amarelo e Preto"
                ></button>
                <button
                    class="color-btn"
                    :class="{ selected: user.cardColor === '#9B0021' }"
                    @click="setColor('#9B0021')"
                    style="background: linear-gradient(90deg, #9B0021 50%, #000 50%);"
                    aria-label="Vinho e Preto"
                ></button>
            </div>
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
        },
        setColor(color) {
            this.user.cardColor = color;
        }
    }
}
</script>

<style>
.user-form {
    display: flex;
    align-items: flex-start;
    gap: 20px;
    border: 2px solid #e0e4e8;
    padding: 20px;
    border-radius: 6px;
    background: #fff;
    width: fit-content;
    margin: 40px auto; /* Centraliza na tela */
}
.photo-section {
    display: flex;
    flex-direction: column;
    align-items: center;
}
.photo-preview {
    width: 120px;
    height: 120px;
    border: 2px solid #888;
    background: #fff center/cover no-repeat;
    margin-bottom: 10px;
}
.photo-btn {
    background: orange;
    color: #fff;
    border: none;
    padding: 10px 24px;
    border-radius: 2px;
    cursor: pointer;
    font-weight: bold;
}
.fields {
    display: flex;
    flex-direction: column;
    gap: 10px;
}
.fields label {
    font-size: 14px;
    margin-bottom: 2px;
}
.fields input {
    padding: 6px;
    border: 1px solid #ccc;
    border-radius: 2px;
    font-size: 15px;
}
.color-buttons {
    display: flex;
    align-items: center;
    gap: 16px;
    margin-top: 10px;
}
.color-btn {
    width: 36px;
    height: 20px;
    border-radius: 2px;
    cursor: pointer;
    outline: none;
    border: 2px solid #ccc;
    padding: 0;
    transition: border 0.2s;
}
.color-btn.selected {
    border: 2px solid #333;
}
</style>