 <template>
     <el-row>
       <el-col :span="24" style="font-size: 29px;text-align: center; color: red"><span >{{currentTime}}</span></el-col>
       <el-col :span="24" style="font-size: 20px;text-align: center;color: green"><span >&lt;{{title}}&gt;</span></el-col>
       <el-col :span="24" style="font-size: 29px;text-align: center;">
         <el-button v-if="supt === 1" @click="start">开启</el-button>
         <el-button v-if="supt === 3" @click="pause">暂停</el-button>
         <el-button v-if="supt === 4" @click="resume">继续</el-button>
         <el-button v-if="supt > 1" @click="reset">重置</el-button>
       </el-col>
     </el-row>
</template>

 <script>
 export default {
   name: 'times-vue',
   props: {
     allTimes: Number,
     title: String
   },
   data() {
     return {
       supt: 1,
       time: this.allTimes,
       // 当前倒计时时间（秒）
       currentTime: this.allTimes,
       // 计时器ID
       timerID: null,
       temp : 0
     };
   },
   mounted() {
   },
   methods: {
     start() {
       this.supt = 3
       this.currentTime = this.time;
       this.timerID = setInterval(() => {
         this.currentTime--;
         this.time = this.currentTime;
         if (this.currentTime < 0) {
           clearInterval(this.timerID);
           this.reset();
           this.start()
         }
       }, 1000);

     },
     // 暂停
     pause(){
       clearInterval(this.timerID);
       this.supt = 4;
     },
     // 继续
     resume(){
       this.supt = 3;
       this.start();
     },
     reset(){
       clearInterval(this.timerID);
       this.supt = 1;
       this.time = this.allTimes;
       this.currentTime = this.allTimes;
     }
   }
 }
 </script>