<template>
     <div class="min-h-screen p-8 bg-gray-100" style="font-family: 'Prompt', sans-serif; ">
        <h1 class="text-2xl font-bold text-center pt-15 pb-5">รายงานผลการประเมินบุคลากร</h1>

        <div class="bg-white p-6 rounded-1xl shadow-md">
            <button @click="clearEvaluations" class="mt-4 bg-red-500 hover:bg-red-600 text-white px-4 oy-2 rounded-lg mb-5">ลบข้อมูลรายงานทั้งหมด </button>
            <table class="w-full border-collapse">
                <thead>
                    <tr class="bg-blue-200 text-gray-700">
                        <th class="border p-2">ลำดับ</th>
                        <th class="border p-2">ชื่อครู</th>
                        <th class="border p-2">ผู้ประเมิน</th>
                        <th class="border p-2">ภาควิชา</th>
                        <th class="border p-2">รอบการประเมิน</th>
                        <th class="border p-2">คะแนนรวม</th>
                        <th class="border p-2">วันที่ประเมิน</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(item, index) in evaluations" :key="index" class="hover:bg-gray-50">
                        <td class="border p-2 text-center">{{ index + 1 }}</td>
                        <td class="border p-2">{{ item.teacher }}</td>
                        <td class="border p-2">{{ item.evaluator }}</td>
                        <td class="border p-2">{{ item.department }}</td>
                        <td class="border p-2">{{ item.period }}</td>
                        <td class="border p-2 text-center font-semibold text-blue-700">{{ item.totalScore }}</td>
                        <td class="border p-2">{{ item.data }}</td>
                    </tr>
                </tbody>
            </table>
            <p v-if="evaluations.length === 0" class="text-center text-gray-500 mt-4">
                ยังไม่มีข้อมูลการประเมิน
            </p>
        </div>
     </div>
</template>
<script>
export default {
    data() {
        return {
            evaluations: []
        };
    },
    mounted() {
        const saved = localStorage.getItem("evaluations");
        this.evaluations = saved ? JSON.parse(saved) : [];
    },
    methods: {
        clearEvaluations() {
            localStorage.removeItem("evaluations");

            this.evaluations = [];

            alert("ลบข้อมูลทั้งหมดเรียบร้อย!");
        }
    }
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Prompt:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap');
</style>