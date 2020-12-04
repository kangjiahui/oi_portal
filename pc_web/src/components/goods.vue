
<!--这个界面用来：在用户d登录之后，展示视频流-->


<template>
  <div>
    <el-row>
      <el-col :span="5">
        <div class="grid-content-userInfo bg-purple-dark-userInfo"></div>
      </el-col>
      <el-col :span="14">
        <div class="grid-content-userInfo bg-purple-dark-userInfo">
          <!--左边-->
          <el-col :span="12" class="grid">
            <div class="demo-img-userPhoto">
              <img :src="'data:image/jpeg;base64,'+ flow_img"
                   style="width: 400px;height: 400px; margin-right: 200px"></img>
            </div>

            <div class="demo-input-userName" style="margin-top: 10px;">
              <el-row :gutter="2">
                <el-col :span="10">输入待检测人name/ID:
                </el-col>
                <el-col :span="12">
                  <el-input
                      :disabled="false"
                      style="margin-top: -6px;"
                      type="textarea"
                      autosize
                      placeholder="name/ID(选填)"
                      v-model="textArea_specific_user">
                  </el-input>
                </el-col>
              </el-row>
            </div>

            <div class="demo-button-signInOut" style="margin-top: 10px;">
              <el-button type="primary" style="margin: 5px" @click.prevent="start_detc()">开始检测</el-button>
              <el-button type="primary" style="margin: 5px" @click.prevent="stop_detc()">暂停检测</el-button>
            </div>

          </el-col>
          <!--右边-->
          <el-col :span="12" class="grid">

            <div class="demo-img-userPhoto">
              <img :src="'data:image/jpeg;base64,'+ flow_img_moment"
                   style="width: 400px;height: 400px; margin-right: 200px"></img>
            </div>

            <div class="demo-input-email" style="margin-top: 10px;">
              <el-row :gutter="2">
                <el-col :span="7">
                  <div style="text-align: right">
                    检测到的人数 :
                  </div>
                </el-col>
                <el-col :span="15">
                  <el-input
                      :disabled="true"
                      style="margin-top: -6px;"
                      type="textarea"
                      autosize
                      v-model="textArea_user_num">
                  </el-input>
                </el-col>
              </el-row>
            </div>

            <div class="demo-input-email" style="margin-top: 10px;">
              <el-row :gutter="2">
                <el-col :span="7">
                  <div style="text-align: right">
                    检测到的人的姓名1 :
                  </div>
                </el-col>
                <el-col :span="15">
                  <el-input
                      :disabled="true"
                      style="margin-top: -6px;"
                      type="textarea"
                      autosize
                      v-model="textArea_user_name1">
                  </el-input>
                </el-col>
              </el-row>
            </div>

            <div class="demo-input-email" style="margin-top: 10px;">
              <el-row :gutter="2">
                <el-col :span="7">
                  <div style="text-align: right">
                    检测到的人的姓名2 :
                  </div>
                </el-col>
                <el-col :span="15">
                  <el-input
                      :disabled="true"
                      style="margin-top: -6px;"
                      type="textarea"
                      autosize
                      v-model="textArea_user_name2">
                  </el-input>
                </el-col>
              </el-row>
            </div>


          </el-col>
        </div>
      </el-col>
      <el-col :span="5">
        <div class="grid-content-userInfo bg-purple-dark-userInfo"></div>
      </el-col>
    </el-row>

    <!--        提示信息行-->
    <el-row>
      <el-col :span="5">
        <div class="grid-content-goods bg-purple-dark-goods"></div>
      </el-col>
      <el-col :span="14">
        <div class="grid-content-goods bg-purple-dark-goods">
          <h3 style="margin: 3px">
            注意！本网站仅用作人脸检测和识别的展示，并不代表正式应用场景<br/>
          </h3>
          <br>
          <h3 style="margin: 2px">
            网站似乎出问题了？请联系 tangjiank@enn.cn<br/>
          </h3>

        </div>
      </el-col>
      <el-col :span="5">
        <div class="grid-content-goods bg-purple-dark-goods"></div>
      </el-col>
    </el-row>

    <br>
  </div>
</template>
<style>
/*搜索行，样式全局影响，要特殊命名*/
.bg-purple-dark-userInfo {
  background: Transparent;
}

.grid-content-userInfo {
  border-radius: 0px;
  min-height: 30px;
}
.bg-purple-dark-goods {
  background: Transparent;
}

.grid-content-goods {
  border-radius: 0px;
  min-height: 30px;
}
.bg-purple-dark-goods2 {
  background: #E5E5E5;
}

.grid-content-goods2 {
  border-radius: 0px;
  min-height: 100px;
}
</style>
<script>
export default {
  created() {
    this.initUserInfo();
  },
  data() {
    return {
      textArea_specific_user: '',
      textArea_user_num: '',
      textArea_user_name1: '',
      textArea_user_name2: '',
      flow_img: '',
      flow_img_moment: ''
    };
  },
  methods: {

    // 界面进来就会根据localStorage存储的当前用户信息，初始化用户详情
    initUserInfo() {
      // this.$message({
      //   showClose: true,
      //   type: 'success',
      //   message: '服务器连接畅通，随时可以开车'
      // });

      this.$message({
        showClose: true,
        type: 'warning',
        message: '服务器连接失败,所以有些功能无法使用~'
      });

    },



    start_detc() {
      this.$http.put("mainView/getUserInfo", {
        userId: 2 // 1是管理员admin,2是gust
      }).then(result => {
        var result = result.body;
        if (result.code === 200) {
          localStorage.removeItem('loginResult');
          localStorage.setItem('loginResult', JSON.stringify(result.data))
          this.textAreaUserName = JSON.parse(localStorage.getItem('loginResult')).userName;
          this.textAreaEmail = JSON.parse(localStorage.getItem('loginResult')).email;
          this.textAreaPhoneNum = JSON.parse(localStorage.getItem('loginResult')).phoneNumber;
          this.textAreaJoinTime = this.getLocalTime(JSON.parse(localStorage.getItem('loginResult')).createDate);
          this.textAreaState = JSON.parse(localStorage.getItem('loginResult')).state;
          this.textAreaLostFoundKey = JSON.parse(localStorage.getItem('loginResult')).lostFoundKey;
          this.demoUserImage = JSON.parse(localStorage.getItem('loginResult')).userDetail;
          this.setAddress();
        } else {
          this.$message('服务器异常');
        }
      });
    },

    stop_detc() {
      this.$http.put("mainView/getUserInfo", {
        userId: 2 // 1是管理员admin,2是gust
      }).then(result => {
        var result = result.body;
        if (result.code === 200) {
          localStorage.removeItem('loginResult');
          localStorage.setItem('loginResult', JSON.stringify(result.data))
          this.textAreaUserName = JSON.parse(localStorage.getItem('loginResult')).userName;
          this.textAreaEmail = JSON.parse(localStorage.getItem('loginResult')).email;
          this.textAreaPhoneNum = JSON.parse(localStorage.getItem('loginResult')).phoneNumber;
          this.textAreaJoinTime = this.getLocalTime(JSON.parse(localStorage.getItem('loginResult')).createDate);
          this.textAreaState = JSON.parse(localStorage.getItem('loginResult')).state;
          this.textAreaLostFoundKey = JSON.parse(localStorage.getItem('loginResult')).lostFoundKey;
          this.demoUserImage = JSON.parse(localStorage.getItem('loginResult')).userDetail;
          this.setAddress();
        } else {
          this.$message('服务器异常');
        }
      });
    },


    // 占据末尾的function ，不会被调用，请在它上面添加functions ，
    useless_f() {
      this.$message({
        message:'道路畅通，随时可以开车',
        type: 'success'
      });
    }


  }
};
</script>