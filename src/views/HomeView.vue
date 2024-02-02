<script setup>
import { ref } from 'vue';
let search_status = ref(false)
let TrackInput = ref('')
let formCustomer = ref(
        [
            {
                trackId : 'ic00001',
                name : 'ทีเด็ด',
                status : 'ซ่อมเสร็จแล้ว',
                desc : 'จอฟ้า'
            },
            {
                trackId : 'ic00002',
                name : 'ทิว',
                status : 'กำลังซ่อม',
                desc : 'ทำความสะอาด'
            },
            {
                trackId : 'ic00003',
                name : 'นวลจันทร์',
                status : 'รอซ่อม',
                desc : 'ลงโปรแกรมใหม่'
            },
            {
                trackId : 'ic00004',
                name : 'ติ๊ก',
                status : 'ซ่อมเสร็จแล้ว',
                desc : 'เปลี่ยน HDD'
            },
            {
                trackId : 'ic00005',
                name : 'มังกร',
                status : 'รอซ่อม',
                desc : 'ติดตั้งวินโดว์ใหม่'
            },
        ],
    )
let displayData = ref([])
const search = () => {
    search_status.value = !search_status.value
    displayData.value = []
    if(TrackInput.value){
        formCustomer.value.filter((findData) => {
            if(findData.trackId === TrackInput.value){
                displayData.value.push(findData)
                // console.log(displayData.value)
                search_status.value = !search_status.value
            }else{
                search_status.value = !search_status.value
            }
        })
    }else{
        search_status.value = !search_status.value
    }
    // console.log(formCustomer.value)
}
</script>

<template>
    <div class="container w-96 h-96 mx-auto md:w-1/2 lg:w-full">
        <div class="flex justify-center gap-3 h-24">
            <span class="loading loading-spinner loading-md h-8" v-if="search_status"></span>
            <input type="text" v-model="TrackInput" class="input input-bordered input-sm w-1/3" placeholder="Track your number">
            <button class="btn border-b-cyan-300 border-e-cyan-300 btn-sm">
                <span class="material-symbols-outlined" @click="search">search</span>
            </button>
        </div>
        <div class="grid grid-cols-4 gap-4 mb-6">
            <div>ชื่อลูกค้า</div>
            <div>สถานะงาน</div>
            <div>รายละเอียด</div>
            <div>ติดต่อสอบถาม</div>
        </div>
        <div class="grid grid-cols-4 gap-4" v-if="displayData.length > 0">
            <div>K. {{ displayData[0].name }}</div>
            <div>
                <span class="badge badge-success" v-if="displayData[0].status == 'ซ่อมเสร็จแล้ว'">{{ displayData[0].status }}</span>
                <span class="badge badge-warning" v-if="displayData[0].status == 'กำลังซ่อม'">{{ displayData[0].status }}</span>
                <span class="badge badge-secondary" v-if="displayData[0].status == 'รอซ่อม'">{{ displayData[0].status }}</span>
            </div>
            <div>{{ displayData[0].desc }}</div>
            <div class="px-6">
                <button class="btn btn-sm btn-secondary">
                    <span class="material-symbols-outlined text-white">
                        support_agent
                    </span>
                </button>
            </div>
        </div>
        <div v-else>
            <div class="container w-96 mx-auto text-3xl text-white mt-12">ไม่พบข้อมูล</div>
        </div>
    </div>
</template>