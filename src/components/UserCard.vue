<template>
  <div class="user-card" :style="{ backgroundColor: fixedColor }">
    <div class="photo-preview">
      <img v-if="user.photo" :src="user.photo" alt="User Photo" />
    </div>
    <div class="user-info-bar">
      <span class="admin">{{ user.name }}</span>
      <span class="imovelguide">{{ user.surname }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'UserCard',
  props: {
    user: Object,
    fixedColor: String
  }
}
</script>

<style>
.user-card {
  width: 260px;
  border-radius: 6px;
  display: flex;
  flex-direction: column;
  align-items: center;
  border: none;
  margin: 0 auto;
  padding: 0;
  box-shadow: 0 2px 8px #0001;
}
.photo-preview {
  width: 180px;
  height: 180px;
  border: 2px solid #000;
  background: #fff center/cover no-repeat;
  margin: 24px 0 0 0;
  display: flex;
  align-items: center;
  justify-content: center;
}
.photo-preview img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
.user-info-bar {
  width: 100%;
  background: #000;
  color: #fff;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 6px;
  font-weight: bold;
  font-size: 18px;
  padding: 8px 0;
  margin-top: 16px;
}
.user-info-bar .admin {
  color: #fff;
}
.user-info-bar .imovelguide {
  color: #FF9900;
}
</style>