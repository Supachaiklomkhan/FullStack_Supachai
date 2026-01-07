<template>
  <div class="p-30 w-screen mx-auto" style="font-family: 'Prompt', sans-serif;">
    
    <div class="flex items-center space-x-4 mb-6">
      <img :src="getAvatar(user.avatar)" alt="Avatar" class=
      "w-20 h-20 rounded-full object-cover" />
      <div>
        <h1 class="text-2xl font-bold">{{ user.name }}</h1>
        <p class="text-gray-500 capitalize">{{ user.role }}</p>
      </div>
    </div>

    <div class="flex gap-2 mb-6">
      <input 
        v-model="newTaskTitle" 
        placeholder="Add new task" 
        class="flex-1 border rounded p-2"
        @keyup.enter="addTask"
      >
      <button @click="addTask" class="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600">
        Add
      </button>
    </div>

    <h2 class="text-xl font-semibold mb-2">เพิ่มงานใหม่</h2>
    <ul>
      <li v-for="task in tasks" :key="task.id" class=
      "flex items-center justify-between border-b py-2">
        <div class="flex items-center gap-2">
          <input type="checkbox" v-model="task.completed" @change="updateTaskStatus(task)">
          <span :class="{ 'line-through text-gray-400': task.completed }">
            {{ task.title }}
          </span>
        </div>
        <button @click="deleteTask(task.id)" class="text-red-500 hover:text-red-700">
          Delete
        </button>
      </li>
    </ul>

  </div>
</template>

<script>
export default {
  data() {
    return {
      // ข้อมูล User [cite: 50-54]
      user: {
        name: 'ศุภชัย กลมขันธ์',
        role: 'นักศึกษา',
        avatar: 'avartar.png' 
      },
      newTaskTitle: '', // ตัวแปรรับค่าจาก Input [cite: 55]
      // รายการงานเริ่มต้น [cite: 56-60]
      tasks: [
        { id: 1, title: 'รายงานประจำเดือน', completed: false },
        { id: 2, title: 'ติดตามงานนำเสนอ', completed: true },
        { id: 3, title: 'ส่งแบบฟอร์มประเมิน', completed: false },
      ]
    }
  },
  methods: {
    // ฟังก์ชันจัดการรูปภาพ [cite: 66-68]
    getAvatar(filename) {
      // คืนค่า path รูปภาพจากโฟลเดอร์ uploads
      return filename ? `/uploads/${filename}` : 'https://via.placeholder.com/150';
    },
    // ฟังก์ชันเพิ่มงาน [cite: 69-79]
    addTask() {
      // ตรวจสอบว่ามีข้อความหรือไม่ (แก้ Bug จากในภาพเพื่อให้ทำงานได้จริง)
      if (!this.newTaskTitle.trim()) return;

      this.tasks.push({
        id: Date.now(),
        title: this.newTaskTitle,
        completed: false
      });
      // เคลียร์ช่อง Input
      this.newTaskTitle = '';
    },
    // ฟังก์ชันอัปเดตสถานะ (แสดงผลใน Console) [cite: 80-82]
    updateTaskStatus(task) {
      console.log(`Task ${task.id} status: ${task.completed}`);
    },
    // ฟังก์ชันลบงาน [cite: 83-84]
    deleteTask(taskId) {
      this.tasks = this.tasks.filter(t => t.id !== taskId);
    }
  }
}
</script>