<template>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container-fluid">
        <router-link to="/home" class="navbar-brand fw-bold text-success">
          Quản lý công việc
        </router-link>
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarNav"
          aria-controls="navbarNav"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav me-auto">
            <li class="nav-item">
              <router-link to="/tasks" class="nav-link">Danh sách</router-link>
            </li>
            <li class="nav-item">
              <router-link to="/add-task" class="nav-link">Thêm công việc</router-link>
            </li>
          </ul>
          <ul class="navbar-nav">
            <li class="nav-item d-flex align-items-center">
              <!-- Avatar -->
              <img
                v-if="userAvatar"
                :src="userAvatar"
                alt="Avatar"
                class="rounded-circle me-2"
                style="width: 40px; height: 40px;"
              />
              <!-- Tên người dùng -->
              <span class="nav-link fw-bold">{{ userName }}</span>
            </li>
            <li class="nav-item">
              <button @click="logout" class="btn btn-outline-danger btn-sm">Đăng xuất</button>
            </li>
          </ul>
        </div>
      </div>
    </nav>
  </template>
  
  <script setup>
  import { ref, onMounted } from "vue";
  import { useRouter } from "vue-router";
  
  // Thông tin người dùng
  const userName = ref("Chưa Đăng Nhập");
  const userAvatar = ref(null);
  const router = useRouter();
  
  // Lấy thông tin người dùng từ sessionStorage khi component được tải
  onMounted(() => {
    const loggedInUser = JSON.parse(sessionStorage.getItem("loggedInUser"));
    if (loggedInUser) {
      userName.value = loggedInUser.name || "Người dùng";
      userAvatar.value = loggedInUser.avatar || null;
    }
  });
  
  const logout = () => {
    // Xóa thông tin đăng nhập khỏi sessionStorage
    sessionStorage.removeItem("isLoggedIn");
    sessionStorage.removeItem("loggedInUser");
    // Chuyển hướng về trang đăng nhập
      router.push("/");
      window.location.reload(); // Tải lại trang để cập nhật giao diện
  };
  </script>
  
  <style scoped>
  .navbar {
    margin-bottom: 20px;
  }
  
  img {
    border: 1px solid #ddd;
  }
  </style>
  
