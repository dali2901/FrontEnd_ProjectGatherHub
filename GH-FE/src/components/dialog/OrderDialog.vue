<template>
  <div class="overlay"></div>
  <div class="meetint-info-dialog">
    <h2>訂單資訊</h2>
    <button class="btn-close" @click="closeDialog">╳</button>
    <div class="info-area">
      <h3 id="od-number">訂單編號：{{ orderId }}</h3>

      <label v-for="(field, index) in fields" :key="index">
        <div :class="['h3-box', field.label === '備註' ? 'note-div' : '']">
          <h3 :class="field.label === '備註' ? 'note-h3-box' : ''">{{ field.label }}</h3>
        </div>
        <div :class="['data-box', field.label === '備註' ? 'note-box' : '']" v-if="!field.editing">{{ field.value }}</div>
        <input v-else type="text" v-model="field.inputValue" :class="['input-field', field.label === '備註' ? 'note-input' : '']" />
      </label>

      <div class="deposit"><h3>訂金：</h3><p>{{ deposit }}</p></div>
      <div class="total"><h3>總額：</h3><p>{{ total }}</p></div>
    </div>
    <button v-if="!editing" class="btn-edit" @click="startEditing">修改訂單</button>
    <button v-else class="btn-confirm" @click="confirmEdit">確認修改</button>
    <!-- <button class="btn-cancle" @click="cancleOrder">取消訂單</button> -->
    <CancleOrderButton/>
  </div>
</template>

<script>
import CancleOrderButton from '../button/CanaleOrderButton.vue'

export default {
  emits: ['close', 'confirm','edit'],
  components: {
    CancleOrderButton
  },
  data() {
    return {
      note: '這裡是備註內容',
      deposit: '$2100',
      total: '$4700',
      showDialog: false,
      eventNameInput: '',
      editing: false,
      fields: [
        {
          label: '日期',
          value: '2021/09/17',
          inputValue: '',
          editing: false
        },
        {
          label: '時間',
          value: '09:00-12:00',
          inputValue: '',
          editing: false
        },
        {
          label: '場地',
          value: 'A',
          inputValue: '',
          editing: false
        },
        {
          label: '活動名稱',
          value: '光明高中2022音樂會',
          inputValue: '',
          editing: false
        },
        {
          label: '聯絡人',
          value: '小飛象',
          inputValue: '',
          editing: false
        },
        {
          label: '公司名稱',
          value: '美商迪士尼科技股份有限公司',
          inputValue: '',
          editing: false
        },
        {
          label: '統編',
          value: '25947861',
          inputValue: '',
          editing: false
        },
        {
          label: '電話',
          value: '14-5497-9245',
          inputValue: '',
          editing: false
        },
        {
          label: '信箱',
          value: 'ajkldie@gmail.com',
          inputValue: '',
          editing: false
        },
        {
          label: '備註',
          value: '備註內容',
          inputValue: '',
          editing: false
        },
        // ...略...
      ],
    };
  },
  methods: {
    closeDialog() {
      this.$emit('close');
    },
    handleConfirm() {
      console.log('開啟修改窗'); 
      // this.$emit('edit');
      // this.$emit('close'); 
      
    },
    startEditing() {
      this.fields.forEach(field => {
        field.inputValue = field.value;
        field.editing = true;
      });
      this.editing = true;
      this.eventNameInput = this.eventName; // 将原始的活动名称赋值给输入框
    },
    confirmEdit() {
      this.fields.forEach(field => {
        field.value = field.inputValue;
        field.editing = false;
      });
      this.eventName = this.eventNameInput; // 更新活动名称为修改后的值
      this.editing = false;
      this.$emit('confirm');
      this.$emit('confirm', this.eventName);
    },
    cancleOrder(){
      
    },
  },
};
</script>


<style scoped>
*{
  font-family: '微軟正黑體';
}
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5); /* 设置半透明的黑色背景 */
  z-index: 9999; /* 确保遮罩层在其他内容之上 */
}
.meetint-info-dialog{
  width: 920px;
  height: 600px;;
  background-color: #ffffff;
  position: fixed;
  z-index: 99999;
  top: 9%;
  left: 20%;
  border-radius: 20px;
}
.btn-close {
  background-color: #ffffff; 
  position: absolute;
  top: 10px;
  right: 10px;
  width: 30px;
  height: 30px;
  border-radius: 50%;
  color: #949191;
  font-size: 20px;
  border: none;
  cursor: pointer;
}
.btn-close:hover {
  color: #676565;
  cursor: pointer;
}
.btn-cancle{
  position: absolute;
  right: 15%;
  bottom: 13%;
  width: 88px;
  height: 34px;
  color: #FFF;
  background-color: #D65151;
  border-radius: 15px;
  border: 0px;
  cursor: pointer;
}
.btn-cancle:hover{
  background-color: #ce6d6d;
  transition: background-color 0.8s;
}
.btn-edit{
  position: absolute;
  right: 15%;
  bottom: 20%;
  width: 88px;
  height: 34px;
  color: #FFF;
  background-color: #BCB0B0;
  border-radius: 15px;
  border: 0px;
  cursor: pointer;
}
.btn-edit:hover{
  background-color: #9c9191;
  transition: background-color 0.8s;
}
.btn-confirm{
  position: absolute;
  right: 15%;
  bottom: 20%;
  width: 88px;
  height: 34px;
  color: #FFF;
  background-color: #f9c06c;
  border-radius: 15px;
  border: 0px;
  cursor: pointer;
}
.btn-confirm:hover{
  background-color: #ffd9a0;
  transition: background-color 0.8s;
}
.meetint-info-dialog h2{
  font-size: 26px;
  position: relative;
  top: 18px;
  text-align: center;
  color: #7D5F4F;
  font-weight:500;
}
.info-area{
  position: relative;
  top: 36px;
}


.meetint-info-dialog label {
  display: flex;
  /* align-items: center; */
  margin-bottom: 2px;
  height: 40px;
}

.meetint-info-dialog h3{
  font-size: 16px;
  font-weight: 600;
  position: relative;
  top: -10px;
  /* left: 80px; */
  text-align: center;
  color: #7d5f4fbe;
}
.data-box{
  text-align: left;
  position: absolute;
  width: 300px;
  height: 36px;
  left: 205px;
  border-radius: 10px;
  border: 0px;
  outline: none;
  color: #777777;
  font-size: 14px;
  padding-left: 10px;
  margin-top: 8px;
}
.h3-box{
    background-color: #FFF7EA; 
    position: absolute;
    left: 110px;
    width: 100px;
    height: 35px;
    border-radius: 5px;
}
input{
  text-align: left;
  position: absolute;
  width: 200px;
  height: 30px;
  left: 200px;
  border-radius: 5px;
  color: #777777;
  font-size: 14px;
  padding-left: 10px;
  margin-left: 12px;
  outline: none;
  border: 0.5px solid #d1c7bf93;
  box-shadow: none;
}
.note-div{
    border: #7d5f4f59 solid 0.5px;
    background-color: #FFF;
    position: absolute;
    left: 500px;
    top: 50px;
    width: 300px;
    height: 150px;
    border-radius: 5px;
}
.note-h3-box{
    background-color: #FFF7EA; 
    position: absolute;
    top: 0px;
    right: 0px;
    width: 300px;
    height: 35px;
    border-radius: 5px;
    margin-top: 10px;
}

.note-box{
    position: absolute;
    left: 500px;
    top: 90px;
    width: 300px;
    height: 150px;
    border-radius: 5px;
    color: #D65151;
}

.note-input{
  position: absolute;
    left: 500px;
    top: 87px;
    width: 287px;
    height: 110px;
    border-radius: 5px;
    color: #D65151;
    margin-left: 0px;
}
.deposit {
  display: flex; /* 使用弹性布局 */
  align-items: center; /* 垂直居中对齐 */
  text-align: left;
  font-size: 16px;
  position: absolute;
  top: 350px;
  right:320px;
}
.deposit p{
  color: #D65151;
  position: relative;
  top: -10px;
}
.total {
  display: flex; /* 使用弹性布局 */
  align-items: center; /* 垂直居中对齐 */
  text-align: left;
  font-size: 16px;
  position: absolute;
  top: 380px;
  right:320px;
}
.total p{
  color: #D65151;
  position: relative;
  top: -10px;
}

/* 訂單編號 */
#od-number{
  font-size: 18px;
    position: relative;
    left: -285px; 
    top: 5px;
    color: #8B827B;
}
</style>