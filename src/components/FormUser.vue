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
    border: 3px solid #e0e4e8;
    border-radius: 4px;
    background: #fff;
    width: fit-content;
    padding: 28px 18px 24px 18px;
    margin: 32px auto;
    box-sizing: border-box;
}
.photo-section {
    display: flex;
    flex-direction: column;
    align-items: center;
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

@media (max-width: 600px) {
  .user-form {
    flex-direction: column;
    align-items: center;
    width: 340px;
    min-width: unset;
    padding: 28px 18px 24px 18px;
    margin: 32px auto;
    border-radius: 4px;
    gap: 0;
  }
  .photo-section {
    width: 100%;
    align-items: center;
  }
  .photo-preview {
    margin-left: auto;
    margin-right: auto;
    display: block;
    width: 150px;
    height: 150px;
  }
  .photo-btn {
    width: 150px;
    margin-bottom: 18px;
  }
  .fields {
    width: 100%;
    align-items: center;
  }
  .fields input {
    width: 150px;
  }
  .color-buttons {
    width: 150px;
  }
}
</style>