<template>
  <div class="min-h-full flex items-center justify-center bg-blue-500 py-12 px-4 sm:px-6 lg:px-8">
    <div class="max-w-md w-full space-y-8 bg-white p-10 rounded-xl shadow-lg">
      <div class="text-center">
        <h2 class="mt-6 text-3xl font-bold text-gray-900">Sign Up</h2>
        <p class="mt-2 text-sm text-blue-500">Please fill in the form below to create an account.</p>
      </div>

      <form @submit.prevent="signup" class="mt-8 space-y-6">
        <div>
          <label class="text-gray-600 font-medium">First Name</label>
          <input v-model="form.fname" type="text"
            class="w-full border border-gray-300 rounded-lg p-2 focus:ring-2 focus:ring-blue-400 focus:outline-none"
            placeholder="First Name" required>
        </div>

        <div>
          <label class="text-gray-600 font-medium">Last Name</label>
          <input v-model="form.lname" type="text"
            class="w-full border border-gray-300 rounded-lg p-2 focus:ring-2 focus:ring-blue-400 focus:outline-none"
            placeholder="Last Name" required>
        </div>

        <div>
          <label class="text-gray-600 font-medium">Username</label>
          <input v-model="form.username" type="text"
            class="w-full border border-gray-300 rounded-lg p-2 focus:ring-2 focus:ring-blue-400 focus:outline-none"
            placeholder="Username" required>
        </div>

        <div>
          <label class="text-gray-600 font-medium">Password</label>
          <input v-model="form.password" type="password"
            class="w-full border border-gray-300 rounded-lg p-2 focus:ring-2 focus:ring-blue-400 focus:outline-none"
            placeholder="Password" required>
        </div>

        <div>
          <label class="text-gray-600 font-medium">Role</label>
          <select v-model="form.role"
            class="w-full border border-gray-300 rounded-lg p-2 focus:ring-2 focus:ring-blue-400 focus:outline-none">
            <option value="user">User</option>
            <option value="admin">Admin</option>
          </select>
        </div>

        <div>
          <label class="text-gray-600 font-medium">Avatar</label>
          <input type="file" @change="handleFile" class="w-full mt-1 text-gray-600">
        </div>

        <button type="submit"
          class="w-full py-3 bg-blue-500 hover:bg-blue-600 text-white font-semibold rounded-lg transition duration-200">
          Sign Up
        </button>

        <div class="text-center text-gray-500 mt-4">
          คุณมีบัญชีอยู่แล้ว?
          <router-link to="/login" class="text-blue-600 hover:underline">เข้าสู่ระบบ</router-link>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "SignUp",
  data() {
    return {
      form: {
        fname: "",
        lname: "",
        username: "",
        password: "",
        avatar: null,
        role: "user",
      },
    };
  },
  methods: {
    handleFile(event) {
      this.form.avatar = event.target.files[0];
    },
    async signup() {
      const formData = new FormData();
      formData.append("fname", this.form.fname);
      formData.append("lname", this.form.lname);
      formData.append("username", this.form.username);
      formData.append("password", this.form.password);
      
      if (this.form.avatar) {
        formData.append("avatar", this.form.avatar);
      }
      
      formData.append("role", this.form.role);

      try {
        const res = await fetch("http://localhost:3000/signup", {
          method: "POST",
          body: formData,
        });

        if (res.ok) {
          this.form = {
            fname: "",
            lname: "",
            username: "",
            password: "",
            avatar: null,
            role: "user",
          };
          alert("Signup successful!");
        } else {
          const error = await res.json();
          alert("Signup failed: " + (error.message || "Unknown error"));
          console.log(error);
        }
      } catch (err) {
        console.error("Error during signup", err);
        alert("Error connecting to server");
      }
    },
  },
};
</script>

