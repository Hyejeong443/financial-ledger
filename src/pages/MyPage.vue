<template>
  <div class="profile-container" v-if="member">
    <img src="../assets/images/profile.png" alt="User Icon">
    <div class="profile-details">
      <div class="profile-item">
        <span class="label">ID</span>
        <span class="value">{{ member.member_id }}</span>
      </div>
      <div class="profile-item">
        <span class="label">사용자명</span>
        <span class="value">{{ member.member_name }}</span>
      </div>
      <div class="profile-item">
        <span class="label">패스워드</span>
        <span class="value">{{ maskedPassword }}</span> <!-- 패스워드 마스킹 처리 -->
      </div>
      <div class="profile-item">
        <span class="label">휴대폰 번호</span>
        <span class="value">{{ member.phone_no }}</span>
      </div>
      <div class="profile-item">
        <span class="label">직장정보</span>
        <span class="value">{{ member.status }}</span>
      </div>
    </div>
    <button @click="handleEdit">수정</button>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';
import { useRouter } from 'vue-router';

export default {
  setup() {
    const member = ref(null);
    const maskedPassword = ref('');
    const router = useRouter();

    onMounted(() => {
      const loggedInUser = JSON.parse(localStorage.getItem('loggedInUser'));
      if (loggedInUser) {
        member.value = loggedInUser;
        maskedPassword.value = '●'.repeat(loggedInUser.password.length);
      }
    });

    const handleEdit = () => {
      router.push({ name: 'UpdateProfile' });
    };

    return {
      member,
      maskedPassword,
      handleEdit
    };
  }
};
</script>

<style scoped>
body {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0;
  background-color: #f5f5f5;
  font-family: Arial, sans-serif;
}

.profile-container {
  width: 400px;
  padding: 20px;
  background-color: #fff;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
  text-align: center;
  margin:0 auto;
}

.profile-container img {
  width: 100px;
  height: 100px;
  margin-bottom: 20px;
}

.profile-details {
  text-align: left;
  margin-bottom: 20px;
}

.profile-item {
  display: flex;
  justify-content: space-between;
  margin-bottom: 10px;
}

.label {
  font-weight: bold;
  margin-right: 10px;
}

.value {
  color: #555;
}

button {
  padding: 10px 20px;
  background-color: #000;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  background-color: #444;
}
</style>
