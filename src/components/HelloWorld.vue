<template>

    <div class="box">
         <div class="tou">
           <div class="item_input">
            <label itemid="name">名称：</label>
            <el-input style=" width: 390px;height: 40px;" v-model="input" id="name" placeholder="请输入名称查询"></el-input> 
           </div>
          
           <div class="item_input">
            <label itemid="age">年龄：</label>
            <el-input  style=" width: 390px;height: 40px;" v-model="input" id="age" placeholder="请输入年龄查询"></el-input>
           </div>
           <div class="item_input">
             <el-button  type="primary" icon="el-icon-search">查询</el-button>
             <el-button  type="primary" icon="el-icon-refresh-right">重置</el-button>
             <el-button  type="primary" icon="el-icon-takeaway-box">高级查询</el-button>
            
             <el-dropdown>
              <span style="color:#0780f2; margin-left: 10px;">展开<img src="../assets/展开.png" style="width:15px;height:15px;margin-left: 5px; position:relative; top: 1px;"/></span>
                  <el-dropdown-menu slot="dropdown">
                   <el-dropdown-item>a</el-dropdown-item>
                   <el-dropdown-item>b</el-dropdown-item>
                   <el-dropdown-item>c</el-dropdown-item>
                   <el-dropdown-item disabled>d</el-dropdown-item>
                   <el-dropdown-item divided>e</el-dropdown-item>
                   </el-dropdown-menu>
            </el-dropdown>
            </div>
         </div>
 
         <div class="tou_two">
           <div class="items_btn">
            <el-button type="primary" icon="el-icon-plus">新增</el-button>
            <el-button icon="el-icon-plus"  type="primary">创建单据</el-button>
            <el-button icon="el-icon-plus"  type="primary">一对多</el-button>
            <el-button icon="el-icon-download" type="primary">导出</el-button>
            <el-button icon="el-icon-upload" type="primary">导入</el-button>
           </div>
         </div>

         <div class="tou_three">
            <div class="all">
             <div class="left">
                <span>已选择<span style="color:#1172f1">0</span>项</span>
                <span style="color:#1172f1;margin-left: 30px;">
                  <el-button style="border:none;background-color:#e6f7ff; color:#1172f1" >清空</el-button>
                </span>
             </div>
             <div class="right">
                <span style="margin-right: 20px;">
                  <!-- <img src="../assets/刷新.png" style="width:15px; height:15px;position:relative; top:1px"/>刷新 -->
                  <el-button
                     style="border:none;background-color:#e6f7ff; color:#1172f1"
                     type="primary"
                     @click="openFullScreen1"
                     v-loading.fullscreen.lock="fullscreenLoading"
                     icon="el-icon-refresh-right">
                      刷新
                  </el-button>
                </span>
                <span><img src="../assets/符号-自定义列.png" style="width:15px; height:15px;position:relative; top:1px"/>自定义列</span>
            </div>
           </div>
         </div>

         <div class="foot">
          <el-table
             ref="multipleTable"
             :data="tableData"
             tooltip-effect="dark"
             style="width: 100%"
             @selection-change="handleSelectionChange">
               <el-table-column type="selection" width="65" align="center" :resizable="false">
               </el-table-column>
               <el-table-column label="#" type="index" width="65" align="center" :resizable="false"></el-table-column>
               <el-table-column prop="name" label="姓名" width="120" show-overflow-tooltip align="center" :resizable="false"></el-table-column>
               <el-table-column prop="kword" label="关键词" width="187" show-overflow-tooltip align="center" :resizable="false"></el-table-column>
               <el-table-column prop="ctime" label="打卡时间" width="300" show-overflow-tooltip align="center" :resizable="false"></el-table-column>
               <el-table-column prop="gender" label="性别" width="90" show-overflow-tooltip align="center" :resizable="false"></el-table-column>
               <el-table-column prop="age" label="年龄" width="90" show-overflow-tooltip align="center" :resizable="false"></el-table-column>
               <el-table-column prop="bday" label="生日" width="200" show-overflow-tooltip align="center" :resizable="false"></el-table-column>
               <el-table-column prop="email" label="邮箱" width="350" show-overflow-tooltip align="center" :resizable="false"></el-table-column>
               <el-table-column prop="resume" label="个人简历" width="140" show-overflow-tooltip align="center" :resizable="false"></el-table-column>
               <el-table-column prop="palys" width="220" align="center" :resizable="false">
                <template slot="header">
                  <span>操作</span>
                  <img src="../assets/205设置-线性.png" style="width:2opx;height:20px;float:right; margin-right:5px;"/>
                 </template>
                  <template>
                      <span style="color:#70bbfa"><el-button @click="show()" style="border:none; color: #70bbfa;">编辑</el-button></span><span style="color:#70bbfa; margin: auto 5px;">|</span>
                      <span style="color:#70bbfa"><el-button style="border:none; color: #70bbfa;">更多<img src="../assets/展开.png" style="width:15px;height:15px;position: relative; top: 3px; left: 2px;"/></el-button></span>
                  </template>
               </el-table-column>
            </el-table>
               
              <div style="float:right; margin-right:5px; margin-top: 10px;">
                <el-pagination
                    @size-change="sizeChange"
                    @current-change="currentChange"
                    :current-page="currentPage"
                    :page-size="10"
                    :page-sizes="[10, 20, 30, 40]"
                    layout="total, sizes, prev, pager, next, jumper"
                    :total="10">
                </el-pagination>
             </div>
         </div>

       <!--弹窗窗口-->
        <el-dialog
        :modal="true"
        :modal-append-to-body="true"
        :title="tittle"
        :visible.sync="isShow"
        :close-on-click-modal="false"
        :show-close="false"
        :close-on-press-escape="false"
        :width="width"
        :height="height"
        center>
        <el-button style="border:none;background-color:white; color:#1172f1;float: right; position: relative;left:20px; bottom: 70px;" icon="el-icon-close" @click="quxiao()"></el-button>
        <el-form ref="form" :model="form" label-width="80px" style="position:relative;left:80px">
               <el-form-item label="姓名:" style="margin-top: 5px; margin-bottom:35px;width:600px">
                 <el-input v-model="form.name" placeholder="请输入姓名"></el-input>
               </el-form-item>

               <el-form-item label="关键词" style="margin-bottom:35px;width:600px">
                 <el-input v-model="form.kword" placeholder="请输入关键词"></el-input>
               </el-form-item>

               <el-form-item label="打卡时间" style="margin-bottom:35px;width:600px">
                <el-col :span="11">
                  <el-date-picker type="date" placeholder="选择日期" v-model="form.ctime" style="width: 100%;"></el-date-picker>
                </el-col>
               </el-form-item>

               <el-form-item label="sex" style="margin-bottom:35px;width:600px">
                 <el-input v-model="form.sex" placeholder="请输入性别"></el-input>
               </el-form-item>

               <el-form-item label="年龄" style="margin-bottom:35px;width:600px">
                 <el-input v-model="form.age" placeholder="请输入年龄"></el-input>
               </el-form-item>

               <el-form-item label="生日" style="margin-bottom:35px;width:600px">
                <el-col :span="11">
                  <el-date-picker type="date" placeholder="选择日期" v-model="form.bday" style="width: 100%;"></el-date-picker>
                </el-col>
               </el-form-item>

               <el-form-item label="邮箱" style="margin-bottom:40px;width:600px">
                 <el-input v-model="form.email" placeholder="请输入邮箱"></el-input>
               </el-form-item>

               <el-form-item label="个人简历" style="width:600px">
                 <el-input v-model="form.resume" placeholder="请输入个人简历"></el-input>
               </el-form-item>
       </el-form>

        <div slot="footer" class="dialog-footer">
            <el-button @click="quxiao()">取 消</el-button>
            <el-button type="primary" @click="sumbim()">确 定</el-button>
        </div>
    </el-dialog>

    </div>
   
</template>

<!-- 引入样式 -->
<link rel="stylesheet" href="https://unpkg.com/element-ui/lib/theme-chalk/index.css"/>
<!-- 引入组件库 -->
<script src="https://unpkg.com/element-ui/lib/index.js">
import InfoEdit from './InfoEdit.vue';</script>


<script>

export default {
  name: 'HelloWorld',
  data(){
      return{

        fullscreenLoading: false,
       
        tittle:"编辑",
        isShow:false,
        width:"800px",
        height:"750px",
        form: {
              name: '',
                region: '',
          },


        input:null,
        currentPage:null,
        tableData: [{
        ctime: '2016-05-02',
        name: '王小虎',
        kword: '上海市普陀区金沙江路 1518 弄',
        gender:'',
        age:15,
        bday:'2002-03-28',
        resume:'打卡',
        email:'aaa@qq.com'
      },{
        ctime: '2016-05-02',
        name: '张三',
        kword: '广东中山',
        gender:'',
        age:25,
        bday:'2000-11-3',
        resume:'打卡',
        email:'bbb@qq.com'
      }],
      loading: true
      }
    },
  methods:{
      getTableData(){
        this.tableData = this.allData.slice(
           (this.page-1)*this.size,
           this.page*this.size
        );
        this.total = this.allData.length
      },
      currentChange(val){
        console.log('翻页，当前为第几页',val);
        this.page = val;
        this.getTableData();
      },
      sizeChange(val){
        console.log('当前页多少条数据',val);
        this.size = val;
        this.page = 1;
        this.getTableData();
     },

     //全选
     toggleSelection(rows) {
        if (rows) {
          rows.forEach(row => {
            this.$refs.multipleTable.toggleRowSelection(row);
          });
        } else {
          this.$refs.multipleTable.clearSelection();
        }
      },
      handleSelectionChange(val) {
        this.multipleSelection = val;
      },

      show(){
           this.isShow=true;
           this.isShow== !this.isShow;
           console.log(this.isShow);
      },

      sumbim(){
          this.isShow = false
      },
      
      quxiao(){
          this.isShow = false
        },

        //加载动画
      openFullScreen1() {
        this.fullscreenLoading = true;
        setTimeout(() => {
          this.fullscreenLoading = false;
        }, 2000);
       },

      


    },
  

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  *{
    margin: 0;
    padding: 0;
  }
   .box{
    margin: 10px auto;
    background-color: white;
    width: 1890px;
    height: 875px;
    font-size: 15px;
    border: 1px solid gray;
   }
   .box>.tou{
    margin: 0 auto;
    height: 80px; 
    width: 1830px;
   }
   .box>.tou>.item_input{
    width: 445px;
    height: 80px;
    line-height: 80px;
    float: left;
   }

   /*tou_two*/
   .box>.tou_two{
    margin: 0 auto;
    height: 80px; 
    width: 1830px;
    line-height: 80px;
   }
   .box>.tou_two>.items_btn{
      float: left;
      margin-left: 3px;
   }

   /*tou_three*/
   .box>.tou_three{
    margin: 0 auto;
    height: 80px; 
    width: 1830px;
   }
   .box>.tou_three>.all{
     width: 1830px;
     height: 45px;
     background-color: #e6f7ff;
     border-radius: 10px;
     border: 1px solid #c6e6fc;
     line-height: 45px;
   }
   .all>.left{
      float: left;
      margin-left: 40px;
   }
   .all>.right{
    float: right;
    margin-right: 40px;
    color: #8ac4e9;
   }

   /*foot*/
   .box>.foot{
     margin: 0 auto;
     width: 1830px;
     text-align: center;
   }
   .foot>el-table{
    text-align: center;
   }


   .divauto{
        margin:  10px auto 0 auto;
     }
    .model-container{
        width: 840px;
        height: 750px;
        padding: 20px;
        border: none;
        box-shadow: #333 0 0 2px;

        position: absolute;
        top: 65px;
        left: 800px;
        box-shadow: white;
        background-color: white;
        text-align: center;
    }

    .info_form{
        width: 800px;
        text-align: center;
        padding: 20px;
        border-left: none;
        border-right: none;
        border-top: 1px solid #9f9fab;
        border-bottom: 1px solid #9f9fab;
    }

</style>
