<script setup>
import { ref } from "vue";

// Dữ liệu danh sách điện thoại
const dienThoais = ref([
  {
    id: 1,
    ten: "iPhone 14 Pro Max",
    hang: "Apple",
    dungLuong: "256GB",
    gia: 32990000,
  },
  {
    id: 2,
    ten: "Samsung Galaxy S23 Ultra",
    hang: "Samsung",
    dungLuong: "512GB",
    gia: 29990000,
  },
  {
    id: 3,
    ten: "Oppo Find X6 Pro",
    hang: "Oppo",
    dungLuong: "256GB",
    gia: 22990000,
  },
  {
    id: 4,
    ten: "iPhone 13",
    hang: "Apple",
    dungLuong: "128GB",
    gia: 19990000,
  },
  {
    id: 5,
    ten: "Samsung Galaxy Z Fold 4",
    hang: "Samsung",
    dungLuong: "1TB",
    gia: 49990000,
  },
]);

// Dữ liệu form
const newDienThoai = ref({
  id: "",
  ten: "",
  hang: "",
  dungLuong: "",
  gia: "",
});

// Dữ liệu cho combobox Hãng và Dung Lượng
const hangOptions = ["Apple", "Samsung", "Oppo"];
const dungLuongOptions = ["64GB", "128GB", "256GB", "512GB", "1TB"];

// Hàm thêm điện thoại
const addDienThoai = () => {
  if (
    !newDienThoai.value.id ||
    !newDienThoai.value.ten ||
    !newDienThoai.value.hang ||
    !newDienThoai.value.dungLuong ||
    !newDienThoai.value.gia ||
    isNaN(newDienThoai.value.gia) || // Kiểm tra giá là số nguyên
    newDienThoai.value.gia <= 0 // Kiểm tra giá lớn hơn 0
  ) {
    alert("Vui lòng nhập đầy đủ thông tin và giá phải là số nguyên lớn hơn 0!");
    return;
  }

  dienThoais.value.push({ ...newDienThoai.value });
  newDienThoai.value = { id: "", ten: "", hang: "", dungLuong: "", gia: "" };
};

// Hàm hiển thị chi tiết điện thoại
const showDetail = (product) => {
  newDienThoai.value = { ...product };
};
</script>

<template>
  <div>
    <!-- Form Thêm Điện Thoại -->
    <form @submit.prevent="addDienThoai">
      <h3>Thêm Điện Thoại Mới</h3>

      <div>
        <label for="id">ID:</label>
        <input
          id="id"
          v-model.number="newDienThoai.id"
          type="number"
          placeholder="ID điện thoại"
        />
      </div>

      <div>
        <label for="ten">Tên:</label>
        <input
          id="ten"
          v-model="newDienThoai.ten"
          type="text"
          placeholder="Tên điện thoại"
        />
      </div>

      <div>
        <label for="hang">Hãng:</label>
        <select id="hang" v-model="newDienThoai.hang">
          <option value="" disabled>Chọn Hãng</option>
          <option v-for="hang in hangOptions" :key="hang" :value="hang">
            {{ hang }}
          </option>
        </select>
      </div>

      <div>
        <label for="dungLuong">Dung Lượng:</label>
        <select id="dungLuong" v-model="newDienThoai.dungLuong">
          <option value="" disabled>Chọn Dung Lượng</option>
          <option
            v-for="dungLuong in dungLuongOptions"
            :key="dungLuong"
            :value="dungLuong"
          >
            {{ dungLuong }}
          </option>
        </select>
      </div>

      <div>
        <label for="gia">Giá:</label>
        <input
          id="gia"
          v-model.number="newDienThoai.gia"
          type="text"
          placeholder="Giá tiền"
        />
      </div>

      <button type="submit">Thêm</button>
    </form>

    <!-- Danh Sách Điện Thoại -->
    <h3>Danh Sách Điện Thoại</h3>
    <table border="1" cellpadding="10">
      <thead>
        <tr>
          <th>ID</th>
          <th>Tên</th>
          <th>Hãng</th>
          <th>Dung Lượng</th>
          <th>Giá</th>
          <th>Chi Tiết</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="dt in dienThoais" :key="dt.id">
          <td>{{ dt.id }}</td>
          <td>{{ dt.ten }}</td>
          <td>{{ dt.hang }}</td>
          <td>{{ dt.dungLuong }}</td>
          <td>{{ dt.gia.toLocaleString() }} VNĐ</td>
          <td>
            <button @click="showDetail(dt)">Detail</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style scoped>
form {
  margin-bottom: 20px;
}
form div {
  margin: 10px 0;
}
label {
  display: inline-block;
  width: 100px;
}
input,
select {
  padding: 5px;
  width: 300px;
}
button {
  padding: 5px 10px;
  background-color: #007bff;
  color: white;
  border: none;
  cursor: pointer;
}
button:hover {
  background-color: #0056b3;
}
table {
  width: 100%;
  margin-top: 20px;
  border-collapse: collapse;
}
th,
td {
  text-align: left;
  padding: 8px;
}
th {
  background-color: #f4f4f4;
}
</style>
